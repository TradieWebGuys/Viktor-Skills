# Client-Facing Report Specification

The client-facing report is a TWG-branded PDF. It presents a positive, easy-to-understand summary focused on wins, improvements, and opportunities. No red indicators, no negative trend callouts, no large decline graphs.

## Core principle

Only compare with the previous period when there is a positive improvement. If a metric declined, show the current value without a comparison. Never highlight declines in client-facing reports.

## Report sections (in order)

### 1. Executive Summary

A summary table of key metrics. Show current values. Only show period comparison when the change is positive.

**Include:**
- GSC Clicks
- GSC Impressions
- Organic Sessions (GA4)
- Total Sessions (GA4)
- Total Keywords Ranked
- Page 1 Keywords
- Estimated Traffic Value
- Google Rating and Total Reviews

**Exclude:**
- GSC Average Position (keyword rankings are shown separately later)

### 2. Search Console Performance

**Include:**
- Top Pages by Clicks

**Columns to display:**
- URL
- Clicks

**Do NOT display:**
- CTR
- Impressions
- Position

Keep it simple — the client sees which pages are getting the most search traffic.

### 3. Google Analytics 4 — All Channels

Present GA4 data visually:
- Traffic trend graphs (if possible in PDF format)
- Channel breakdown table
- Top Performing Pages (sessions/traffic only)

**Rules:**
- Only compare with the previous period when there is a positive improvement.
- Top Landing Pages: show traffic only. Do NOT show conversions in this section.
- Keep the layout clean and visual.

### 4. Conversion Events

**Only show key events:**
- Phone call clicks
- Email clicks
- Form submissions

Do not show generic events (page_view, scroll, session_start, etc.).

### 5. Keywords Ranking

**Include:**
- Top keywords on page 1 with their position
- Top 10 keywords moving towards page 1 (positions 11–20, trending upward)
- Estimated search volume for each keyword

**Visual format:**
Present as a clean, visual table. Matt's reference: a table that "offers a good perspective, which looks nice in a report." Use colour-coded position indicators or rank badges where appropriate. Consider grouping by position range (1–3, 4–10, 11–20).

### 6. Backlinks Profile

**Only show:**
- Total Backlinks
- Referring Domains
- Dofollow Backlinks

**Do NOT display:**
- Broken backlinks
- Spam score
- First seen dates
- Domain Rank

### 7. Google Business Profile

**Display:**
- Call Clicks
- Website Clicks
- Search vs Maps Views
- Direction Requests
- Profile Interactions
- Total Reviews
- Average Rating

**Additional items:**
- Number of GBP posts published in the last month (e.g. "30 posts published")
- Recently published pages with links (e.g. "1. www.clientdomain.com.au/new-blog")

**Rules:**
- Only compare with the previous period when performance has improved (positive).
- Present with visual graphs where possible — performance trend charts for calls, clicks, direction requests, searches.

### 8. AI / LLM Visibility

**Include:**
- Online brand mentions
- AI Overview appearances
- LLM visibility (ChatGPT, Gemini, Perplexity, Claude, etc. — where available)
- The exact keywords/queries where the business appears in AI search
- Any AI visibility trend or growth metrics

### 9. Website Audit Score

**Include:**
- Overall Audit Score (target 90%+)

If there are genuine issues worth discussing, mention them briefly in the "Next Month" section rather than dwelling on them here. Examples:
- Canonical improvements
- Broken links
- Sitemap updates
- robots.txt improvements
- llms.txt implementation
- AI optimisation recommendations

### 10. Next Month To-Do's

Refer to the client's SEO strategy in ClickUp (e.g. the strategy document created during onboarding) and align with the current report data. Identify what has changed and offer the 5 key areas of focus for the following period.

Example items:
- Resolve remaining website audit issues
- Publish 30 Google Business Profile posts to improve Local Map Pack visibility
- Create planned location pages and blog content
- Refresh underperforming service pages
- Expand FAQs and add authoritative statistics
- Improve AI optimisation for Google AI Overviews and LLM visibility
- Strengthen internal linking and topical authority

## CTA (report footer)

Use this exact CTA at the bottom of every report:

> Questions about this report? Reply to this email, or contact us at
> Support@TradieWebGuys.com.au

**Never use:** go.tradiewebguys.com.au/book

## Algorithm update note

If a significant Google Search algorithm update occurred during the reporting period, include a short note in the Executive Summary section:

> "Google released an algorithm update during this period. We have already adjusted the SEO strategy accordingly."

## Branding

- TWG-branded header and footer
- Clean, visual layout with charts and graphs where possible
- Australian English spelling throughout (colour, organise, realise, optimise)
- Professional but approachable tone
