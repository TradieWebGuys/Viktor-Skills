# Data Sources

API calls and fields for each data source. All date ranges: previous complete calendar month (reporting period) vs the month before that (comparison period).

**Only these 4 sources. No SE Ranking, no Meta Ads, no Google Ads.**

## 1. Google Search Console (GSC)

**Integration:** `google_search_console` (Campaign @ account)
**Function:** `pd_google_search_console_retrieve_site_performance_data`

### Calls

| Call | Dimensions | Purpose |
|------|-----------|---------|
| Site-level summary | None | Total clicks, impressions, CTR, avg position |
| By query | `query` | Top 20 queries by clicks |
| By page | `page` | Top 15 pages by clicks |

### Client-facing filtering

Show only: Top Pages by Clicks with URL + Clicks columns. No CTR, no impressions, no position.

## 2. Google Analytics 4 (GA4)

**Integration:** `google_analytics` (Campaigns @ account)
**Function:** `pd_google_analytics_run_report_in_ga4`

### Calls

| Call | Dimensions | Metrics | Purpose |
|------|-----------|---------|---------|
| Channel breakdown | `sessionDefaultChannelGroup` | `sessions`, `totalUsers`, `newUsers`, `engagementRate`, `averageSessionDuration` | Traffic by channel |
| Top landing pages | `landingPage` | `sessions`, `totalUsers`, `engagementRate` | Top pages by traffic |
| Conversion events | `eventName` | `eventCount` | Key events only |
| Organic sessions | `sessionDefaultChannelGroup` (filter: Organic Search) | `sessions` | Executive summary |
| Total sessions | None | `sessions` | Executive summary |

### Client-facing filtering

- Only compare channels when change is positive.
- Top Landing Pages: traffic only, no conversions.
- Conversion Events: show only phone call clicks, email clicks, form submissions. Exclude page_view, scroll, session_start.

## 3. DataForSEO

**Integration:** `dataforseo` (Team's Account)

### Calls

| Call | Function | Purpose |
|------|----------|---------|
| Keyword rankings | `pd_dataforseo_get_ranked_keywords` | Keywords ranked, position, search volume |
| Backlinks summary | `pd_dataforseo_get_backlinks_summary` | Total backlinks, referring domains, dofollow |
| On-page audit | `pd_dataforseo_create_onpage_task` → retrieve | Audit score and issues |
| AI/LLM visibility | `pd_dataforseo_get_content_citations` | Brand mentions, AI visibility |

### Client-facing filtering

**Keywords:** Page 1 keywords (positions 1–10) + top 10 moving towards page 1 (11–20, trending up). With position and search volume.

**Backlinks:** Total, referring domains, dofollow only. No spam score, no broken links, no first seen, no domain rank.

**Audit:** Overall score only. Issues mentioned briefly in "Next Month" section if genuine (canonicals, broken links, sitemap, robots.txt, llms.txt).

**AI/LLM:** Brand mentions, AI Overview appearances, LLM visibility (ChatGPT, Gemini, Perplexity, Claude), exact queries, trend/growth metrics.

## 4. Google Business Profile (GBP)

**Integration:** `google_my_business` (Campaigns @ account)

### Calls

| Call | Function | Purpose |
|------|----------|---------|
| Performance metrics | Proxy GET to Business Performance API | Calls, clicks, directions, searches |
| Reviews | `pd_google_my_business_list_all_reviews` | Total reviews, avg rating |
| Posts | `pd_google_my_business_list_posts` | Posts published count (filter to reporting period) |

### Client-facing fields

- Call Clicks, Website Clicks, Direction Requests, Search vs Maps Views, Profile Interactions
- Total Reviews, Average Rating
- Number of GBP posts actually published this month (Mon/Wed/Fri schedule — report actual count, not a target)
- Recently published pages with links

Only compare with previous period when improvement is positive.

## Error Handling

For any source, on any error (auth, rate limit, timeout, broken connection):
- Skip that source for that client.
- Log: `"[ERROR] {Client Name} — {Source}: {error reason}"`
- Include in Slack summary under "⚠️ Data source errors."
- Never use partial, cached, or stale data from a previous run.
