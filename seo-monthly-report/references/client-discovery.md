# Client Discovery

How to determine which clients to include in the monthly SEO report.

## Source of Truth

The ClickUp **Account Health Tracker** (list ID: `901804854897`) is the master client roster. Use the **SEO clients view** (ID: `9d6k-264358`) to get active SEO clients.

**API call:** `GET https://api.clickup.com/api/v2/view/9d6k-264358/task?page=0`

## Filtering Logic

1. Fetch all tasks from the SEO view.
2. For each task, read the `🤝 Services` custom field (labels, ID: `9abef61f-56a5-4756-ac79-af1060af4856`).
3. Include the client only if services contain `SEO` AND `Status` = `Active`.
4. Read the `⭐ Shortcode` custom field for the 3-letter code.
5. Cross-reference against `references/account-mapping.md` for data source IDs.

## Setup Check

Beyond the ClickUp roster, each client must have a complete setup to be reported on:

| Check | Path | Skip reason if missing |
|-------|------|----------------------|
| Client KB | `skills/clients/{shortcode}/SKILL.md` | "No Client KB — run onboarding first" |
| STATE.md | `skills/clients/{shortcode}/seo/STATE.md` | "No STATE.md — run initial baseline first" |
| Strategy doc | Link in STATE.md | "No strategy doc — create strategy first" |
| Account mapping | `references/account_mapping.json` | "No data source IDs mapped" |

If any check fails, skip the client and include the reason in the Slack summary.

## Finding Client ClickUp Folders

Each client has a folder in [DELIVERY] space (`90182597483`) named `{SHORTCODE} - {Client Name}`. Use the shortcode to locate the correct folder for creating the Reporting list and tasks.

## Key IDs

| Resource | ID |
|----------|-----|
| Workspace | `308435` |
| [DELIVERY] space | `90182597483` |
| Account Health Tracker list | `901804854897` |
| SEO clients view | `9d6k-264358` |
| Services field | `9abef61f-56a5-4756-ac79-af1060af4856` |
