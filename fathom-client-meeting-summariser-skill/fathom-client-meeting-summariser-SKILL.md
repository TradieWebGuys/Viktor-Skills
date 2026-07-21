---
name: fathom_meeting_processor
description: >-
  Processes Fathom meeting transcripts for TWG client calls — identifies the client,
  files the Fathom AI summary as a new ClickUp Doc page under the client's Project Hub
  Meetings section (organized by Australian financial year), reads the client's Roadmap
  and Current Focus pages, analyzes the transcript for updates needed, and posts a Slack
  summary for approval before making changes. Triggered by a Zapier automation that posts
  a Slack message with meeting title, Fathom recording link, and attached transcript.
  Use when a Zapier message says "call has been completed", or someone says "process this
  meeting", "file meeting notes", "meeting transcript for a client", or "process fathom
  meeting". Output changes are a draft for the meeting conductor to approve.
---

# Fathom Meeting Processor

Processes a completed Fathom meeting call for a TWG client: files the AI summary into ClickUp, analyzes the transcript against the client's Roadmap and Current Focus, and proposes updates for approval.

The most important thing to get right: **never update a ClickUp doc without explicit Slack approval from the meeting conductor.**

## Inputs

The trigger is a Slack message (usually from Zapier) in this format:

```
@Viktor call has been completed with {conductor_name}, {invitee_names}

Meeting title: {meeting_title}
Meeting link: {fathom_recording_url}
```

With the Fathom transcript attached as a file.

- **Meeting title** (required) — extracted from the message. Used to identify the client and meeting type.
- **Fathom recording link** (required) — URL like `https://fathom.video/calls/{id}` or `https://app.fathom.video/...`. Used to pull the recording ID for the Fathom API.
- **Conductor name** (required) — the TWG team member who ran the call. Extracted from the message.
- **Attached transcript** (required) — the Fathom transcript file attached to the Slack message.

Missing-input handling: if the meeting title, Fathom link, or transcript is missing, reply in-thread asking for the missing piece. Do not guess.

## Workflow

### Step 0: Parse the incoming message

Extract from the triggering Slack message:

1. **Conductor name** — the name after "call has been completed with" (first name before the comma).
2. **Invitee names** — the name(s) after the comma (the client-side attendees).
3. **Meeting title** — the line starting with "Meeting title:".
4. **Fathom recording URL** — the line starting with "Meeting link:".
5. **Attached transcript** — download the attached file from Slack.

Map the conductor name to their Slack user ID using `references/team-roster.md`. This is who gets tagged for approval in Step 6.

### Step 1: Identify the client

Parse the meeting title and invitee names to identify which TWG client this meeting is about. Client meetings typically include the client contact's name and/or the TWG team member's name in the title (e.g., "David Casnji & Ethan Carter Marketing Strategy Call").

To find the client:

1. Pull the list of active clients from the ClickUp Account Health Tracker (list ID `901804854897`). Each task has a **Client Name** and **Shortcode** custom field.
2. Match the invitee names or meeting title keywords against client contact names, business names, or shortcodes.
3. If no confident match is found, reply in Slack asking the conductor to confirm the client.

Once matched, get the client's **folder ID** in the ClickUp [DELIVERY] space (space `90182597483`). Client folders follow the pattern `{SHORTCODE} - {Client Name}`.

### Step 2: Determine the meeting type

Classify the meeting type from the **meeting title** using these rules (check in order):

| Title contains (case-insensitive) | Meeting type |
|---|---|
| "onboarding" | Onboarding |
| "strategy" or "roadmap" | Strategy Review |
| "check-in" or "catch-up" or "catch up" or "check in" | Check-in Call |
| "impact" | Impact Roadmap |
| "L10" | L10 Meeting |
| None of the above | Meeting |

### Step 3: Pull the Fathom AI summary

Extract the **recording ID** from the Fathom URL. The URL format is typically `https://fathom.video/calls/{call_id}` — the call_id may differ from the recording_id.

