# Report Registry

Maps each scheduled report to its required integrations, ClickUp filtering logic, and account mapping location.

## Monthly SEO Report

- **Skill name**: `monthly-seo-report`
- **Schedule**: 1st of each month, 7am AEST
- **ClickUp filter**: Clients with `SEO` in their `🤝 Services` custom field, status set to `Active`
- **Account mapping**: `monthly-seo-report/references/account_mapping.json` (maps shortcodes to GSC, GA4, GBP, DataForSEO, SE Ranking IDs)

### Required integrations per client

| Integration | Field in mapping | Required | Notes |
|-------------|-----------------|----------|-------|
| Google Search Console | `gsc_property` | Yes | Core data source — clicks, impressions, queries, pages |
| Google Analytics 4 | `ga4_property` | Yes | Sessions, channel breakdown, conversions |
| Google Business Profile | `gbp_account`, `gbp_location` | Yes | Calls, clicks, directions, reviews |
| DataForSEO | `dataforseo_target` | Yes | Rankings, backlinks, audit score, AI visibility |
| SE Ranking | `se_ranking_project` | No | Optional — falls back to DataForSEO if unavailable. Mark as WARN not FAIL if missing. |

### Failure impact

If GSC, GA4, GBP, or DataForSEO access fails for a client, that client's report will be incomplete. Flag as `FAIL`.
If SE Ranking access fails, flag as `WARN` (the report can proceed using DataForSEO fallback, but note the limitation).

## Daily Ads Report

- **Skill name**: `daily-ads-report`
- **Schedule**: Daily at 6am AEST
- **ClickUp filter**: Clients with `PDSOCL (META)` and/or `PDSRCH (GOOGLE)` in their `🤝 Services` custom field
- **Account mapping**: `daily-ads-report/references/account_mapping.json` (maps ad account IDs to client shortcodes)

### Required integrations per client

| Integration | Mapping key | Required when |
|-------------|------------|---------------|
| Meta Ads | Account ID in `meta_ads` section | Client has `PDSOCL (META)` service |
| Google Ads | Account ID in `google_ads` section | Client has `PDSRCH (GOOGLE)` service |

### Failure impact

If Meta Ads access fails for a PDSOCL client, or Google Ads access fails for a PDSRCH client, that client will be skipped in the daily report. Flag as `FAIL`.

## Adding new report types

When a new scheduled report is created, add an entry here with:
1. The skill name and schedule
2. The ClickUp filter logic
3. The account mapping location
4. The required integrations per client and their failure impact
