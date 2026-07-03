---
name: pre-report-access-audit
description: Run a pre-flight access audit before any scheduled report to verify Viktor has working access to every required integration for every client. Use when someone says "run the access audit", "check report access", "pre-report access check", "verify tool access", "do we have access to everything", "check the integrations before the report", or "access audit for SEO clients" or "access audit for ads clients". Also runs automatically on a cron before each scheduled report cadence. Posts a pass/fail summary to Slack and alerts the team to fix any issues before the report is due. Never allows a report to run with known missing access.
---

# Pre-Report Access Audit

Verify that Viktor has working access to every integration required for a scheduled report, for every client on that report's roster, *before* the report runs. If any access is missing, alert the team in Slack with enough lead time to fix it.

The single most important rule: *no scheduled report should ever run if this audit has flagged a missing integration that has not been resolved. Catch it early, fix it early.*

## Inputs

- **Report type** (required) — which report to audit for: `SEO` (monthly SEO report), `ADS` (daily ads report), or `ALL` (both). When run by cron, the report type is set automatically based on the upcoming report.
- **Client** (optional) — a specific client shortcode to audit. If omitted, audit all active clients for the given report type.
- **Client roster** (auto-discovered) — pulled live from the ClickUp Account Health Tracker, same logic as the reports themselves. See `references/report-registry.md` for the filtering rules per report type.
- **Account mapping** (required) — the report skill's own mapping file provides the account/property IDs to check. SEO reports use the monthly-seo-report mapping; Ads reports use the daily-ads-report mapping.

Missing-input handling: if the ClickUp view is unreachable, post a Slack alert saying the access audit could not run because the client roster is unavailable. Do not guess the client list.

## Workflow

### Step 0 — Determine scope

Identify which report type is being audited and load the corresponding requirements from `references/report-registry.md`. This tells you:
- Which ClickUp service tags to filter on (e.g. `SEO`, `PDSOCL (META)`, `PDSRCH (GOOGLE)`)
- Which integrations each report requires per client
- Where the account mapping lives

### Step 1 — Discover active clients

Query the ClickUp Account Health Tracker (view `9d6k-155558`) to get the active client roster for the report type. Resolve each client's shortcode against the relevant account mapping file. If a client has no mapping entry, flag it immediately — that is already a failure.

### Step 2 — Run access checks

For each client, run a lightweight test call against every required integration. The exact calls are in `references/access-checks.md`. Each check must:
- Use the *minimum possible* API call (a list call, a tiny date range, or a metadata request) to confirm access without burning credits.
- Return a clear pass or fail.
- Capture the error reason on failure (auth expired, property not found, permission denied, rate limited, timeout).

Run checks in parallel where possible to keep the audit fast.

### Step 3 — Compile results

Build a results table per client:

```
Client          | GSC | GA4 | GBP | DFSO | SER | Status
Coffison Plumb. |  ✅  |  ❌  |  ✅  |  ✅   |  ⚠️  | FAIL
East Coast Elec.|  ✅  |  ✅  |  ✅  |  ✅   |  ✅  | PASS
```

Status per integration:
- ✅ `PASS` — access confirmed, test call returned valid data
- ❌ `FAIL` — access denied, property not found, or auth error
- ⚠️ `WARN` — access works but with a caveat (e.g. SE Ranking fallback expected, partial data)
- ⬜ `N/A` — integration not required for this client/report type

Overall client status:
- `PASS` — all required integrations passed
- `FAIL` — one or more required integrations failed
- `WARN` — all required passed but one or more have warnings

### Step 4 — Post Slack summary

Post the results to the `#agency-viktor` Slack channel. Format:

**If all clients pass:**
> ✅ *Pre-report access audit — all clear*
> All {N} clients for the {report type} report have confirmed access to every required integration. Report is clear to run on {date}.

**If any clients fail:**
> 🚨 *Pre-report access audit — action required*
> {N} of {M} clients have access issues that must be resolved before the {report type} report runs on {date}.
>
> *Failures:*
> • {Client Name} — {integration}: {error reason}
> • {Client Name} — {integration}: {error reason}
>
> *All clear:*
> • {Client Name}, {Client Name}, ...
>
> @Matt - OPS @Ehtisham — please resolve before {date}.

Always tag relevant team members when there are failures. For SEO reports, tag Ehtisham. For Ads reports, tag Ethan Carter. Always tag Matt.

### Step 5 — Block the report if failures exist

If any client has a `FAIL` status, the audit must prevent the corresponding report from running with missing data. Do this by:
1. Writing the audit results to a status file at `references/last-audit-result.json` with the timestamp, report type, and per-client pass/fail status.
2. The report skill checks this file before running. If the most recent audit for its report type has any unresolved `FAIL` entries, the report skill should skip those clients and note in its output that they were skipped due to a failed access audit.

When a failure is resolved (team confirms in Slack or re-runs the audit), update the status file.

## Output

- **Slack**: Pass/fail summary posted to `#agency-viktor` with tagged team members on failures.
- **Status file**: `references/last-audit-result.json` — machine-readable results for report skills to check.
- **Log**: Detailed per-client, per-integration results logged for debugging.

## Cron Schedule

| Report | Report runs | Audit runs | Path |
|--------|------------|------------|------|
| Monthly SEO Report | 1st of month, 7am AEST | 2 business days before the 1st (typically 28th–29th of prior month), 7am AEST | `/cron/pre-report-access-audit/seo` |
| Daily Ads Report | Daily, 6am AEST | Weekly on Monday, 5am AEST | `/cron/pre-report-access-audit/ads` |

"2 business days before" means: count backwards from the 1st, skipping weekends. If the 1st is a Monday, the audit runs on the prior Thursday. If the 1st is a Tuesday, the audit runs on the prior Friday.

The ads audit runs weekly (not daily) because the integrations rarely change. If a failure is detected, the team has until the next morning to fix it.

## Guardrails

- Use the lightest possible API calls. This skill exists to check access, not to pull report data. Minimise credit usage.
- Never fabricate access results. If a check call itself fails in an ambiguous way (timeout, rate limit), mark it as `WARN` with the reason, not as `PASS`.
- Do not fix access issues automatically. This skill detects and reports — humans fix.
- Do not skip the audit. If the cron fires and ClickUp is unreachable, post a Slack alert saying the audit could not run, rather than silently skipping it.
- Pause on missing inputs (no mapping file, no ClickUp view) and alert in Slack rather than guessing.

## Reference files

| File | Use it for |
|------|------------|
| `references/report-registry.md` | Step 0 — which integrations each report type requires, ClickUp filters, and mapping file locations |
| `references/access-checks.md` | Step 2 — exact lightweight API calls per integration to verify access |
