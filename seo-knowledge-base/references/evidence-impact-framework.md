# Evidence Hierarchy & Impact Framework

Two independent classifications applied to every SEO finding and recommendation.

- **Evidence level** answers: *how do we know this?*
- **Impact** answers: *how much does it matter to this client?*

They are independent. A Level 1 (Google-documented) finding can be Low impact. A Level 3 (convention) finding can be High impact. Never collapse them into one "priority" number.

## Evidence Hierarchy

| Level | Definition | Example |
|---|---|---|
| **L1** | Explicitly documented by Google or another relevant search engine | Core Web Vitals as a ranking signal — Google Search Central documentation |
| **L2** | Supported by repeatable industry research or testing | Title tag correlation studies — study linked, methodology described |
| **L3** | Widely accepted implementation convention | Descriptive anchor text on internal links — universally recommended, not a documented Google rule |
| **L4** | Reasonable hypothesis requiring testing | Responding to GBP reviews may improve local rankings — plausible, unconfirmed |
| **L5** | Personal, stylistic, or tool-specific preference | Title case headings. "Fix everything Screaming Frog flags." |

**Hard rule:** L3, L4, and L5 recommendations are NEVER described as Google requirements. Use "generally considered helpful", "our convention", or "worth testing" — not "Google requires".

## Impact Framework

| Impact | Definition | Examples |
|---|---|---|
| **Critical** | Likely to prevent crawling, indexing, or normal site operation | Robots.txt blocking key pages; site-wide noindex; broken SSL; 5xx on key pages |
| **High** | Strong potential to materially affect organic visibility or lead generation | Missing/duplicate titles on key service pages; no mobile responsiveness; no GBP listing; no indexable content on critical pages |
| **Medium** | Worthwhile improvement with a plausible but limited effect | Missing meta descriptions; heading hierarchy issues; alt text gaps; CWV in "Needs Improvement"; incomplete LocalBusiness schema |
| **Low** | Minor optimisation or preventative maintenance | URL structure cleanup; minor redirect chains; optional schema properties; anchor text specificity |
| **Informational** | Preference, observation, or optional enhancement | Heading capitalisation; FAQ schema markup (post-May 2026); SEO tool score improvements; cosmetic formatting |

**Hard rule:** an issue is not High or Critical merely because a tool flagged it that way. Tool severity is L5 evidence. Reclassify every tool finding against this table before it reaches a report.

## How to display them

### Internal output — tags visible

Internal audits, ClickUp report tasks, strategy doc technical priorities, and content briefs show both tags inline:

```
Missing meta descriptions on 14 service pages  [Impact: Medium] [Evidence: L1]
Heading capitalisation inconsistent  [Impact: Informational] [Evidence: L5]
```

Findings are **sorted by impact**, Critical first. Never sorted by tool severity or by the order the tool returned them.

### Client-facing output — tags hidden

Client PDFs and client emails do NOT show `L1`–`L5` or the word "evidence". Clients don't need our epistemics; they need to know what to fix first.

Translate instead:

| Internal | Client-facing |
|---|---|
| `[Impact: Critical]` | "Fix immediately" |
| `[Impact: High]` | "High priority" |
| `[Impact: Medium]` | "Recommended" |
| `[Impact: Low]` | "Nice to have" |
| `[Impact: Informational]` | Usually omitted entirely from client reports |

Evidence level shapes the **language** used, not a visible label:

| Level | Client-facing phrasing |
|---|---|
| L1 | "Google requires…" / "Google documents this as…" |
| L2 | "Industry research shows…" |
| L3 | "Best practice is…" |
| L4 | "We'd like to test whether…" |
| L5 | "Our preference is…" — or leave it out |

Informational + L5 findings are generally cut from client reports altogether. Padding a report with cosmetic issues to make it look thorough is how clients lose trust in the priorities that matter.

## Applying it per skill

| Skill | Application |
|---|---|
| `dataforseo_audit` | Every finding tagged. Sorted by impact. Prospect-facing version uses the translated labels. Reclassify DataForSEO's own severity scores. |
| `seo-monthly-report` | Internal ClickUp report tags everything; traffic lights map to impact (red = Critical/High, amber = Medium, green = resolved). Client PDF uses translated labels only. |
| `seo-strategy` | Section 6 (Technical Priorities) ordered by impact with tags. Section 4 content plan doesn't need tags — it's a schedule, not findings. |
| `content-quality-evaluation` | Each of the 8 content factors carries a fixed impact rating (see below). Used to decide which weak factors are worth flagging in a rewrite brief. |
| Writing skills | Internal guidance only. If a brief or copy makes an SEO claim, it must be L1 or L2, otherwise phrase it as convention. Never surface tags in published copy. |

## Fixed ratings for content quality factors

Used by `seo-strategy/references/content-quality-evaluation.md` so a rewrite brief leads with what actually matters.

| Factor | Impact | Evidence |
|---|---|---|
| Meta title missing/duplicate | High | L1 |
| No indexable content / very thin (<300w) | High | L1 |
| Heading structure (missing or multiple H1) | Medium | L1 |
| Keyword targeting in title/H1 | Medium | L2 |
| Internal linking | Medium | L3 |
| Meta description missing | Medium | L1 |
| CTA placement | Medium | L5 (conversion convention, not SEO) |
| Content freshness on evergreen pages | Low | L4 |
| Word count above the minimum | Low | L5 (internal guideline, not a Google rule) |
| Service / FAQPage / BreadcrumbList schema | Informational | L1 (documented as producing no rich result for these clients) |

Note that CTA placement and word count are **not SEO factors** — they're TWG quality standards. They belong in the score, but must never be reported to a client as an SEO fix.

## Uncertainty

When evidence is mixed or absent, say so. Do not invent a definitive rule. See section 7 of `seo-rules-reference.md` for the current list of genuinely uncertain areas (CTR as a ranking signal, backlink weighting, AI search citation behaviour, GBP ranking factors, freshness on evergreen pages, heading keyword weight).

Standard phrasing: *"This isn't confirmed by Google. What would tell us more is [specific data source]."*
