# Internal Report Specification

The internal report is the full diagnostic version posted as a ClickUp task description. It contains all data, including negative trends and detailed diagnostics.

## Traffic-light system

Apply these indicators to every metric that has a comparison value:

| Indicator | Meaning | When to use |
|-----------|---------|-------------|
| 🟢 | On track / improved | Positive change or at/above target |
| 🟡 | Needs attention | Slight decline (under 10%) or approaching threshold |
| 🔴 | Urgent / significant decline | Decline over 10% or below acceptable threshold |

## Report structure

### Header

```
# 📊 SEO Internal Report — {client domain}
**Period:** {start date} to {end date}  |  **Comparison:** {prev start} to {prev end}
**Generated:** {date}
**Status:** ⏳ Pending Review
```

### Section 1 — Executive Summary

Full metrics table with traffic-light indicators and period-over-period change:

| Metric | This Period | Previous | Change | Status |
|--------|------------|----------|--------|--------|
| GSC Clicks | {value} | {value} | {%} | 🟢/🟡/🔴 |
| GSC Impressions | {value} | {value} | {%} | 🟢/🟡/🔴 |
| GSC Avg Position | {value} | {value} | {%} | 🟢/🟡/🔴 |
| Organic Sessions (GA4) | {value} | {value} | {%} | 🟢/🟡/🔴 |
| Total Sessions (GA4) | {value} | {value} | {%} | 🟢/🟡/🔴 |
| Total Keywords Ranked | {value} | {value} | {%} | 🟢/🟡/🔴 |
| Page 1 Keywords | {value} | {value} | {%} | 🟢/🟡/🔴 |
| Est. Traffic Value | {value} | {value} | {%} | 🟢/🟡/🔴 |
| GBP Rating | {value} ({n} reviews) | — | — | 🟢/🟡/🔴 |
| Website Audit Score | {value}% | {value}% | {%} | 🟢/🟡/🔴 |

### Section 2 — Search Console Performance

Full detail including CTR, impressions, and position for internal analysis.

- Top 15 Queries by Clicks (all columns)
- Top 10 Pages by Clicks (all columns)
- CTR analysis and position trends

### Section 3 — GA4 Traffic and Conversions

- Traffic by Channel (full table with engagement metrics)
- Channel Comparison vs Previous Period (show all changes, including negatives)
- Top Landing Pages (with conversions)
- All Conversion Events

### Section 4 — Keyword Rankings

- All keywords on page 1 with position and search volume
- Keywords moving towards page 1 (positions 11–20, trending up)
- Keywords that dropped off page 1 (internal diagnostic)
- Competitor comparison (if SE Ranking data available)

### Section 5 — Backlinks Profile

Full detail:
- Total Backlinks
- Referring Domains
- Dofollow Backlinks
- New/lost backlinks this period
- Spam score assessment
- Toxic backlinks flagged

### Section 6 — Google Business Profile

All metrics with period comparison:
- Call Clicks, Website Clicks, Direction Requests
- Search vs Maps Views
- Profile Interactions
- Reviews: total count, average rating, new reviews this period
- Posts published this period

### Section 7 — AI/LLM Visibility

- Brand mentions found
- AI Overview appearances
- LLM visibility across platforms
- Exact queries where the business appears

### Section 8 — Website Audit

- Overall audit score and target (90%+)
- Critical issues list
- Improvement recommendations

### Section 9 — Urgent Items

If any metric is flagged 🔴, list it here with a one-line explanation:

```
🚨 URGENT ITEMS
- GSC Clicks down 36% — investigate potential algorithm impact
- Organic Sessions dropped 25% — review content freshness
```

### Section 10 — Next Month Recommendations

5 key areas of focus for the following period, aligned with the client's SEO strategy in ClickUp.

## Algorithm update note

If a significant Google Search algorithm update was released during the reporting period, add this note in the executive summary:

> ℹ️ Google released an algorithm update during this reporting period. The SEO strategy has been reviewed and adjusted accordingly.

### Section 11 — Proposed Client-Facing Report

This section is **mandatory** at the end of every internal report. It contains the exact content Viktor proposes to put into the client-facing PDF — already populated with real data from the current reporting period, with positive framing applied.

**Purpose:** The team reviews this section directly in the ClickUp task description. They can edit wording, add commentary, remove sections, or restructure content before approving. Viktor then reads the approved text back from ClickUp (picking up all edits) and generates the PDF once, with no revisions needed.

**What to include:**

Reproduce the complete client-facing report content in markdown, following all sections from `client-report-spec.md`:

1. Executive Summary table (positive comparisons only)
2. Search Console — Top Pages by Clicks (URL + Clicks only)
3. GA4 — Channel breakdown + Top Landing Pages (traffic only, positive comparisons only)
4. Conversion Events — phone calls, email clicks, form submissions only
5. Keywords Ranking — page 1 keywords, top 10 moving towards page 1, search volumes
6. Backlinks Profile — Total, Referring Domains, Dofollow only
7. GBP — calls, clicks, directions, views, reviews, posts, published pages
8. AI/LLM Visibility — mentions, AI Overview appearances, LLM visibility
9. Website Audit Score — overall score
10. Next Month To-Do's — 5 key focus areas

**Rules:**
- Populate every section with real data from this reporting period — no placeholders.
- Apply the positive-framing rule: only show period comparisons when the change is positive. Show current values without comparison for declines.
- Do NOT include traffic-light indicators (🟢🟡🔴) — those are internal only.
- Do NOT include CTR, position by query, spam score, toxic backlinks, or any internal-only metrics.
- Include the CTA: "Questions about this report? Reply to this email, or contact us at Support@TradieWebGuys.com.au"
- Include the algorithm update note if applicable.

**Formatting:**

```
---

## 📄 Proposed Client-Facing Report

> ⚠️ REVIEW REQUIRED — The content below is what Viktor proposes to send to the client.
> Edit directly in this description, then tick the approval checklist when ready.

{Full client-facing report content here, populated with real data}

---
```

## Formatting

- Use standard markdown tables for all data (pipe tables with `| --- |` separator rows).
- Use emoji indicators consistently.
- Bold any metrics that changed more than 20% in either direction.
- Keep the tone analytical and direct — this is for the internal team.
- Section 11 (Proposed Client-Facing Report) uses client-facing tone — professional, positive, approachable.

## ClickUp API — Critical Table Formatting Rule

**MUST use `markdownDescription` parameter** (not `description`) when creating or updating tasks via the ClickUp API. Pass standard markdown pipe tables — ClickUp automatically converts them to rendered `[table-embed:]` format.

**NEVER pass raw `[table-embed:...]` text** as input — ClickUp stores it as literal unrendered text.

```python
# ✅ CORRECT — standard markdown via markdownDescription
pd_clickup_create_task(
    ...,
    markdownDescription="| Col1 | Col2 |\n| --- | --- |\n| A | B |"
)

# ❌ WRONG — [table-embed:] as input (renders as raw text)
pd_clickup_create_task(
    ...,
    description="[table-embed:1:1 Col1 | 1:2 Col2 | 2:1 A | 2:2 B]"
)

# ❌ WRONG — plain description parameter (no markdown rendering)
pd_clickup_create_task(
    ...,
    description="| Col1 | Col2 |\n| --- | --- |\n| A | B |"
)
```
