# Account Mapping

How client shortcodes map to data source IDs for each integration.

## Structure

The account mapping lives in `references/account_mapping.json`:

```json
{
  "seo_clients": {
    "NGE": {
      "client": "NG Elec",
      "domain": "ngelec.com.au",
      "gsc_property": "sc-domain:ngelec.com.au",
      "ga4_property": "properties/XXXXXXXXX",
      "gbp_account": "accounts/XXXXXXXXX",
      "gbp_location": "locations/XXXXXXXXX",
      "dataforseo_target": "ngelec.com.au"
    }
  }
}
```

## Fields Per Client

| Field | Source | Purpose |
|-------|--------|---------|
| `client` | ClickUp | Display name |
| `domain` | Manual | Primary domain |
| `gsc_property` | GSC API | Search Console property URL |
| `ga4_property` | GA4 API | Analytics 4 property ID |
| `gbp_account` | GBP API | Business Profile account ID |
| `gbp_location` | GBP API | Business Profile location ID |
| `dataforseo_target` | Manual | Domain for DataForSEO calls |

**No SE Ranking fields.** SE Ranking is not used.

## Resolving IDs for New Clients

1. **GSC:** Use `pd_google_search_console_configure` to list available properties.
2. **GA4:** Use `accountSummaries` Admin API with pagination. **DO NOT use `pd_google_analytics_list_property_options()`** — pagination bug returns ~65 of 122+ properties. Match via data streams `defaultUri`.
3. **GBP:** Use `pd_google_my_business_list_accounts` and `pd_google_my_business_list_locations`.
4. **DataForSEO:** Use the client's primary domain from their KB.

Store resolved IDs in the mapping JSON for future runs.

## Missing Mappings

If a client in the ClickUp SEO view has no mapping entry:
- Skip for this run.
- Log: `"[SKIP] {Client Name} ({shortcode}) — no data source IDs in account mapping"`
- Include in Slack summary under "⚠️ Missing account mappings."

## Current Clients (12)

Shortcodes from ClickUp: COF, ATS, SPC, TCE, BEC, OPG, L4L, HDK, LDY, SLM, CLE, NGE.

The mapping JSON must be populated with real IDs via the resolution process above before reporting can run for each client.
