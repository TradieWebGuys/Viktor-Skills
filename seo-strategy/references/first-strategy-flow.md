# First Strategy Flow (Onboarding)

Triggered by PM: `@Viktor create the SEO strategy for [SHORTCODE]`

---

## Step 0 — Validate Prerequisites

Check all 4 exist. If any missing, reply with what's not ready and stop.

| Prerequisite | How to check |
|---|---|
| Client KB | `skills/clients/{shortcode}/SKILL.md` exists and has confirmed services/locations |
| Services confirmed | KB has a `## Services` section populated (set by "Confirm Services & Locations" completion — see `references/service-confirmation-workflow.md`) |
| Content register | KB or STATE.md links to a Google Sheet; verify sheet exists via Sheets API |
| Keyword research | KB or STATE.md links to a Google Sheet; verify sheet exists via Sheets API |
| Site is crawlable | Content register confirms pages were found |

If the keyword research skill ran successfully, it would have posted a Slack message with "Prerequisites met for strategy doc." That's the PM's cue — but the strategy skill validates independently.

---

## Step 1 — Run Fresh DataForSEO Audit (Pre-Access)

Do NOT reuse the prospect audit. The prospect audit reflects what DataForSEO found pre-sale; the client's confirmed services may differ.

**Important:** At onboarding, the strategy doc is created BEFORE GSC/GA/GBP access is confirmed (see task order — "Confirm Access" and "Setup GSC & GA" come after "Create Strategy Doc"). This means the first strategy relies entirely on DataForSEO for audit data. GSC, GA, and GBP data become available for monthly reports and quarterly reviews.

**Calls to make (parallel where possible):**

1. **On-page crawl** — `pd_dataforseo_create_onpage_task` with `target={domain}`, `maxCrawlPages=100`. Poll until done. Extract:
   - Technical health score
   - Issue counts by severity (critical, warning, info)
   - Top issues for Section 6

2. **SERP/keyword rankings** — `pd_dataforseo_get_domain_keywords` with `target={domain}`, `locationCode=2036` (or NZ 2554), `limit=100`. Extract:
   - Total keywords ranking
   - Page-one count
   - Position distribution
   - Estimated traffic value (ETV)

3. **Backlink profile** — `pd_dataforseo_proxy_post` to `/v3/backlinks/summary/live`. Extract:
   - Referring domains
   - Domain rank
   - Total backlinks

4. **Competitor data** — For each competitor named in the KB, run `pd_dataforseo_get_domain_rank_overview` and `pd_dataforseo_get_domain_keywords`. Do NOT use `get_competitor_domains` — competitors come from the KB, not DataForSEO overlap.

5. **AIO/LLM visibility** — `pd_dataforseo_get_google_organic_results` for 3–5 head keywords from the keyword sheet. Check for AI Overview presence in SERP features. Record which keywords show AI Overviews and whether the client appears in them.

---

## Step 2 — Read Input Data

**From keyword research sheet (Google Sheets API):**
- All page → keyword assignments
- Primary/secondary keywords per page
- Search volumes and difficulty scores
- Services × locations matrix (if in separate tab)

**From content register (Google Sheets API):**
- Published pages list
- Page types (service, location, blog, other)
- Any content gaps identified

**From client KB:**
- Confirmed services and locations
- Competitors (for Section 5)
- Brand voice and tone rules (for content angle decisions)
- Business goals (for Section 1 vision)

---

## Step 2.2 — Score Existing Content Quality

Before gap analysis, score every existing page on both axes and produce a verdict per page. See `references/content-quality-evaluation.md` for the full model.

- **Axis 1 — Content Quality (0–16):** 8 factors from the content register scrape (word count, keyword targeting, headings, meta title, meta description, internal links, freshness, CTAs). Schema is not scored.
- **Axis 2 — SEO Performance (0–6):** organic traffic, keyword rankings, referring domains. At onboarding GSC access usually isn't live — use DataForSEO estimates from Step 1 and label them as estimates.
- **Verdict:** cross the two bands → Keep / Monitor / Rewrite / Replace. Apply the override rules (never Replace a page with backlinks or under 6 months old; never Replace a core page).

Write the results to a new **"Content Quality"** tab on the client's existing content register sheet.

Rewrite/Replace/Consolidate verdicts become the quality gaps consumed by Step 2.5. Monitor verdicts go to Section 6 or keyword sheet review, not the content plan.

---

## Step 2.5 — Run Content Gap Analysis

Cross-reference the content register, keyword research, services × locations matrix, and competitor data to identify what's missing or underperforming. See `references/content-gap-analysis.md` for the full methodology.

