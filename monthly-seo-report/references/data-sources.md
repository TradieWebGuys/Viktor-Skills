# Data Sources

Exact API calls and fields for each data source used in the monthly SEO report. All date ranges are the previous complete calendar month (reporting period) and the month before that (comparison period).

## 1. Google Search Console (GSC)

**Integration**: `google_search_console` (Campaign @ account)
**Function**: `pd_google_search_console_retrieve_site_performance_data`

### Calls to make

| Call | Dimensions | Purpose |
|------|-----------|---------|
| Site-level summary | None | Total clicks, impressions, CTR, average position |
| By query | `query` | Top queries by clicks — top 20 |
| By page | `page` | Top pages by clicks — top 15 |

### Fields used

- **Clicks** — used in executive summary and search console section
- **Impressions** — used in executive summary (internal report includes CTR and position)
- **CTR** — internal report only
- **Average Position** — internal report only (removed from client-facing per Matt's feedback)

### Client-facing filtering

For the client-facing report, only show:
- Top Pages by Clicks: URL and Clicks columns only (no CTR, Impressions, or Position)

## 2. Google Analytics 4 (GA4)

**Integration**: `google_analytics` (Campaigns @ account)
**Function**: `pd_google_analytics_run_report_in_ga4`

### Calls to make

| Call | Dimensions | Metrics | Purpose |
|------|-----------|---------|---------|
| Channel breakdown | `sessionDefaultChannelGroup` | `sessions`, `totalUsers`, `newUsers`, `engagementRate`, `averageSessionDuration` | Traffic by channel |
| Top landing pages | `landingPage` | `sessions`, `totalUsers`, `engagementRate` | Top pages by traffic |
| Conversion events | `eventName` | `eventCount` | Key events (calls, emails, forms only) |
| Organic sessions | `sessionDefaultChannelGroup` (filter: Organic Search) | `sessions` | Executive summary |
| Total sessions | None | `sessions` | Executive summary |

### Fields used

- **Organic Sessions** — executive summary
- **Total Sessions** — executive summary
- **Traffic by Channel** — full table in both reports
- **Top Landing Pages** — sessions and engagement only (no conversions in client-facing)
- **Conversion Events** — filter to only: phone call clicks, email clicks, form submissions. Exclude generic page_view, scroll, session_start events.

### Client-facing filtering

- Only compare channel data with previous period when the change is positive.
- Top Landing Pages: show traffic only, do not display conversions.
- Conversion Events: only show call clicks, email clicks, and form submissions.

## 3. DataForSEO

**Integration**: `dataforseo` (Team's Account)

### Calls to make

| Call | Function | Purpose |
|------|----------|---------|
| Keyword rankings | `pd_dataforseo_get_ranked_keywords` | Keywords the domain ranks for, with position and search volume |
| Backlinks summary | `pd_dataforseo_get_backlinks_summary` | Total backlinks, referring domains, dofollow count |
| On-page audit | `pd_dataforseo_create_onpage_task` then retrieve results | Website audit score and issues |
| AI/LLM visibility | `pd_dataforseo_get_content_citations` | Brand mentions and AI visibility signals |

### Fields used

**Keywords Ranking (client-facing)**:
- Top keywords on page 1 (positions 1–10) with position and estimated search volume
- Top 10 keywords moving towards page 1 (positions 11–20, trending up)
- Present in a visual table format

**Backlinks Profile (client-facing)**:
- Total Backlinks
- Referring Domains
- Dofollow Backlinks
- Do NOT show: broken backlinks, spam score, first seen, domain rank

**Website Audit Score**:
- Overall audit score (target 90%+)
- If genuine issues exist, mention briefly in the "Next Month" section (canonicals, broken links, sitemap, robots.txt, llms.txt, AI optimisation)

**AI/LLM Visibility**:
- Online brand mentions
- AI Overview appearances
- LLM visibility (ChatGPT, Gemini, Perplexity, Claude — where available)
- Exact keywords/queries where the business appears in AI search
- AI visibility trend or growth metrics

## 4. Google Business Profile (GBP)

**Integration**: `google_my_business` (Campaigns @ account)

### Calls to make

| Call | Function | Purpose |
|------|----------|---------|
| Performance metrics | Proxy GET to Business Performance API | Calls, website clicks, direction requests, searches |
| Reviews | `pd_google_my_business_list_all_reviews` | Total reviews and average rating |
| Posts | `pd_google_my_business_list_posts` | Count of posts published in the reporting period |

### Fields used (client-facing)

- Call Clicks
- Website Clicks
- Search vs Maps Views
- Direction Requests
- Profile Interactions
- Total Reviews
- Average Rating
- Number of GBP posts published in the last month
- Recently published pages with links

### Client-facing filtering

- Only compare with previous period when there is a positive improvement.
- Present with visual graphs where possible — performance graphs, calls, clicks, direction requests, searches.

## 5. SE Ranking

**Integration**: `doppler_secretops_3` (SE Ranking Team's Account — API key stored in Doppler)

SE Ranking provides keyword position tracking and competitor comparison. Use the SE Ranking API with the API key retrieved from Doppler.

### Calls to make

- Keyword position history for the domain
- Competitor keyword comparison

### Fallback

SE Ranking API access may not be available for all clients. If the API call fails or returns no data, fall back to DataForSEO keyword data and note in the internal report that SE Ranking data was unavailable.

## Error handling

For any data source:
- If the API call fails (auth, rate limit, timeout, broken connection): skip that source for that client.
- Log: `"[ERROR] {Client Name} — {Source}: {error reason}"`
- Include in the Slack summary under "⚠️ Data source errors".
- Never use partial or cached data from a previous run.
