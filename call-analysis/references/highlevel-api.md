# HighLevel API Reference

## Base Configuration

- **Base URL**: `https://services.leadconnectorhq.com`
- **Required header**: `{"Version": "2021-07-28"}`
- **SDK function (sub-account)**: `highlevel_oauth_2_pd_highlevel_oauth_proxy_get`
- **SDK function (agency POST)**: `highlevel_oauth_pd_highlevel_oauth_proxy_post`

## Location Token Generation

The agency token generates location-scoped tokens for any sub-account.

```
POST /oauth/locationToken
Body: {"companyId": "bTiMi4YoiWs5tnhivWSI", "locationId": "<location_id>"}
```

Returns a Bearer token with all scopes. Expires in 24 hours. This POST creates a draft requiring user approval.

## Discovering Calls

### Step 1 — Search conversations

```
GET /conversations/search?locationId={location_id}
```

Returns conversations with `lastMessageDate` (epoch milliseconds — NOT ISO string).

### Step 2 — Get messages for each conversation

```
GET /conversations/{conversation_id}/messages?limit=50
```

Filter to `messageType == "TYPE_CALL"`.

### Step 3 — Download recording

```
GET /conversations/messages/{messageId}/locations/{locationId}/recording
```

**Response format varies by sub-account:**
- Check `Content-Type` header
- If `audio/x-wav`: write bytes directly to a .wav file
- If JSON: response is `{"encoding": "base64", "data": "..."}` — decode with `base64.b64decode(data)`

GHL's built-in transcription endpoint returns 404 (not available). Always use ElevenLabs Scribe v2 instead.

## Call Message Fields

| Field | Description |
|-------|-------------|
| `direction` | Inbound or outbound |
| `status` | Call status |
| `from` | Caller number |
| `to` | Recipient number |
| `dateAdded` | ISO string (e.g. `2026-06-03T05:27:02.089Z`) |
| `userId` | Staff member's HighLevel user ID |
| `contactId` | CRM contact ID |
| `meta.call.duration` | Call duration in seconds (NOT `meta.duration`) |
| `meta.call.status` | Call outcome status |

## Contact Notes

```
POST /contacts/{contactId}/notes
Body: {"body": "note text"}
```

- The agency proxy returns 401 on location-scoped endpoints like notes — use a location token via direct `urllib.request` with a `User-Agent` header (Cloudflare blocks requests without one, returning error 1010).
- The proxy also blocks custom `Authorization` headers — cannot pass location tokens through it.

## Pagination — Critical

The `skip` parameter is completely broken — returns identical results regardless of value. The parameters `sort_by`, `sort_order`, `startAfterId`, `page`, `searchAfter`, `cursor`, and `after` are all ignored.

**The only working pagination method is `startAfterDate`:**

1. Fetch a page of conversations
2. Get the minimum `lastMessageDate` from the results
3. Pass that value as `startAfterDate` in the next request
4. Repeat until no results or all results are outside the target date range

Adding `sort_by` or `sort_order` parameters may actually break `startAfterDate` pagination. Do not combine them.

## Date Format Gotchas

| Field | Format | Example |
|-------|--------|---------|
| `lastMessageDate` (on conversations) | Epoch milliseconds (integer) | `1717394822089` |
| `dateAdded` (on messages) | ISO 8601 string | `2026-06-03T05:27:02.089Z` |

Parse `lastMessageDate` with `datetime.fromtimestamp(val / 1000, tz=timezone.utc)`.
