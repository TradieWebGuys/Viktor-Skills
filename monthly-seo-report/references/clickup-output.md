# ClickUp Output Structure

How reports are structured and stored in ClickUp.

## One-time setup (per client)

Each SEO client has a folder in the [DELIVERY] space named `{SHORTCODE} - {Client Name}`. On the first run, check whether a **Reporting** list already exists in that folder. If not, create one:

- **List name:** `Reporting`
- **Parent:** The client's folder in [DELIVERY] space (ID: `90182597483`)
- **Function:** `pd_clickup_create_list` with the client's `folderId`

## Monthly task creation

For each client, create a new task in their Reporting list:

### Task details

| Field | Value |
|-------|-------|
| **Name** | `SEO Report — {Month Year}` (e.g. "SEO Report — June 2026") |
| **Description** | The full internal report (see `internal-report-spec.md`) |
| **Assignee** | Ehtisham (ClickUp ID: `48626346`) |
| **Status** | `to do` (moves to `in review` once generated) |
| **Priority** | Normal (3) |
| **Tags** | `seo-report`, `viktor` |

### Description structure

The task description contains the full internal report in this order:

1. **Notable Wins section** (top) — 3 key wins marked for approval
2. **Full internal report** — all sections from `internal-report-spec.md`

### Approval mechanism

Add a checklist to the task called "Report Approval" with these items:
- [ ] Internal report reviewed
- [ ] Notable wins approved for marketing
- [ ] Client-facing PDF approved for delivery

When all checklist items are ticked, the report is approved and the client-facing PDF can be generated.

## Important rules

- **Post report in the description**, not in the comments. Matt was explicit about this.
- **Always create the ClickUp task first.** Do not generate the client-facing PDF until the task exists and is approved.
- **Assign to Ehtisham** (ClickUp ID: `48626346`).
- **Add the `viktor` tag** so it is clear Viktor generated the report.
- **Set status to `in review`** after posting the report, so Ehtisham knows it needs attention.

## Workspace and space IDs

| Resource | ID |
|----------|-----|
| Workspace | `308435` |
| [DELIVERY] space | `90182597483` |
| Viktor user ID | `113581164` |
| Ehtisham user ID | `48626346` |