To get the recording ID:

1. List recent meetings via `pd_fathom_list_meetings()` with a narrow date window around the meeting date.
2. Match by meeting title or URL to find the correct meeting record.
3. Extract the `recording_id` from the matched meeting.
4. Call `pd_fathom_get_recording_summary(recordingId=recording_id)` to get the AI-generated summary.

The summary is markdown-formatted text with sections like Meeting Purpose, Key Takeaways, Topics, and Action Items.

If the Fathom API call fails or returns no summary, use the attached transcript as fallback content. Note in the ClickUp doc that the Fathom AI summary was unavailable.

### Step 4: File the meeting in ClickUp

Create a new page in the client's **Project Hub** doc under the **Meetings** section, organized by Australian financial year.

**4a. Find the Project Hub doc**

Search for docs in the client's folder:

```
GET /api/v3/workspaces/308435/docs?parent_id={folder_id}&parent_type=5
```

Look for a doc with "Project Hub" in the name. If no Project Hub doc exists, check for a "Client Profile" doc with a meetings-related page. See `references/clickup-docs-api.md` for full API patterns.

**4b. Find the Meetings page**

List the doc's pages and find the one named "Meetings", "Client Meeting Notes", or "Client Impact Meetings":

```
GET /api/v3/workspaces/308435/docs/{doc_id}/pages
```

If no Meetings page exists, create one named "Meetings" as a top-level page in the doc.

**4c. Determine the financial year**

Australian financial year runs **1 July to 30 June**. A meeting on 15 March 2026 falls in **FY25-26**. A meeting on 10 August 2026 falls in **FY26-27**.

Format: `FY{start_year_short}-{end_year_short}` → e.g., `FY25-26`, `FY26-27`.

**4d. Find or create the FY sub-page**

Look for an existing sub-page under the Meetings page named with the financial year (e.g., "FY25-26"). If it does not exist, create it:

```
POST /api/v3/workspaces/308435/docs/{doc_id}/pages
Body: {"name": "FY25-26", "content": "", "parent_page_id": "{meetings_page_id}"}
```

**4e. Create the meeting entry page**

Create a new sub-page under the FY page with:

- **Title**: `[dd/mm/yy] - {Meeting Type}` (e.g., "21/07/26 - Strategy Review")
- **Content**: The Fathom AI summary markdown from Step 3

```
POST /api/v3/workspaces/308435/docs/{doc_id}/pages
Body: {
  "name": "[dd/mm/yy] - Meeting Type",
  "content": "{fathom_summary_markdown}",
  "parent_page_id": "{fy_page_id}"
}
```

All ClickUp write operations create drafts requiring approval. Submit the drafts for the meeting filing — these are internal records, not client-facing.

### Step 5: Read Roadmap Timeline and Current Focus

From the same Project Hub doc's pages (fetched in Step 4b), find these two pages. They are top-level pages in the Project Hub doc (not nested under another page). Names may include emoji prefixes.

**5a. 🗺️ Roadmap Timeline**

Search for a page with "Roadmap" in the name (e.g., "🗺️ Roadmap Timeline" or "CPG Roadmap (07/05/26)"). This page tracks the client's full journey with milestone tables organized by quarter. Template structure:

```markdown
# 🗺️ Roadmap Timeline
## Q[X] [YYYY/YYYY] — [Month]–[Month] [Year] _(Current)_
| Milestone | Status | Started | Completed | Key Decision / Outcome |
## Q[X-1] [YYYY/YYYY] — [Month]–[Month] [Year]
| Milestone | Status | Started | Completed | Key Decision / Outcome |
```

Status values: ✅ Done · 🔄 In Progress · ⏳ Queued · ⚡ External Event · 🔴 Overdue · 🛑 Paused · 📝 Noted

**5b. 📍 Current Focus**

