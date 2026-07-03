---
name: monthly-seo-report
description: Generate monthly SEO reports for active TWG SEO clients on the 1st of each month. Produces an internal ClickUp report (with traffic-light diagnostics) and, after approval, a client-facing branded PDF. Use when someone says "run the SEO reports", "monthly SEO report", "generate the SEO report", "SEO client reports", "run the monthly reports for SEO clients", or "create the SEO report for [client]". Only reports on clients with an active SEO service in the ClickUp Account Health Tracker. Output is a draft for Ehtisham to review — no client PDFs are generated without approval.
---

# Monthly SEO Report

Automated monthly SEO reporting for active TWG clients. Pulls data from Google Search Console, Google Analytics 4, DataForSEO, Google Business Profile, and SE Ranking. Produces two outputs per client:

1. **Internal report** — full diagnostic data with traffic-light indicators, posted as a ClickUp task description for internal review.
2. **Client-facing PDF** — a positive, visual summary focused on wins and opportunities, generated only after internal approval.

The single most important rule: *present client-facing reports positively. Focus on wins, improvements, and opportunities. Keep diagnostic detail and negative trends for internal reports only. Never fabricate data — if a source is unavailable, say so.*

## Inputs

- **Client roster** (auto-discovered) — pulled live from the ClickUp Account Health Tracker. Only clients with the `SEO` service set to active are included. See `references/client-discovery.md`.
- **Account mapping** (required) — `references/account-mapping.md` explains how client shortcodes map to GSC properties, GA4 property IDs, GBP location IDs, and DataForSEO targets. A client must appear in both the ClickUp roster and have mapped accounts to be reported on.
- **Reporting period** — always the previous complete calendar month (e.g. on 1 July, report on 1–30 June). Comparison period is the month before that.

Missing-input handling: if the ClickUp view is unreachable or a client has no mapped accounts, skip that client and log a warning. Do not guess account IDs.

## Workflow

### Step 0 — Discover active SEO clients

Query the ClickUp Account Health Tracker to get the current roster of active SEO clients. Cross-reference against the account mapping to resolve data source IDs. See `references/client-discovery.md` for the exact logic.

If a client is in the ClickUp view but has no mapping entry, skip them and log a warning.

### Step 1 — One-time setup (first run only)

For each SEO client, check whether their ClickUp folder already has a **Reporting** list. If not, create one. Future reports go into this list. This only needs to happen once per client.

### Step 2 — Pull data from all sources

For each client, pull data from the available sources for the reporting period. See `references/data-sources.md` for the exact API calls and fields.

| Source | Data pulled |
|--------|------------|
| Google Search Console | Clicks, impressions, CTR, position by query and page |
| Google Analytics 4 | Sessions by channel, top landing pages, key conversion events |
| DataForSEO | Keyword rankings, estimated search volume, backlink profile, website audit score, AI/LLM visibility |
| Google Business Profile | Call clicks, website clicks, direction requests, search vs maps views, reviews, posts published |
| SE Ranking | Keyword position tracking, competitor comparison (when available) |

**If an API call fails** (auth error, rate limit, timeout): skip that data source for that client. Do not include partial or stale data. Log the client name, data source, and error reason — these are reported in Step 6.

### Step 3 — Generate internal report

For each client with valid data, produce an internal report using the traffic-light format. Post the report as the **task description** (not a comment) in a new ClickUp task in the client's Reporting list. See `references/internal-report-spec.md` for the exact format.

Key rules for internal reports:
- Apply the traffic-light system (🟢 🟡 🔴) to every metric for visual status at a glance.
- Clearly identify anything urgent.
- Include full diagnostic detail — this is for the team, not the client.
- Assign each task to Ehtisham (ClickUp ID: `48626346`).

### Step 4 — Extract notable wins

For each client, extract 3 key wins that showcase only positive outcomes. These are short, punchy statements with concrete numbers — before/after comparisons, percentage increases, or absolute figures. See `references/notable-wins-spec.md` for the format.

Post the 3 wins as a separate section at the top of the ClickUp task description, marked for approval. Once approved, these go to the marketing team for use in client communications.

### Step 5 — Wait for approval

The internal report and notable wins must be reviewed and approved in ClickUp before any client-facing PDF is generated. Add a checklist item or approval mechanism to the ClickUp task so that Ehtisham (or another reviewer) can approve the report for client-facing output.

Do not generate the client-facing PDF until the task is explicitly approved.

### Step 6 — Generate client-facing PDF (after approval only)

Once approved, generate a TWG-branded PDF report for the client. This report follows a strict positive-framing approach. See `references/client-report-spec.md` for the exact sections, what to include, and what to exclude.

Key rules for client-facing reports:
- Focus on wins, improvements, and opportunities.
- Only compare with the previous period when there is a positive improvement. Avoid highlighting negative declines.
- If a significant Google Search algorithm update occurred during the reporting period, include a short note: "Google released an algorithm update during this period. We have already adjusted the SEO strategy accordingly."
- CTA at the bottom: "Questions about this report? Reply to this email, or contact us at Support@TradieWebGuys.com.au"
- Never use the link go.tradiewebguys.com.au/book as the CTA.

### Step 7 — Post summary to Slack

Post a summary to the appropriate Slack channel listing:
- Total SEO clients reported on and the reporting period.
- Clients with urgent items (name + one-line finding).
- Clients skipped due to API errors (name + reason).
- Links to the ClickUp tasks.

## Output

- **ClickUp**: One task per client in their Reporting list, with the internal report as the task description and 3 notable wins at the top. Assigned to Ehtisham.
- **Client-facing PDF** (after approval): TWG-branded PDF uploaded to the ClickUp task and the client's Google Drive folder.
- **Slack**: Summary posted after report generation.

## Cron

- Schedule: Monthly on the 1st at 7am AEST (21:00 UTC previous day)
- Path: `/cron/monthly-seo-report`
- Credit check: before running, estimate the number of API calls required. If it looks like the run will exceed reasonable credit usage, message Matt in Slack for confirmation before proceeding.

## Guardrails

- Never fabricate metrics. If a data source is unavailable, skip it and report the gap. Do not fill in zeros or estimates.
- Do not report on clients outside the ClickUp roster, even if their accounts are accessible.
- Do not generate client-facing PDFs without explicit approval on the ClickUp task.
- Client-facing reports must be positive. No red indicators, no decline callouts, no large negative graphs. Keep that detail for internal reports only.
- Post the report in the ClickUp task description, never in the comments.
- Always create the ClickUp task first before generating any PDF.
- Writing: plain, direct, active sentences. Australian English spelling (colour, organise, realise). Avoid generic filler vocabulary.
- Never share internal-only diagnostic detail in client-facing output.

## Reference files

| File | Use it for |
|------|------------|
| `references/client-discovery.md` | Step 0 — how to query ClickUp and resolve client accounts |
| `references/data-sources.md` | Step 2 — exact API calls, fields, and fallback handling per source |
| `references/internal-report-spec.md` | Step 3 — internal report format with traffic-light system |
| `references/notable-wins-spec.md` | Step 4 — format for the 3 key wins per client |
| `references/client-report-spec.md` | Step 6 — client-facing PDF sections, includes, and excludes |
| `references/clickup-output.md` | Steps 3–5 — ClickUp task structure, naming, and approval flow |
| `references/account-mapping.md` | How client shortcodes map to data source IDs |
