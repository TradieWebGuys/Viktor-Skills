# Content Quality Evaluation

Scores every existing page on a client's site during onboarding (and re-scores at quarterly review) to decide: **Keep, Monitor, Rewrite, or Replace**.

Runs after the content register crawl, before content gap analysis. Its output feeds Gap Type 2 (quality gaps) in `content-gap-analysis.md`.

## Why two axes

Scoring on-page content alone produces wrong verdicts. A thin page ranking position 8 for a commercial keyword has real equity and must not be replaced. A well-written page with zero traffic isn't a rewrite candidate — it's an investigation.

So every page gets two independent scores:

- **Axis 1 — Content Quality** (max 16): how good the page is as a piece of content. Sourced from the content register scrape.
- **Axis 2 — SEO Performance** (max 6): how the page actually performs in search. Sourced from DataForSEO + GSC.

The verdict comes from crossing them.

## Axis 1 — Content Quality (8 factors, 0–2 each, max 16)

| # | Factor | 0 | 1 | 2 |
|---|---|---|---|---|
| 1 | **Word count** (service/location) | < 300 | 300–799 | 800+ |
| 1 | **Word count** (blog) | < 300 | 300–699 | 700+ |
| 2 | **Keyword targeting** | No identifiable target keyword | Keyword present but not in title/H1 | Target keyword in title, H1, and first 100 words |
| 3 | **Heading structure** | No H1, or multiple H1s | Single H1, fewer than 2 H2s | Single H1, 3+ H2s, logical hierarchy, no skipped levels |
| 4 | **Meta title** | Missing, or duplicate of another page | Present but > 60 chars or no keyword | Present, unique, under 60 chars, contains target keyword |
| 5 | **Meta description** | Missing | Present but > 160 chars or generic | Present, unique, 120–160 chars, includes a benefit or CTA |
| 6 | **Internal linking** | No internal links in body | 1–2 body links | 3+ contextual body links to relevant service/location pages |
| 7 | **Content freshness** | No date, or last modified 24+ months ago | Modified 12–24 months ago | Modified within 12 months |
| 8 | **CTA presence** | No CTA | 1–2 CTAs | CTAs at all 5 placements (per service page copy standard) |

**Bands:** High 12–16 · Mid 7–11 · Low 0–6

### Schema is deliberately excluded from scoring

Do not score Service, FAQPage, or BreadcrumbList schema. Per the SEO knowledge audit:

- **Service schema** — Google supports no Service rich result. Low impact. Semantic clarity only.
- **FAQPage schema** — since May 2026 no rich results for local businesses. Informational/optional.
- **BreadcrumbList** — no evidence basis in the audit.

**LocalBusiness schema is checked separately** as a site-level technical finding (Medium impact, Evidence L1), not as a per-page content quality factor. Missing or incomplete LocalBusiness schema goes into strategy doc Section 6 (Technical Priorities), not the page verdicts.

Visible FAQ *content* on the page still counts — it contributes to word count and heading structure. The markup does not.

## Axis 2 — SEO Performance (3 factors, 0–2 each, max 6)

| Factor | 0 | 1 | 2 | Source |
|---|---|---|---|---|
| **Organic traffic** | 0 sessions/month | 1–50 sessions | 50+ sessions | GSC (or DataForSEO estimate pre-access) |
| **Keyword rankings** | No keywords in top 50 | 1+ keywords ranking 11–50 | 1+ keywords in top 10 | DataForSEO ranked keywords by URL |
| **Backlinks** | 0 referring domains | 1–5 referring domains | 6+ referring domains | DataForSEO backlinks by URL |

**Bands:** High 4–6 · Mid 2–3 · Low 0–1

At onboarding, GSC access usually isn't available yet — use DataForSEO estimated traffic and note the source. Never present an estimate as measured data.

## Verdict Matrix

| | Content High (12–16) | Content Mid (7–11) | Content Low (0–6) |
|---|---|---|---|
| **SEO High (4–6)** | Keep | **Keep** — ranking despite mid content, leave it alone | **Rewrite** — real equity, improve the content |
| **SEO Mid (2–3)** | Keep | Rewrite | Rewrite |
| **SEO Low (0–1)** | **Monitor** — investigate targeting or give it time | Rewrite if < 6 months live, else Replace | Replace |

### Verdict meanings

- **Keep** — no action. Page stays as-is.
- **Monitor** — content is good but not performing. Check for wrong keyword target, indexation issue, or insufficient age. Goes to Section 6 (technical) or keyword sheet review, not the content plan.
- **Rewrite** — page keeps its URL. Content is rewritten and expanded. Counts against the rewrite allocation in the content plan, tracked separately from new content.
- **Replace** — new page created, old URL 301-redirected. Only when there is no equity to preserve.

### Override rules

1. **Never Replace a page with any backlinks.** If referring domains > 0, downgrade Replace to Rewrite regardless of scores.
2. **Never Replace a page under 6 months old.** It hasn't had time to perform. Downgrade to Rewrite or Monitor.
3. **Consolidate instead** when two or more pages score Mid/Low and target the same keyword × location. Merge into the strongest URL, redirect the rest. Flag as a cannibalisation fix.
4. **Core pages are never Replaced.** Homepage, About, Contact get Rewrite at worst.

## Output

A new **"Content Quality"** tab appended to the client's existing content register Google Sheet — same sheet, so everything about existing content lives in one place.

| Column | Content |
|---|---|
| URL | Page URL |
| Type | From content register classification |
| Content Score | 0–16 |
| Content Band | High / Mid / Low |
| SEO Score | 0–6 |
| SEO Band | High / Mid / Low |
| Verdict | Keep / Monitor / Rewrite / Replace |
| Override Applied | Which override rule fired, if any |
| Weakest Factors | The 2–3 lowest-scoring content factors |
| Data Source | GSC / DataForSEO estimate |
| Notes | Blank for PM |

Per-factor scores are written to the same tab in columns to the right so the score is auditable, not a black box.

## When it runs

| Trigger | Behaviour |
|---|---|
| **Onboarding** | Automatically, as part of the content register step. No separate trigger for the PM to remember. |
| **Quarterly review** | Re-scored with 3 months of real GSC data. Verdicts can change — a Monitor page that started ranking becomes Keep. |
| **Ad hoc** | `@Viktor evaluate content quality for [SHORTCODE]` if a PM wants a fresh pass mid-block. |

The PM does not review the raw quality tab before the strategy doc is drafted. Verdicts flow straight into the content plan, same as gap analysis. The tab exists so the PM can audit a verdict they disagree with.

## Guardrails

- **Don't fabricate performance data.** If DataForSEO returns nothing for a URL, score 0 and record "no data" in Data Source — don't assume it means zero traffic without saying so.
- **Never act on a Replace verdict autonomously.** Replaces mean redirects and lost URLs. Every Replace is listed explicitly in the strategy doc for PM sign-off.
- **Score, don't rewrite, in this step.** Rewriting is the writing skills' job, driven by the content plan.
