# Client Configuration

Each client entry contains the identifiers needed to run the full pipeline.

## Active Clients

### TWG — Tradie Web Guys (internal)

| Field | Value |
|-------|-------|
| HighLevel Location ID | `cuS7M6EnfbXM2s2VJ4I8` |
| Google Drive Folder | `1V5YSNEl-ZFwAbCoBCDlJW5MwAdH0qIfe` (Call Reports) |
| ClickUp Folder ID | `901812667133` |
| ClickUp Ad Hoc List ID | `901816475942` |
| Report Mode | Individual (low volume) |
| Cron | Daily, 7am AEST — `/call-analysis/twg-daily` |

**Staff user mapping:**

| HighLevel userId | Name |
|------------------|------|
| X60V6OAZnJO04oPDCxlx | Matthew Jones |
| im9W0Hfileh9pFGOqyae | Buzz Brady |
| ojuvWyFAA7gOcCFCC4hu | Amanda Jones |
| tLSGjYPFckbMSBGHxUTV | Ethan Carter |
| qInORa48D2MhW0czd64J | Imran Noorani |

---

### PPG — Pace Plumbing And Gas

| Field | Value |
|-------|-------|
| HighLevel Location ID | `zpOFe02gJVNskkFv7Kru` |
| Google Drive Folder | `1icFJw2T3IBeJxAf4UHCz9URhESlkjOS5` (PPG - Call Summaries) |
| ClickUp Folder ID | `90185114414` |
| ClickUp Ad Hoc List ID | `901807758614` |
| Report Mode | Weekly batch (high volume — 70–80+ calls/week) |
| Cron | Weekly, Monday 8am AEST — `/call-analysis/pace-plumbing-weekly` |

**Staff user mapping:** Uses the same TWG staff IDs (TWG team handles PPG calls).

---

### HEG — Hughes Electrical Group

| Field | Value |
|-------|-------|
| HighLevel Location ID | `GZN4K82UwJN0qGZDrV2a` |
| Google Drive Folder | `1-kjW6I9fN5W8JHTutNfmD2AyzFSsnFfW` (Sales Call Analysis) |
| Google Drive Parent | `16YeWjIuz-KlbeSDwaMvVNDLQlYI_mixW` (HEG - Delivery) |
| Report Mode | Individual |

**Staff user mapping:**

| HighLevel userId | Name |
|------------------|------|
| eGV6v6fOGb45Wg2SFXKk | Benji Boys |
| OKqZbuWcUBb7RTJG51dV | Lachlan Boys |
| im9W0Hfileh9pFGOqyae | Buzz Brady |

---

## Adding a New Client

Each new client needs:

1. **HighLevel location ID** — the sub-account's locationId
2. **Client code** — the 3-letter code used in Drive and ClickUp folder names
3. **Google Drive folder ID** — the client's existing reports folder in the shared drive (never create new folders — find the existing one or ask the team)
4. **ClickUp folder and list IDs** — the client's folder in the DELIVERY space and their Ad Hoc Tasks list
5. **Staff user mapping** — HighLevel userIds mapped to staff names for the sub-account
6. **Report mode** — individual or weekly batch, based on call volume
7. **Cron schedule** (optional) — if the client wants automated recurring analysis

## Multi-Account Access

The agency token can generate location-scoped tokens for any of the 86 installed sub-accounts. No per-client manual connection is needed. See `highlevel-api.md` for the token generation endpoint.

- **App ID**: `647f5f5293cf661d5c0e8831` (Pipedream marketplace app)
- **Company ID**: `bTiMi4YoiWs5tnhivWSI`
