---
name: seo-monthly-report
description: Generate monthly SEO reports for active TWG SEO clients. Runs as two crons — a pre-flight access check on the last day of the month and the full report on the 2nd at 7am AEST. Produces an internal ClickUp report (traffic-light diagnostics, proposed client content) and, after PM approval, a TWG-branded client-facing PDF. Use when someone says "run the SEO reports", "monthly SEO report", "generate the SEO report for [client]", "run the monthly reports", "SEO client reports", or "create the report for [client]". Only reports on clients with an active SEO service in ClickUp and a completed setup (KB, STATE.md, strategy doc). Output is a draft for Ehtisham to review — no client PDFs are generated without approval.
---

# Monthly SEO Report

Automated monthly SEO reporting for active TWG clients. Two crons, one workflow:

1. **Pre-flight access check** (last day of month) — tests all 4 data source connections per client. Posts failures to the ClickUp urgent channel and Slack so the team has 48 hours to fix before the report runs.
2. **Report generation** (2nd of month, 7am AEST) — pulls data, builds internal report, waits for approval, then generates client PDF.

Each client gets two outputs:
- **Internal report** — full diagnostic data with traffic-light indicators (🟢🟡🔴), posted as a ClickUp task description in the client's Reporting list.
- **Client-facing PDF** — positive, visual summary focused on wins and opportunities. Generated only after the PM approves and edits the proposed content in ClickUp.

The single most important rule: **after PM approval, re-read the ClickUp task description to pick up all edits before generating the PDF. Never generate from cached/in-memory data.**

## Inputs

- **Client roster** — auto-discovered from ClickUp Account Health Tracker (list `901804854897`, SEO clients view `9d6k-264358`). Only clients with `SEO` service label + `Active` status.
- **Setup check** — client must have a Client KB (`skills/clients/{shortcode}/SKILL.md`), STATE.md (`skills/clients/{shortcode}/seo/STATE.md`), and strategy doc. Skip clients without complete setup.
- **Account mapping** — `references/account-mapping.md` maps shortcodes to GSC properties, GA4 property IDs, GBP location IDs, and DataForSEO targets.
- **Reporting period** — always the previous complete calendar month. Comparison = month before that.

If a client is in ClickUp but has no mapping entry or incomplete setup, skip and log a warning.

## Workflow

### Step 0 — Pre-flight access check (separate cron, last day of month)

For each active SEO client with a complete setup, run one lightweight API call per data source. See `references/access-checks.md` for the exact check methods.

| Source | Check | Pass | Fail |
|--------|-------|------|------|
| GSC | 1-day performance query | Returns data | Auth/permission error |
| GA4 | Property metadata GET | Returns property | Auth/not found |
| GBP | List locations | Location found | Auth/not found |
| DataForSEO | 1 keyword result | Returns result | Auth/API error |

**On failure:**
1. Post to ClickUp urgent channel (`9d6k-176338`), assigned to Ehtisham (`48626346`): "🚨 [Client Name] — [integration] connection failed. Error: [reason]. SEO report blocked until resolved."
2. Post Slack summary listing all pass/fail results.

**On pass:** No action needed — the report cron runs normally on the 2nd.

Timeouts (30s) are marked WARN, not FAIL. One retry after 5s for rate limits. See `references/access-checks.md` for full logic.

### Step 1 — Discover clients and check readiness (report cron)

Query the ClickUp Account Health Tracker SEO view (`9d6k-264358`). For each client:
1. Resolve shortcode from custom field.
2. Check account mapping exists.
3. Check Client KB, STATE.md, and strategy doc exist.
4. If any check fails, skip with a logged warning.

First-run setup: if the client's ClickUp folder has no **Reporting** list, create one.

### Step 2 — Pull data from all sources

For each ready client, pull data for the reporting period. See `references/data-sources.md` for exact API calls.

| Source | Key data |
|--------|----------|
| Google Search Console | Clicks, impressions, CTR, position by query (top 20) and page (top 15) |
| Google Analytics 4 | Sessions by channel, top landing pages, conversion events (calls/emails/forms only) |
| DataForSEO | Keyword rankings + volumes, backlinks summary, on-page audit score, AI/LLM visibility |
| Google Business Profile | Calls, clicks, directions, search/maps views, reviews, posts published |

**If an API call fails:** skip that source for that client. Log the error. Never use partial or stale data. Never fabricate metrics.

### Step 3 — Generate internal report + proposed client content

Create a ClickUp task in the client's Reporting list. See `references/internal-report-spec.md` for the full format.

**Task structure:**
- **Name:** `SEO Report — {Month Year}`
- **Assignee:** Ehtisham (`48626346`)
- **Status:** `in review`
- **Tags:** `seo-report`, `viktor`
- **Priority:** Normal (3)
- **Description** (using `markdownDescription`):
  1. Notable Wins section (top) — 3 concrete wins with numbers
  2. Full internal report — all sections with traffic-light indicators
  3. Proposed Client-Facing Report (bottom) — exact content for the PDF, populated with real data, positive framing applied, marked for review/edit

**Approval checklist** on the task:
- [ ] Internal report reviewed
- [ ] Notable wins approved for marketing
- [ ] Proposed client-facing content reviewed and edited
- [ ] Client-facing PDF approved for generation

