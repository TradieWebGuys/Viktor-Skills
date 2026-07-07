# Delivery Channels

## 1. Google Drive

### Creating the report document

1. Create the Google Doc in My Drive first using `gdrive_google_docs_create(title, content)` — creating directly in shared drive folders fails with 404.
2. Parse the document ID from the response status string using `r"ID:\s*([A-Za-z0-9_-]+)"`.
3. Move the document to the client's reports folder using `gdrive_move()`.
4. Share with `tradie@tradiewebguys.com.au` (permission = "writer") using `gdrive_share()`. Service-account-created docs are not automatically accessible to the team, even in shared drives.

### SDK details

- Module: `sdk.tools.gdrive`
- Create function: `gdrive_google_docs_create(title, content)` — NOT `gdrive_create`
- Share function: `gdrive_share()` — pass plain file ID as `unified_uri`, NOT `gdrive://ID` prefix
- Shared drive: `3. Delivery (Client)` contains `_Client Folders`

### Folder rules

- Never create new client folders. Clients already have existing folders.
- Client delivery folders may live outside `_Client Folders` (e.g. directly in shared drives or separate structures).
- The `_Client Folders` listing is truncated — may not show all clients.
- `gdrive_search` is unreliable for finding shared drive folders. If you cannot locate a client's folder, ask the requester.
- Reports go under the client's delivery subfolder, not directly in `_Client Folders`.

### Document naming

- Individual: `Call Analysis — {Staff} → {Contact} — {Date}`
- Weekly batch: `Weekly Call Report — {Client} — {Date Range}`

## 2. ClickUp

- Workspace: `308435`
- DELIVERY space: `90182597483`
- Create a task in the client's Ad Hoc Tasks list
- Task title: same as the Google Doc name
- Task description: summary with score, outcome, key findings, and link to the full Google Doc
- Assignee: the account manager for the client

## 3. HighLevel Contact Notes

For each call, add a note to the contact's CRM profile:

**Note format:**
```
📞 Call Analysis — {Date}
Score: {X}/10 | Sentiment: {sentiment} | Outcome: {outcome}

Summary: {2-sentence summary}

Key Details:
- {detail 1}
- {detail 2}

Action Items:
- {action 1}
- {action 2}

Full Report: {Google Doc URL}
```

**Technical notes:**
- Use `POST /contacts/{contactId}/notes` with `{"body": "note text"}`
- Must use location token via direct `urllib.request` (not the agency proxy)
- Include a `User-Agent` header — Cloudflare blocks bare requests (error 1010)
- The proxy blocks custom `Authorization` headers, so location tokens cannot be passed through it

## 4. Slack Digest

Post a summary message to the designated Slack channel after processing:

**Individual mode:** one message per call with score, outcome, and doc link.

**Batch mode:** single digest message with:
- Total calls processed and booking rate
- Per-staff summary (calls, avg score, booking rate)
- Any calls flagged for urgent attention
- Link to the full Google Doc report

## Duplicate Prevention

Track processed calls by `messageId` in a persistent log file per client (stored in the workspace). On each run, compare discovered calls against the log and only process new ones.
