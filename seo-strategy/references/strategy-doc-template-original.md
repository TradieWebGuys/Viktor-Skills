# SEO Strategy Document — Template & Methodology

Output format: ClickUp doc, saved to Client Folder > Project Hub Docs > "SEO Strategy [date]". A ClickUp task is created in the client's shortcode SEO task list, assigned to user 48626346, linking to the doc. After the strategy doc is created, run skill `clickup-roadmap-focus` to sync the roadmap doc.

Every section below is sourced from two places only: the DataForSEO audit and the client's shortcode knowledge base (growth direction, target areas, competitors, promotions, channel priorities). Nothing in this doc should be invented — if a section has no supporting data from either source, say so rather than filling it in.

---

## 1. 12-Month Vision (top section)

Start from the client's stated 6–12 month goals in the KB. Sharpen them with specific, measurable targets rather than repeating the goal as written — pull the numbers from the audit's current baseline and its own longer-range roadmap targets where relevant (e.g. keyword count, page-one count, referring domains).

Format: 3–5 bullet points, each a specific outcome with a number attached, not a restated aspiration.

## 2. Current State

The baseline everything else in the doc is measured against. Structure as labelled subsections, not one paragraph — this is the section a PM or client will scan first, so it needs to be scannable:

**SEO Snapshot** — keywords ranking, page-one rankings, estimated traffic, traffic value, technical score, and the single biggest headline finding from the audit ("the bottom line"), stated as one sentence.

**AI/LLM Visibility Baseline** — current AI search citation/appearance status, where that data is available (e.g. via SE Ranking's AI ranking tracking). This is a starting-point number, not a target — it exists so movement can be measured against it later. If no AI ranking data was pulled for this audit, say so explicitly rather than omitting the subsection — an absent baseline is itself worth flagging.

**Competitive Snapshot** — one line per named competitor (from the KB, not DataForSEO's overlap list) on where they currently lead.

## 3. Target Keywords & Locations

The full inventory — every keyword and location in scope, not a curated example set. This section is the complete list; prioritisation and sequencing happen in the content plan section that follows it.

- **Target keywords** — every keyword from the audit's ranking/opportunity data that ties to a service the KB lists as "grow," in full, with position and volume
- **Target locations** — every suburb/region from the KB's target-area list, in full, regardless of whether a page exists yet

**Excluded** — keywords or locations the audit surfaces but that fall outside the KB's target-area list, travel radius, or growth-service list, even where volume looks attractive. State why each is excluded.

**Flagged** — anything that needs a manual check before being trusted as a real target: brand-name confusion, existing pages ranking for out-of-area suburbs built under an earlier scope, or volume that looks out of line with the rest of the set. Flagged items don't go into the content plan until resolved.

## 4. Content Plan (this block)

Turns the target inventory above into the actual 3-month block: a specific topic per week, tied to one keyword and one location, not a broad monthly theme. Kept directly under Target Keywords & Locations since the two are read together — sequencing decisions only make sense against the full target list.

Follows the content planning methodology: cadence and mix per that framework, rewrites tracked separately from new-content output, rewrite priority given to any target page with existing traffic, rankings, or backlinks.

Table format:

| Week | Type | Page/Topic | Target Keyword | Location |
|---|---|---|---|---|

Cross-check the audit's own suggested page list against the KB's target areas before locking this table — the audit doesn't know the client's current growth priorities, so its generic recommendations need filtering the same way the keyword list above does.

## 5. Competitive Positioning

Named competitors come from the KB first — client-named, Amanda's notes, onboarding form — not DataForSEO's keyword-overlap list, which includes aggregators and irrelevant overlap. Cross-reference the audit's competitive landscape table only for competitors the KB already named. One line per competitor: their advantage, and the angle that counters it.

## 6. Technical Priorities

Pull directly from the audit's Issues to Fix / Priority Actions, ranked by the audit's own severity tags (Critical/Warning/Info). These run in parallel with content production, not as separate calendar slots.

## 7. Goals for This Block

2–3 measurable targets for the block specifically, tied to the KB's "service to push right now" and channel priorities — not the 12-month vision restated.

## Sources

Log the audit date and the KB's "last synced" date at the bottom of the doc, so anyone reading it later knows how current the inputs were.
