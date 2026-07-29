# Pre-Flight Access Checks

Lightweight API calls to verify working access to each data source before the report runs. Every check is the minimum possible call — confirm access without pulling report data or burning credits.

## Schedule

Runs as a separate cron on the **last day of the month at 7am AEST**, giving the team ~48 hours to fix broken connections before the report fires on the 2nd.

## Google Search Console (GSC)

**Integration:** `google_search_console` (Campaign @ account)

**Check:** Call `pd_google_search_console_retrieve_site_performance_data` with the client's `gsc_property`, requesting just 1 day of data (yesterday), no dimensions.

| Result | Meaning |
|--------|---------|
| PASS | Returns a valid response (even zeros) |
| FAIL | Auth error, property not found, permission denied |
| WARN | Timeout or rate limit (transient) |

**Common failures:** Property not shared with service account. URL mismatch (http vs https, www vs non-www, domain vs URL prefix). Permissions revoked.

## Google Analytics 4 (GA4)

**Integration:** `google_analytics` (Campaigns @ account)

**Check:** Call `pd_google_analytics_proxy_get` with `https://analyticsadmin.googleapis.com/v1beta/{ga4_property}` — a free metadata check.

| Result | Meaning |
|--------|---------|
| PASS | Returns property details with valid displayName |
| FAIL | Auth error, property not found, permission denied |
| WARN | Timeout or rate limit |

**⚠ DO NOT use `pd_google_analytics_list_property_options()`** — pagination bug returns ~65 of 122+ properties. Use `accountSummaries` Admin API with pagination for discovery.

**Common failures:** Property not shared with campaigns@ account. Wrong property ID (UA instead of GA4). Property deleted or migrated.

## Google Business Profile (GBP)

**Integration:** `google_my_business` (Campaigns @ account)

**Check:** Call `pd_google_my_business_list_locations` for the client's `gbp_account`.

| Result | Meaning |
|--------|---------|
| PASS | Expected location found in response |
| FAIL | Auth error, account not found, location not found |
| WARN | Account accessible but expected location ID missing (mapping issue) |

**Common failures:** Account ownership transferred. Location removed or merged. API permissions revoked.

## DataForSEO

**Integration:** `dataforseo` (Team's Account)

**Check:** Call `pd_dataforseo_get_ranked_keywords` with the client's `dataforseo_target` domain, limit 1.

| Result | Meaning |
|--------|---------|
| PASS | Returns at least one keyword result |
| FAIL | Auth error or API error |
| WARN | Empty results (new domain or not indexed — valid but worth noting) |

**Common failures:** API key expired or rate-limited. Domain typo in mapping.

## General Rules

1. **One check per source per client.** No redundant calls.
2. **Timeout:** 30 seconds. Timeout = WARN, not FAIL.
3. **Rate limits:** Wait 5s and retry once. Still limited = WARN.
4. **Error capture:** Always capture the exact error message for the ClickUp/Slack alert.
5. **Credit awareness:** Use negligible credits (1 row, 1 day, metadata only).

## Failure Handling

When a check returns FAIL:

1. **ClickUp urgent channel** (`9d6k-176338`): Post via direct API (`POST /api/v2/view/9d6k-176338/comment`) with `assignee: 48626346` (Ehtisham, integer):
   ```
   🚨 [Client Name] — [Source] connection failed.
   Error: [exact error message]
   SEO report blocked until resolved. Report runs on the 2nd.
   ```

2. **Slack summary:** List all results (pass/fail/warn) per client in a table.

When all checks pass: no ClickUp post needed. Slack summary confirms all clear.

## Results Storage

Write results to a temporary file so the report cron can read them on the 2nd:
- Path: `skills/clients/{shortcode}/seo/preflight-results.json`
- Structure: `{"date": "2026-06-30", "results": {"gsc": "pass", "ga4": "pass", "gbp": "fail", "dataforseo": "pass"}, "errors": {"gbp": "Location not found"}}`

The report cron checks this file. If any source shows FAIL and was not resolved (no re-check showing pass), the report skips that client and re-flags in Slack.
