# ClickUp Output Structure

How reports are structured and stored in ClickUp.

## One-Time Setup (per client)

Each SEO client has a folder in [DELIVERY] space (`90182597483`) named `{SHORTCODE} - {Client Name}`. On first run, check for a **Reporting** list. If missing, create one:

- **List name:** `Reporting`
- **Parent:** Client's folder
- **Function:** `pd_clickup_create_list` with the client's folderId

## Monthly Task Creation

### Task Details

| Field | Value |
|-------|-------|
| **Name** | `SEO Report — {Month Year}` (e.g. "SEO Report — June 2026") |
| **Description** | Full internal report via `markdownDescription` |
| **Assignee** | Ehtisham (`48626346`) |
| **Status** | `in review` |
| **Priority** | Normal (3) |
| **Tags** | `seo-report`, `viktor` |

### Description Structure (order matters)

1. **Notable Wins** (top) — 3 wins marked for approval
2. **Full Internal Report** — all sections from `internal-report-spec.md`
3. **Proposed Client-Facing Report** (bottom) — exact content for the PDF, real data, positive framing. PM edits this directly.

### Approval Checklist

Add a checklist called "Report Approval":
- [ ] Internal report reviewed
- [ ] Notable wins approved for marketing
- [ ] Proposed client-facing content reviewed and edited
- [ ] Client-facing PDF approved for generation

All items must be ticked before generating the PDF.

## Post-Approval: PDF Generation

**Critical rule:** After approval, Step 7 MUST re-read the ClickUp task description via API (`pd_clickup_get_task`). Extract Section 11 (Proposed Client-Facing Report) including all PM edits. Generate the PDF from the re-read content only. Never generate from cached or in-memory data.

Upload the finished PDF to the ClickUp task as an attachment.

## Reporting List vs SEO List

- **Reporting list** — monthly reports only (`SEO Report — June 2026`, etc.)
- **SEO list** (or other work lists) — SEO tasks, content work, technical fixes

These are separate. Reports go in Reporting. Work tasks go in the client's other lists.

## Key IDs

| Resource | ID |
|----------|-----|
| Workspace | `308435` |
| [DELIVERY] space | `90182597483` |
| Viktor user ID | `113581164` |
| Ehtisham user ID | `48626346` |
| ClickUp urgent channel | `9d6k-176338` |

## ClickUp Formatting

- **Always use `markdownDescription`** (not `description`) for formatted content.
- Use standard markdown pipe tables — ClickUp auto-renders them.
- **Never pass `[table-embed:...]`** — that's ClickUp's internal output format, not an input.
- Use `@Viktor` in descriptions, not Slack user ID syntax (`<@U...>`).
