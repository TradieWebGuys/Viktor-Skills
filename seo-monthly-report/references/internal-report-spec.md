# Internal Report Specification

The full diagnostic report posted as a ClickUp task description. Contains all data, including negative trends and diagnostics. This is for the internal team only.

## Traffic-Light System

| Indicator | Meaning | When |
|-----------|---------|------|
| 🟢 | On track / improved | Positive change or at/above target |
| 🟡 | Needs attention | Slight decline (under 10%) or approaching threshold |
| 🔴 | Urgent / significant decline | Decline over 10% or below threshold |

## Report Structure

### Header

```
# 📊 SEO Internal Report — {client domain}
**Period:** {start date} to {end date}  |  **Comparison:** {prev start} to {prev end}
**Generated:** {date}  |  **Status:** ⏳ Pending Review
```

### Section 1 — Executive Summary

Full metrics table with traffic-light indicators:

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

Include algorithm update note if applicable:
> ℹ️ Google released an algorithm update during this reporting period. The SEO strategy has been reviewed and adjusted accordingly.

### Section 2 — Search Console Performance

- Top 20 Queries by Clicks (all columns: clicks, impressions, CTR, position)
- Top 15 Pages by Clicks (all columns)
- CTR analysis and position trends

### Section 3 — GA4 Traffic and Conversions

- Traffic by Channel (full table with engagement metrics)
- Channel Comparison vs Previous Period (all changes, including negatives)
- Top Landing Pages (with conversions)
- All Conversion Events

### Section 4 — Keyword Rankings

- All keywords on page 1 with position and search volume
- Keywords moving towards page 1 (positions 11–20, trending up)
- Keywords that dropped off page 1 (internal diagnostic)

### Section 5 — Backlinks Profile

- Total Backlinks, Referring Domains, Dofollow Backlinks
- New/lost backlinks this period
- Spam score assessment
- Toxic backlinks flagged

### Section 6 — Google Business Profile

All metrics with period comparison:
- Call Clicks, Website Clicks, Direction Requests
- Search vs Maps Views, Profile Interactions
- Reviews: total count, average rating, new reviews
- Posts actually published this month (not a target number)

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

List every 🔴 metric with a one-line explanation:
```
🚨 URGENT ITEMS
- GSC Clicks down 36% — investigate potential algorithm impact
- Organic Sessions dropped 25% — review content freshness
```

### Section 10 — Next Month To-Do's

**Must be specific to the client's strategy** — not generic bullets.

Read the client's strategy doc (Section 4 content plan + Section 7 block goals) and STATE.md. List the specific planned deliverables:
- Which pages will be written or rewritten
- Which technical fixes are scheduled
- Which GBP activities are planned
- Any block milestones approaching

### Section 11 — Proposed Client-Facing Report

**Mandatory.** Contains the exact content proposed for the client PDF, populated with real data and positive framing.

```markdown
---

## 📄 Proposed Client-Facing Report

> ⚠️ REVIEW REQUIRED — The content below is what @Viktor proposes to send to the client.
> Edit directly in this description, then tick the approval checklist when ready.

{Full client-facing report content here — all sections from client-report-spec.md, populated with real data}

---
```

**Rules for Section 11:**
- Populate every section with real data. No placeholders.
- Positive framing: only show comparisons when positive. Show current values without comparison for declines.
- No 🟢🟡🔴 indicators.
- No CTR, position by query, spam score, toxic backlinks.
- Include CTA: "Questions about this report? Reply to this email, or contact us at Support@TradieWebGuys.com.au"
- Include algorithm update note if applicable.

## Formatting Rules

- Use standard markdown pipe tables. ClickUp renders them via `markdownDescription`.
- Bold any metrics that changed more than 20% in either direction.
- Analytical, direct tone for Sections 1–10.
- Professional, positive, approachable tone for Section 11.
- Australian English spelling throughout.
