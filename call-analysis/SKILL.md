---
name: call-analysis
description: Analyse phone call recordings from GoHighLevel sub-accounts — download, transcribe, score, and deliver coaching reports. Use when someone asks to "analyse calls", "run call analysis", "review call recordings", "score the calls", "process calls for [client]", "call coaching report", "how did [staff] go on the phones", or "pull the call data from HighLevel". Produces individual or weekly batch reports delivered to Google Drive, ClickUp, and HighLevel CRM notes. Output is a draft for the account manager to review before sharing with the client.
---

# Call Analysis

Download phone call recordings from a client's GoHighLevel sub-account, transcribe them, run AI-powered scoring and coaching analysis, and deliver reports across four channels: Google Drive, ClickUp, HighLevel contact notes, and Slack.

The single most important thing: every report is a draft for internal review. No call analysis output goes to a client without a human reviewing it first.

## Inputs

- **Client name or code** (required) — the 3-letter client code (e.g. TWG, PPG, HEG) or client name. Used to look up the client's HighLevel location, Drive folder, and ClickUp list. If not provided, ask.
- **Date range** (optional) — defaults to "since last run" for cron, or "last 7 days" for ad hoc requests. Accepts natural language ("last week", "May 13–20").
- **Report mode** (inferred) — individual per-call reports for low-volume accounts (under 15 calls/week), weekly batch summary for high-volume accounts. Can be overridden by the requester.

Missing-input handling: if the client code is missing or unrecognised, pause and ask. Do not guess.

## Workflow

### 1. Look up client configuration

Load the client's HighLevel location ID, Google Drive folder ID, ClickUp list ID, and staff user-ID mapping from `references/client-config.md`. If the client is not listed, ask the requester for the details before proceeding.

### 2. Generate a location token

Use the HighLevel agency token to generate a location-scoped Bearer token for the client's sub-account. Token details are in `references/highlevel-api.md`.

### 3. Discover calls in the date range

Search the sub-account's conversations, filter to call-type messages, and collect recordings. Pagination and date filtering details are in `references/highlevel-api.md`.

Skip calls that have already been processed (check the client's processed-calls log to avoid duplicates).

### 4. Download and transcribe each recording

Download the recording from HighLevel (handles both base64 and direct binary responses). Transcribe using ElevenLabs Scribe v2 speech-to-text.

### 5. Analyse the transcript

For each call, produce:
1. **Call details** — staff member, contact name, duration, direction, date
2. **Overall score** (out of 10) and sentiment classification
3. **Outcome** — booked, lost, voicemail, follow-up required, general enquiry
4. **Executive summary** — 2–3 sentences
5. **Contact detail capture check** — did the agent obtain and confirm the essential lead details (name, phone, email, business name, web address, location, service type)? Flag anything missing, and flag any follow-up the agent committed to (email, callback, quote) without capturing the detail needed to deliver it.
6. **Sentiment arcs** — staff and caller emotional trajectory
7. **What went well** — with transcript evidence
8. **Areas for improvement** — with coaching notes and suggested scripts
9. **Lead quality assessment** — for sales/enquiry calls only
10. **Call tags** — auto-categorisation

For weekly batch mode, also produce:
- Aggregate booking rate and conversion metrics
- Per-staff performance comparison
- Top coaching priorities across all calls
- Trend comparison with previous period

Full report section specifications are in `references/report-spec.md`.

### 6. Deliver the report

Deliver across four channels:

1. **Google Drive** — create a Google Doc in the client's reports folder. Share with `tradie@tradiewebguys.com.au`. Doc creation details in `references/delivery.md`.
2. **ClickUp** — create a task in the client's Ad Hoc Tasks list with a summary and link to the Google Doc.
3. **HighLevel contact note** — add a summary note to each contact's CRM profile (score, sentiment, outcome, action items, link to full report).
4. **Slack** — post a digest to the designated channel with key metrics and any calls flagged for urgent attention.

### 7. Log processed calls

Record each processed call's message ID in the client's log to prevent duplicate processing on subsequent runs.

## Output

- **Individual mode**: one Google Doc per call with full coaching analysis
- **Batch mode**: one Google Doc covering all calls in the period, with per-call breakdowns and aggregate metrics
- ClickUp task with summary and doc link
- HighLevel contact notes on each caller's profile
- Slack digest message

All outputs are drafts for the account manager to review. Nothing is shared with the client automatically.

## Guardrails

- Draft plus human review for anything client-facing. Reports are internal tools — the account manager decides what (if anything) to share with the client.
- No external sends without approval. Reports go to internal Drive, internal ClickUp, and internal Slack only.
- Pause on missing inputs. If the client code is not recognised or a required integration is unavailable, stop and ask.
- Never fabricate data. If a recording fails to download or transcribe, log the failure and skip that call — do not invent a transcript or score.
- Keep internal coaching notes out of any client-facing communication. Scores, improvement areas, and suggested scripts are for staff development only.
- Confirm before processing large batches. If more than 50 calls are queued, confirm with the requester before proceeding (credit consciousness).
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Reference files

| File | Use it for |
|------|------------|
| `references/client-config.md` | Client roster — location IDs, Drive folders, ClickUp lists, staff mappings |
| `references/highlevel-api.md` | HighLevel API endpoints, authentication, pagination, and known quirks |
| `references/report-spec.md` | Full report template — sections, scoring criteria, batch vs individual format |
| `references/delivery.md` | Google Drive, ClickUp, HighLevel notes, and Slack delivery details |