**Four gap types (in order):**
1. **Matrix gaps** — services × locations from KB vs content register. Any combination without a page = structural gap.
2. **Quality gaps** — taken directly from the Step 2.2 verdicts (Rewrite / Replace / Consolidate). Do not re-derive.
3. **Competitor keyword gaps** — keywords competitors rank for that the client doesn't target. Up to 5 competitors (KB-named first, then DataForSEO discovery filtered to service businesses only — no ecomm, directories, manufacturers).
4. **Intent gaps** — service clusters missing supporting content (blogs, FAQs) for informational queries.

**Prioritize** by: search demand → business relevance → location priority → competitive difficulty.

The output is a prioritized gap list that feeds directly into Section 4 (content plan). The PM never sees the raw gap analysis — they see the content plan.

---

## Step 3 — Populate Strategy Doc

Use the template from `references/strategy-doc-template.md`. Populate each section:

### Section 1: 12-Month Vision
- Derive 3–5 measurable outcomes from KB goals + audit baselines
- Use specific numbers: "Grow page-one rankings from X to Y"
- If KB has no explicit goals, flag for PM and use audit-derived targets

### Section 2: Current State
- **SEO Snapshot table** — from DataForSEO audit data (Step 1)
- **AI/LLM Visibility Baseline** — from SERP feature checks. If no AI Overviews found for target keywords, note: "No AI Overview presence detected for target keywords — baseline established"
- **Competitive Snapshot** — from KB competitors + DataForSEO data. One line per competitor naming their specific advantage

### Section 3: Target Keywords & Locations
- **Priority clusters** — Select 3–5 service clusters for Block 1 based on the gap analysis output (biggest/most actionable gaps). First block defaults to location pages (highest local-intent lever) unless gap data suggests otherwise
- Link to keyword research sheet (don't duplicate the full list)
- Link to services × locations matrix
- **Target Locations** — full confirmed list from KB
- **Excluded** — keywords/locations from the audit that fall outside scope, with reasons
- **Flagged** — items needing PM check (brand confusion, out-of-area ranking, volume anomalies)

### Section 4: Content Plan
- **Source:** gap analysis output (Step 2.5) — matrix gaps, quality gaps, competitor gaps, intent gaps, all prioritized
- Apply content planning methodology from `references/content-planning-methodology.md`
- Determine entry path: TWG build (2-week health check) or non-TWG (4-week audit/fix)
- Apply ramp period — don't start at full 2/week pace
- Build 12-week content table with: week, type (service/location/blog), page/topic, target keyword, location — items come from the prioritized gap list, sequenced by priority score
- Build separate rewrites table from quality gaps that passed the rewrite decision tree — existing pages with traffic/rankings/links that need improvement
- Rewrites don't count against 2/week new content rate

### Section 5: Competitive Positioning
- Named competitors from KB ONLY (not DataForSEO overlap)
- Cross-reference with audit data for their actual SERP advantage
- If no competitors in KB, flag for PM — do not auto-discover

### Section 6: Technical Priorities
- From on-page audit, ranked: Critical → Warning → Info
- Each row: severity, issue, impact (plain English), action
- These run in parallel with content — not separate calendar slots

### Section 7: Goals for This Block
- 2–3 measurable targets for the 3-month block
- Tied to the priority clusters chosen in Section 3
- Not the 12-month vision restated smaller

---

## Step 4 — Create ClickUp Page

Find the client's Project Hub doc in ClickUp DELIVERY space (`90182597483`).

```
GET /api/v3/workspaces/308435/docs?parent_id={folder_id}&parent_type=5
```

Find the Hub page, then create the strategy page as a subpage. Each block gets its own page — previous blocks stay as read-only history.

```
POST /api/v3/workspaces/308435/docs/{doc_id}/pages
{
  "name": "SEO Strategy — Block 1 (Oct–Dec 2026)",
  "sub_title": "Block 1 — [Service Cluster] | Created [Date]",
  "content": "{populated_template}",
  "content_format": "text/md",
  "parent_page_id": "{hub_page_id}"
}
```

Page naming convention: `SEO Strategy — Block {N} ({Mon}–{Mon} {YYYY})`

This creates a draft requiring approval.

---

## Step 5 — Post for PM Review

Send Slack message to the PM with:
- Summary: "Strategy doc drafted for [CLIENT] — Block 1 focused on [cluster]"
- What to review: cluster choice, content plan sequence, block goals, excluded/flagged items
- Link to the ClickUp draft
- Note: "Approve and I'll publish, create STATE.md, update roadmap, and start scheduling content tasks"

---

## Step 6 — On Approval

1. **Publish** the ClickUp page draft
2. **Create STATE.md** at `skills/clients/{shortcode}/seo/STATE.md` — see `references/state-md-template.md`
3. **Update roadmap/focus** — call `clickup-roadmap-focus` with:
   - Roadmap: "SEO program launched — Block 1: [cluster]" entry
   - Current Focus: add SEO priorities, milestones, KPIs
4. **Trigger content scheduler** (future skill) — create ClickUp tasks for weeks 1–4 of the content plan