See `references/notable-wins-spec.md` for win format. See `references/clickup-output.md` for full task structure.

### Step 4 — "Next Month" section: align with strategy

The "Next Month To-Do's" in both the internal and proposed client-facing content must be specific to the client's strategy — not generic bullets.

1. Read the client's current strategy doc (Section 4 content plan + Section 7 block goals).
2. Read the client's STATE.md for what was done last month and what's queued.
3. List the specific planned deliverables for next month (which pages, which blogs, which technical fixes).

### Step 5 — Detect block ending

Read the client's STATE.md to check if this is the final month of the current strategy block.

If yes: flag in the Slack summary — "📅 [Client Name]: Final month of Block N. Quarterly review due. PM to trigger: @Viktor run the quarterly review for [client]"

### Step 6 — Wait for approval

Do not generate any client-facing PDF until the ClickUp task checklist is fully ticked.

### Step 7 — Generate client-facing PDF (after approval only)

**Critical:** Re-read the ClickUp task description via API. Extract the Proposed Client-Facing Report section (Section 11) — including all PM edits. Generate the PDF from the re-read content only, never from cached data.

Apply TWG brand from `/work/brand/DESIGN.md`:
- Dark Navy `#1A1F2E` headers/footer with white logo
- Lime Green `#8DC63F` accents, metric highlights, section markers
- Outfit headings (Poppins fallback), Inter body text
- Off-White `#F5F4F2` page backgrounds
- Clean, structured layout

See `references/client-report-spec.md` for sections and rules. See `references/pdf-template.md` for the HTML template.

CTA at bottom: "Questions about this report? Reply to this email, or contact us at Support@TradieWebGuys.com.au" — never use go.tradiewebguys.com.au/book.

Upload PDF to the ClickUp task.

### Step 8 — Update STATE.md

After generating each report, update the client's STATE.md:
- Last report date
- Key metrics snapshot (for next month's comparison)
- What was done this month
- What's planned next month (from the approved report)
- Block progress

### Step 9 — Post Slack summary

Post to the reporting Slack channel:
- Total clients reported, reporting period
- Clients with urgent items (🔴 flags)
- Clients skipped (reason)
- Block-ending alerts
- Links to ClickUp tasks

## Cron Schedule

| Cron | When | Path |
|------|------|------|
| Pre-flight access check | Last day of month, 7am AEST | `/cron/seo-pre-flight` |
| Report generation | 2nd of month, 7am AEST | `/cron/seo-monthly-report` |

## Data Sources

Only these 4 SEO sources. No SE Ranking, no Meta Ads, no Google Ads:
- Google Search Console (`google_search_console`)
- Google Analytics 4 (`google_analytics`)
- DataForSEO (`dataforseo`)
- Google Business Profile (`google_my_business`)

## Guardrails

- Never fabricate metrics. If a source is unavailable, skip it and report the gap.
- **Every internal finding carries `[Impact: …]` and `[Evidence: L…]` tags, sorted by impact.** Read `skills/seo_knowledge_base/references/evidence-impact-framework.md`. Traffic lights map to impact: red = Critical/High, amber = Medium, green = resolved. Tool severity scores are not evidence — reclassify them.
- **Client PDFs never show evidence levels or the L1–L5 labels.** Translate impact to plain language ("Fix immediately" / "High priority" / "Recommended") and cut Informational findings entirely.
- Do not report on clients outside the ClickUp roster or without complete setup.
- Do not generate client-facing PDFs without explicit ClickUp checklist approval.
- After approval, MUST re-read the ClickUp task description to pick up PM edits. Never generate PDF from cached data.
- Client-facing reports are positive only. No 🟢🟡🔴 indicators, no decline callouts. Show current values without comparison when a metric declined.
- Always use `markdownDescription` for ClickUp tasks. Never pass `[table-embed:...]`.
- Always use `@Viktor` in ClickUp descriptions, not Slack user ID syntax.
- Australian English spelling (colour, organise, realise, optimise).
- Plain, direct, active sentences. No filler (delve, leverage, robust, seamless, unlock, streamline, elevate).
- Internal diagnostic detail stays internal. Never include in client-facing output.
- Reports must align with TWG brand visual guide (`/work/brand/DESIGN.md`).

## Reference files

| File | When to read |
|------|-------------|
| `references/access-checks.md` | Step 0 — lightweight API checks per source |
| `references/client-discovery.md` | Step 1 — ClickUp query and client resolution |
| `references/data-sources.md` | Step 2 — exact API calls and fields per source |
| `references/internal-report-spec.md` | Step 3 — full internal report format with traffic-light system |
| `references/notable-wins-spec.md` | Step 3 — format for the 3 wins per client |
| `references/client-report-spec.md` | Step 7 — client-facing PDF sections and rules |
| `references/clickup-output.md` | Step 3 — ClickUp task structure and approval flow |
| `references/account-mapping.md` | How shortcodes map to data source IDs |
| `skills/seo_knowledge_base/references/evidence-impact-framework.md` | Step 3 and Step 7 — impact/evidence classification and internal vs client-facing display rules |
| `references/pdf-template.md` | Step 7 — HTML template for branded PDF generation |
