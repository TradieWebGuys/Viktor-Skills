# Content Gap Analysis

Cross-references what the site has (content register) against what it should have (keyword research + services × locations matrix + competitor data) to produce a prioritized gap list. Feeds directly into the content plan — the PM never sees this as a separate output.

Runs as part of the strategy skill, between reading input data and populating the content plan.

---

## When It Runs

- **First strategy (onboarding):** After content register + keyword research are done, before populating Section 4.
- **Quarterly review:** Re-run against updated competitor data and 3 months of GSC/GA performance. Feeds the next block's content plan.
- **Monthly (lightweight):** Monthly reports surface new keyword opportunities and decay signals. These aren't a full gap analysis but flag items for the quarterly re-run.

---

## Four Gap Types (checked in order)

### 1. Matrix Gaps (structural)

Compare the services × locations matrix from the KB against the content register.

- Every confirmed service should have a service page
- Every confirmed location should have a location page (or location variant of the relevant service)
- Any service × location combination without a page = a gap

This is mechanical — no judgment needed. Output: a table of missing pages with the target keyword from the keyword sheet.

### 2. Quality Gaps (existing content that's failing)

**This gap type is produced by the content quality evaluation — see `content-quality-evaluation.md`.** Do not re-derive it here.

Every existing page is scored on two axes (Content Quality 0–16 from the register scrape, SEO Performance 0–6 from DataForSEO/GSC) and crossed to produce a verdict: **Keep, Monitor, Rewrite, or Replace**.

For gap analysis purposes:
- **Rewrite** and **Replace** verdicts become quality gaps that feed the content plan
- **Consolidate** flags (multiple Mid/Low pages on the same keyword × location) become cannibalisation fixes
- **Monitor** verdicts do NOT enter the content plan — they go to Section 6 (technical) or keyword sheet review
- **Keep** verdicts are excluded entirely

Note: a Mid-content page with High SEO performance is a **Keep**, not a rewrite. Pages that rank get left alone even when the content isn't perfect.

Output: a rewrite/replace/consolidate list, separate from new content, with the weakest factors per page so the writing brief knows what to fix.

### 3. Competitor Keyword Gaps

Use DataForSEO to find keywords competitors rank for that the client doesn't target.

**Competitor selection (5 max):**
1. Start with competitors named in the client KB (typically 2–3)
2. Use `pd_dataforseo_get_competitor_domains` to find additional ranking competitors
3. **Filter out non-service businesses:**
   - Ecomm/supplier sites (selling products, not providing service)
   - Directories (Hipages, ServiceSeeking, Airtasker)
   - Marketplaces (Amazon, Bunnings, eBay)
   - Review/comparison platforms (ProductReview, SolarQuotes, Canstar Blue)
   - Manufacturer sites (Rheem, Daikin, Rinnai)
   - Only keep businesses that offer the **same service** (installation, repair, maintenance) in the same area
4. Fill to 5 total, prioritizing by keyword overlap relevance
5. If the KB already has 5+ named competitors, use those and skip discovery

**Analysis per competitor:**
- `pd_dataforseo_get_domain_intersection` — keywords they rank for that the client doesn't
- Filter results to commercial/transactional intent (skip blog-only informational rankings unless supporting content is needed)
- Group by service cluster

Output: opportunity keywords grouped by service cluster, with volume and difficulty.

### 4. Intent Gaps (topical depth)

For each priority service cluster, check whether the site has:

| Intent | Content type | Example |
|---|---|---|
| Transactional | Service page | "hot water system installation brisbane" |
| Local transactional | Location page variants | "hot water system installation ascot" |
| Informational | Supporting blog | "how to choose a hot water system", "signs your hot water system needs replacing" |
| FAQ | FAQ schema on service page | "how much does a hot water system cost", "how long does installation take" |

If a service cluster has the service page but no supporting content, that's an intent gap. These feed the blog portion of the content plan.

---

## Prioritization

Each gap gets scored on four factors (in order of weight):

1. **Search demand** — from keyword data (volume + intent match)
2. **Business relevance** — primary service from KB vs secondary/ancillary
3. **Location priority** — High/Medium/Low from the service confirmation suburb expansion
4. **Competitive difficulty** — from KD scores (lower = faster win for newer sites)

**Scoring output per gap:**

| Gap | Type | Action | Target Keyword | Volume | KD | Location Priority | Business Relevance | Suggested Block |
|---|---|---|---|---|---|---|---|---|

High-demand + low-difficulty + primary-service + high-priority-location gaps go into the first block. Everything else is sequenced into later blocks.

---

## Output

Not a separate deliverable. The gap list feeds directly into:

- **Strategy doc Section 3** — priority clusters chosen based on where the biggest/most actionable gaps are
- **Strategy doc Section 4** — content plan populated from the gap list, sequenced by the content planning methodology (velocity, ramp, blocks, new-vs-rewrite)
- **Strategy doc Section 7** — block goals tied to closing the most impactful gaps

The PM reviews the content plan (the output of gaps + sequencing), not the raw gap analysis.
