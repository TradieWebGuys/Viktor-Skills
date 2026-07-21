# ClickUp v3 Docs API Reference

All endpoints use the ClickUp v3 API via `pd_clickup_proxy_*` helpers. The workspace ID is `308435`.

**Base URL:** `https://api.clickup.com/api/v3/workspaces/308435`

## Read Operations

### List docs in a folder

```python
from sdk.tools.pd_clickup import pd_clickup_proxy_get

result = await pd_clickup_proxy_get(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs",
    query_params={"parent_id": "{folder_id}", "parent_type": "5"}
)
# parent_type: 5 = folder, 6 = list, 1 = doc (nested)
# Returns: {"docs": [{"id": "9d6k-...", "name": "...", "parent": {"id": "...", "type": 5}}]}
```

### Get a single doc

```python
result = await pd_clickup_proxy_get(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}"
)
# Returns: {"id": "9d6k-...", "name": "...", "parent": {...}, "workspace_id": 308435, "type": 1}
```

### List pages in a doc

```python
result = await pd_clickup_proxy_get(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}/pages",
    query_params={"max_pages": "100"}
)
# Returns: [{"id": "9d6k-...", "name": "...", "parent_page_id": null or "9d6k-...", "content": "..."}]
```

Pages with `parent_page_id: null` are top-level. Pages with a `parent_page_id` are nested under that parent page.

### Get a single page (full content)

```python
result = await pd_clickup_proxy_get(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}/pages/{page_id}"
)
# Returns: {"id": "...", "name": "...", "content": "markdown content...", ...}
```

## Write Operations

All write operations create drafts requiring user approval before execution.

### Create a new page

```python
from sdk.tools.pd_clickup import pd_clickup_proxy_post

result = await pd_clickup_proxy_post(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}/pages",
    json_body={
        "name": "Page Title",
        "content": "Markdown content goes here",
        "parent_page_id": "{parent_page_id}"  # omit for top-level page
    }
)
# Returns a draft_id for approval
```

### Update an existing page

```python
from sdk.tools.pd_clickup import pd_clickup_proxy_put

result = await pd_clickup_proxy_put(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}/pages/{page_id}",
    json_body={
        "content": "Updated markdown content",
        "content_edit_mode": "replace"  # replaces full content; use "append" to add to end
    }
)
# Returns a draft_id for approval
```

**Important:** When using `content_edit_mode: "replace"`, you must include the entire page content, not just the changes. To preserve existing content, read the page first, merge your changes, then write back the full content.

To append content without overwriting:

```python
result = await pd_clickup_proxy_put(
    url="https://api.clickup.com/api/v3/workspaces/308435/docs/{doc_id}/pages/{page_id}",
    json_body={
        "content": "\n\n## New Section\nAppended content here",
        "content_edit_mode": "append"
    }
)
```

## Response Handling

All proxy responses have this structure:

```python
result = {
    "response_role": "general",
    "content": '{"status_code": 200, "body": {...}}'  # JSON string
}
```

Parse the response:

```python
import json
response = json.loads(result['content'])
body = response.get('body', response)
```

For write operations, the response contains a draft_id instead of the API response. Submit the draft for approval.

## Known Patterns

### Client Doc Structure

Each client folder (type 5) in the [DELIVERY] space typically contains:

- **{SC} - Project Hub** doc — main client workspace with sub-pages:
  - Main page (assets, plan, important links)
  - Roadmap page (business overview, goals, milestone table)
  - Meetings page (where meeting notes are filed)
  - Other pages vary by client

- **{SC} - Client Profile** doc — client details with sub-pages:
  - Client Profile page
  - Client Meeting Notes page (some clients use this instead of Project Hub Meetings)
  - SEO Goals Sheet (if applicable)

### Finding the Right Meetings Page

Not all clients have the same page names. Search for meetings pages in this priority order:

1. "Meetings" in the Project Hub doc
2. "Client Impact Meetings" in the Project Hub doc
3. "Client Meeting Notes" in the Client Profile doc

If none exist, create a "Meetings" page in the Project Hub doc (or Client Profile if no Project Hub exists).

### Doc ID Format

ClickUp doc and page IDs follow the format `{workspace_prefix}-{number}` (e.g., `9d6k-225178`). These IDs are stable and can be used in URLs: `https://app.clickup.com/308435/v/dc/{doc_id}`.

### Folder Lookup

To find a client's folder by shortcode, get all folders in the [DELIVERY] space:

```python
result = await pd_clickup_proxy_get(
    url="https://api.clickup.com/api/v2/space/90182597483/folder"
)
# Parse response, find folder where name starts with "{SHORTCODE} - "
```
