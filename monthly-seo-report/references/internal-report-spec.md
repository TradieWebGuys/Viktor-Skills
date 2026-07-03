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

## Formatting

- Use markdown tables for all data.
- Use emoji indicators consistently.
- Bold any metrics that changed more than 20% in either direction.
- Keep the tone analytical and direct — this is for the internal team.