Search for a page with "Current Focus" or "Focus" in the name (e.g., "📍 Current Focus"). This page tracks the current quarter's priorities, active milestones, KPIs, and next steps. Template structure:

```markdown
# 📍 Current Quarter Focus — Q[X] [YYYY/YYYY]
## This Quarter's Priorities
1. **[Priority 1]** — [description]
## 🔄 Active Milestones
| Milestone | Status | Owner | Notes |
## 📊 Current KPIs
| Metric | Current | Target | Status |
## 📅 Next Steps
- [Action item — who, by when]
```

Status values: ✅ Done · 🔄 In Progress · ⏳ Queued · 🔴 Action Required · 🛑 Paused

If either page does not exist, note that in the Slack summary (Step 6) and skip that part of the analysis. Do not create these pages — they are maintained manually by the team.

Read each page's content via:

```
GET /api/v3/workspaces/308435/docs/{doc_id}/pages/{page_id}
```

### Step 6: Analyze and post Slack summary

Read the attached transcript (downloaded in Step 0). Compare it against the Roadmap and Current Focus content to identify:

- **Completed milestones** — Roadmap Timeline items discussed as done → mark ✅ Done with completion date and outcome.
- **New milestones or changes** — new goals, shifted timelines, or changed priorities → add rows to the current quarter's table in Roadmap Timeline.
- **Updated focus areas** — changes to current quarter priorities, KPIs, or active milestones → update the Current Focus page sections.
- **Action items** — specific next steps mentioned, with owners if stated → add to Current Focus "Next Steps" section.
- **Key discussion points** — important topics covered in the meeting.

Post a Slack message **in the same thread** as the triggering message with:

1. ✅ Confirmation that the meeting summary has been filed in ClickUp (with a link to the doc).
2. A brief summary of key discussion points.
3. **Proposed Roadmap updates** — specific changes to make, shown as a diff (what to add, change, or mark complete).
4. **Proposed Current Focus updates** — specific changes to make.
5. A clear ask: "Please approve these updates or let me know what to change."
6. **Tag the meeting conductor** by their Slack user ID (from `references/team-roster.md`).

If no updates are needed for Roadmap or Current Focus, say so clearly and skip the approval step.

### Step 7: Apply approved updates

When the meeting conductor replies with approval:

1. Update the **Roadmap page** content with the approved changes.
2. Update the **Current Focus page** content with the approved changes.

Use the ClickUp Docs API to update page content:

```
PUT /api/v3/workspaces/308435/docs/{doc_id}/pages/{page_id}
Body: {"content": "{updated_markdown}"}
```

These updates create drafts requiring approval — submit them.

If the conductor requests modifications to the proposed changes, adjust and resubmit for approval. Do not update without explicit approval.

## Guardrails

- **Draft plus human review for all doc updates.** The meeting summary filing (Step 4) can proceed without conductor approval (it is an internal record). Roadmap and Current Focus updates (Step 7) require explicit approval from the meeting conductor before executing.
- **Never fabricate content.** If the Fathom API is unavailable, say so. If the transcript does not clearly support a proposed update, do not propose it. When in doubt, quote the relevant transcript passage.
- **Pause on ambiguous client identification.** If the client cannot be confidently matched from the meeting title and attendees, ask — do not guess the wrong client folder.
- **No external sends.** This skill works entirely within internal systems (ClickUp, Slack). It does not email clients or post publicly.
- **Preserve existing doc content.** When updating Roadmap or Current Focus pages, merge changes into the existing content. Never overwrite the entire page — only modify the specific sections that need updating.
- **Writing:** plain, direct, active sentences. Avoid filler (delve, leverage, robust, seamless, unlock, streamline, elevate). State findings straight.

## Reference files

| File | Use it for |
|---|---|
| `references/team-roster.md` | Map conductor names to Slack IDs and email addresses for tagging and Fathom matching |
| `references/clickup-docs-api.md` | ClickUp v3 Docs API endpoints, request/response patterns, and known quirks |
