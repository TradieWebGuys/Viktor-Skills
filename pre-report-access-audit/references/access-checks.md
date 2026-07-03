# Access Checks

Lightweight API calls to verify Viktor has working access to each integration for a specific client. Every check should be the minimum possible call — confirm access exists without pulling full report data or burning unnecessary credits.

## Google Search Console (GSC)

**Integration**: `google_search_console` (Campaign @ account)

**Check method**: Call `pd_google_search_console_retrieve_site_performance_data` with the client's `gsc_property`, requesting just 1 day of data (yesterday) with no dimensions.

- **PASS**: Returns a valid response with at least one row of data (even zeros).
- **FAIL**: Returns an auth error, "property not found", or permission denied.
- **WARN**: Returns a timeout or rate limit error (may be transient).

**Common failure reasons**:
- GSC property not shared with the service account
- Property URL mismatch (http vs https, www vs non-www, domain property vs URL prefix)
- Service account permissions revoked

## Google Analytics 4 (GA4)

**Integration**: `google_analytics` (Campaigns @ account)

**Check method**: Call `pd_google_analytics_proxy_get` with `https://analyticsadmin.googleapis.com/v1beta/{ga4_property}` to verify the property is accessible. This is a free metadata check (no draft, no credits).

- **PASS**: Returns property details with a valid `displayName`.
- **FAIL**: Returns auth error, property not found, or permission denied.
- **WARN**: Returns a timeout or rate limit error.

**⚠️ Property discovery note**: Do NOT use `pd_google_analytics_list_property_options()` to find GA4 properties — it only returns ~65 of 122+ due to a pagination bug. Use the `accountSummaries` Admin API endpoint with pagination instead (see google_analytics integration skill for the helper function).

**Common failure reasons**:
- GA4 property not shared with the campaigns@ account
- Wrong property ID (UA property instead of GA4)
- Property deleted or migrated

## Google Business Profile (GBP)

**Integration**: `google_my_business` (Campaigns @ account)

**Check method**: Call `pd_google_my_business_list_locations` for the client's `gbp_account` to confirm the account and location are accessible.

- **PASS**: Returns the expected location in the response.
- **FAIL**: Returns auth error, account not found, or location not found.
- **WARN**: Account accessible but expected location ID not in the response (may be a mapping issue).

**Common failure reasons**:
- GBP account ownership transferred
- Location removed or merged
- API permissions revoked

## DataForSEO

**Integration**: `dataforseo` (Team's Account)

**Check method**: Call `pd_dataforseo_get_ranked_keywords` with the client's `dataforseo_target` domain, requesting limit of 1 result.

- **PASS**: Returns at least one keyword result.
- **FAIL**: Returns auth error or API error.
- **WARN**: Returns empty results (domain may be new or not indexed — valid but worth noting).

**Common failure reasons**:
- DataForSEO API key expired or rate-limited
- Domain typo in the mapping

## SE Ranking

**Integration**: `doppler_secretops_3` (SE Ranking Team's Account — API key in Doppler)

**Check method**: Retrieve the SE Ranking API key from Doppler, then make a lightweight API call to list projects or check the client's `se_ranking_project` status.

- **PASS**: API key valid and project accessible.
- **FAIL**: API key expired or project not found.
- **WARN**: No `se_ranking_project` in the mapping (expected — SE Ranking is optional). This is the normal state for many clients.

**Important**: SE Ranking failures are always `WARN`, never `FAIL`, because the monthly SEO report falls back to DataForSEO data when SE Ranking is unavailable.

## Meta Ads

**Integration**: `meta_ads` (Team's Account)

**Check method**: Call `pd_meta_ads_get_adaccount` with the client's ad account ID to confirm the account is accessible and active.

- **PASS**: Returns account info with `account_status` = 1 (active).
- **FAIL**: Returns auth error, account not found, or permission denied.
- **WARN**: Account accessible but status is not active (paused, disabled, etc.) — may be intentional.

**Common failure reasons**:
- Ad account removed from Business Manager
- User permissions revoked
- Account disabled by Meta

## Google Ads

**Integration**: `google_ads` (Team's Account)

**Check method**: Call `pd_google_ads_search` with the client's customer ID, querying `SELECT customer.id, customer.descriptive_name FROM customer` (a minimal metadata query that returns the account name).

- **PASS**: Returns the customer record.
- **FAIL**: Returns auth error, customer ID not found, or permission denied.
- **WARN**: Returns a timeout (may be transient).

**Common failure reasons**:
- MCC access to the client account revoked
- Client account suspended or cancelled
- Wrong customer ID in the mapping

## General rules for all checks

1. **One check per integration per client.** Do not run multiple calls to the same integration for the same client.
2. **Timeout**: Set a 30-second timeout per check. If it times out, mark as `WARN` not `FAIL` (transient network issues should not block reports).
3. **Rate limiting**: If a check returns a rate limit error, wait 5 seconds and retry once. If still rate-limited, mark as `WARN`.
4. **Error capture**: Always capture the exact error message — it goes into the Slack alert to help the team diagnose.
5. **Credit awareness**: These checks should use negligible credits. If an integration charges per call, use the absolute minimum query (1 row, 1 day, metadata only).
