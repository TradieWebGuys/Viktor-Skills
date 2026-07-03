# Account Mapping

How client shortcodes map to data source IDs for each integration.

## Structure

The account mapping lives in a JSON file (`references/account_mapping.json`) with this structure:

```json
{
  "seo_clients": {
    "TWG": {
      "client": "Tradie Web Guys",
      "domain": "tradiewebguys.com.au",
      "gsc_property": "sc-domain:tradiewebguys.com.au",
      "ga4_property": "properties/XXXXXXXXX",
      "gbp_account": "accounts/XXXXXXXXX",
      "gbp_location": "locations/XXXXXXXXX",
      "dataforseo_target": "tradiewebguys.com.au"
    }
  }
}
```

## Fields per client

| Field | Source | Purpose |
|-------|--------|---------|
| `client` | ClickUp | Display name |
| `domain` | Manual | Primary domain for the client |
| `gsc_property` | GSC API | Google Search Console property URL |
| `ga4_property` | GA4 API | Google Analytics 4 property ID |
| `gbp_account` | GBP API | Google Business Profile account ID |
| `gbp_location` | GBP API | Google Business Profile location ID |
| `dataforseo_target` | Manual | Domain target for DataForSEO API calls |
| `se_ranking_project` | SE Ranking | Project ID in SE Ranking (optional) |

## Resolving IDs

When the skill runs for the first time or for a new client:
1. Use `pd_google_search_console_configure` to list available GSC properties.
2. **DO NOT use `pd_google_analytics_list_property_options`** — it only returns ~65 of 122+ properties due to a pagination bug. Instead, use the `accountSummaries` Admin API endpoint with pagination (see the `get_all_ga4_properties()` helper in the google_analytics integration skill).
3. Use `pd_google_my_business_list_accounts` and `pd_google_my_business_list_locations` to find GBP IDs.
4. Match each to the client's domain (pull data streams to get `defaultUri` for matching).
5. Store resolved IDs in the mapping file for future runs.

## Missing mappings

If a client has no entry in the mapping file:
- Skip the client for this run.
- Log a warning with the client name and shortcode.
- Include in the Slack summary so the team can add the mapping.

## Maintaining the mapping

The mapping file should be updated when:
- A new SEO client is onboarded.
- A client changes their domain.
- New data source connections are added (e.g. SE Ranking project created).

The mapping file is the only place client-specific account IDs live. All other skill files are generic.
