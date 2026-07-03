# Client Discovery

How to determine which clients to include in the monthly SEO report.

## Source of truth

The ClickUp **Account Health Tracker** (list ID: `901804854897`) is the single source of truth. Use the "Active Accounts by AM" view (ID: `9d6k-155558`) to get the current roster.

- **API endpoint**: `GET https://api.clickup.com/api/v2/view/9d6k-155558/task?page=0`

## Filtering logic

1. Fetch all tasks from the view.
2. For each task, read the `🤝 Services` custom field (type: labels, ID: `9abef61f-56a5-4756-ac79-af1060af4856`).
3. Include the client if their services contain `SEO`.
4. Also check the `Status` custom field — only include clients set to `Active`.
5. Read the `⭐ Shortcode` custom field to get the client's three-letter code.
6. Cross-reference the shortcode against `references/account-mapping.md` to resolve data source IDs.

## When a client is missing from the mapping

If a client appears in the ClickUp view with an SEO service tag but has no matching entry in the account mapping:

- Skip them.
- Log a warning: `"[SKIP] {Client Name} ({shortcode}) — no data source IDs in account mapping"`
- Include this warning in the Slack summary under a "⚠️ Missing account mappings" section.

## Finding client ClickUp folders

Each client has a folder in the [DELIVERY] space (ID: `90182597483`) named `{SHORTCODE} - {Client Name}`. Use the shortcode to locate the correct folder for creating the Reporting list and tasks.
