# Quarterly Review Flow

Triggered by PM: `@Viktor run the quarterly review for [SHORTCODE]`

The monthly report cron detects when it's the final month of a block (reads STATE.md for `block_start_date`, calculates 3-month window) and posts a Slack flag:

> "Block [N] ending for [CLIENT] — quarterly strategy review due. Say the word and I'll draft the next block."

PM triggers when ready — they may want to hold for a client meeting first.

---

## Step 0 — Read Current State

1. **STATE.md** — `skills/clients/{shortcode}/seo/STATE.md`
   - Current block number, cluster, date range
   - Links to all artifacts
   - Last 3 months of metric snapshots
   - Block goals and progress

2. **Current strategy doc** — read from ClickUp (page ID in STATE.md)
   - Section 7 goals — which were met?
   - Section 4 content plan — what was published vs planned?
   - Section 3 clusters — did the prioritised keywords move?

3. **Last 3 monthly reports** — read from wherever they're stored (ClickUp, Drive, or STATE.md links)
   - MoM trends: traffic, rankings, conversions
   - Flags raised during the block
   - Content published vs planned each month

4. **Client KB** — check for any updates to services, locations, competitors since last block

---

## Step 1 — Run Fresh Audit (All Sources)

Unlike the first strategy (which is pre-access and DataForSEO-only), the quarterly review has full access to all data sources.

**DataForSEO:** Same crawl, keywords, backlinks, and AIO/LLM checks as the first strategy.

**Google Search Console:** Organic clicks, impressions, CTR, position by query and page for the full block period. Shows actual search performance, not just estimated rankings.

**Google Analytics 4:** Sessions by channel, top landing pages, conversion events. Shows real traffic and conversions driven by SEO work.

**Google Business Profile:** Calls, clicks, directions, reviews, posts published. Shows local visibility outcomes.

Compare against the block-start baselines in STATE.md to measure movement:
- Keywords gained/lost page-one rankings (DataForSEO)
- Organic traffic change — absolute and % (GSC + GA4)
- Conversion events — calls, emails, forms (GA4)
- Technical health score change (DataForSEO)
- New/lost referring domains (DataForSEO)
- GBP engagement trends — calls, clicks, directions (GBP)
- AIO/LLM visibility changes — new AI Overview appearances? (DataForSEO)

---

## Step 2 — Block Assessment

Evaluate the completed block:

### Goals Assessment
For each Section 7 goal from the current strategy doc:
- **Met** — what evidence? (ranking position, traffic number, pages published)
- **Partially met** — what's left? Should it carry into the next block?
- **Not met** — why? (content not published, keyword didn't move, external factor)

### Content Plan Assessment
- Planned vs actual: how many of the 12-week plan items were published?
- Rewrites completed vs planned
- Any content that performed unexpectedly well or poorly
- GBP posting consistency

### Competitive Movement
- Did competitors gain or lose ground?
- Any new competitors appearing for target keywords?

---

## Step 2.5 — Re-Run Content Gap Analysis

Re-run the full gap analysis (see `references/content-gap-analysis.md`) with updated data:

1. **Matrix gaps** — check against updated content register (pages published during the block should have closed some gaps)
2. **Quality gaps** — re-run the content quality evaluation (`references/content-quality-evaluation.md`) with 3 months of real GSC data on Axis 2. Verdicts can change between blocks: a Monitor page that started ranking becomes Keep; a Keep page that decayed becomes Rewrite. Update the Content Quality tab in place.
3. **Competitor keyword gaps** — fresh `get_domain_intersection` against the same 5 competitors. New opportunities may have emerged.
4. **Intent gaps** — check which service clusters now have supporting content and which still don't

The quarterly re-run is more data-rich than onboarding because GSC, GA4, and GBP data are available. Pages ranking below page 3 after 3+ months of being live are stronger rewrite candidates than at onboarding.

Prioritize the updated gap list → feeds into Section 4 of the next block.

---

## Step 3 — Draft Next Block

### Choose next cluster
Inputs for cluster selection:
1. **Updated gap analysis** — which gaps are biggest and most actionable now?
2. Keyword sheet — which service clusters haven't been covered yet?
3. Block assessment — any partially-met goals that need continued focus?
4. Seasonal timing — does the next 3-month window align with a service's peak season?
5. Client KB — any new services or priorities from recent meetings?
6. Content planning methodology — first block defaults to location pages, subsequent blocks use data

### Update strategy doc sections

Only these sections get rewritten. Sections 1 and 5 are reviewed but typically unchanged:

| Section | Action |
|---|---|
| 1. 12-Month Vision | Review — adjust only if goals were met or client direction changed |
| 2. Current State | Rewrite — fresh audit data replaces old baselines |
| 3. Target Keywords | Rewrite — new priority clusters for this block, updated excluded/flagged |
| 4. Content Plan | Rewrite — new 12-week table for the new cluster |
| 5. Competitive Positioning | Review — update if competitive landscape shifted |
| 6. Technical Priorities | Update — remove resolved issues, add newly found ones |
| 7. Goals for This Block | Rewrite — new block-specific targets |

Update the doc subtitle: `"Block [N] — [Service Cluster] | Updated [Date]"`

---

## Step 4 — Create New Block Page in ClickUp

Each block gets its own page — previous blocks stay as read-only history. Create a new sibling page under the same Hub parent, not a PUT to the existing page.

```
POST /api/v3/workspaces/308435/docs/{doc_id}/pages
{
  "name": "SEO Strategy — Block [N] ([Mon]–[Mon] [YYYY])",
  "sub_title": "Block [N] — [Service Cluster] | Created [Date]",
  "content": "{populated_template}",
  "content_format": "text/md",
  "parent_page_id": "{hub_page_id}"
}
```

Page naming convention: `SEO Strategy — Block {N} ({Mon}–{Mon} {YYYY})`

The previous block's page stays untouched — PM and team can compare blocks side by side at any time.

---

## Step 5 — Post for PM Review

Slack message with:
- **Block [N-1] summary:** goals met/missed, content published count, key wins
- **Block [N] proposal:** chosen cluster, why now, 12-week content plan overview
- **Changes to review:** anything in Excluded/Flagged that changed, cluster choice rationale
- Link to ClickUp draft

---

## Step 6 — On Approval

1. **Publish** ClickUp page draft
2. **Update STATE.md:**
   - Increment block number
   - Set new `block_start_date`
   - Archive previous block's metrics as history
   - Update strategy doc link to point to the new block's page
   - Move previous block page ID to `Strategy Doc History`
3. **Update roadmap/focus** (block boundary → conditional trigger fires):
   - Roadmap: "Block [N-1] complete — [outcomes]. Block [N] started — [cluster]"
   - Current Focus: update SEO priorities and milestones for new block
4. **Trigger content scheduler** — create ClickUp tasks for weeks 1–4 of new content plan
