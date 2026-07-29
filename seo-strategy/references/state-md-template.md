# STATE.md Template

Location: `skills/clients/{shortcode}/seo/STATE.md`

This is Viktor's rolling working memory for a client's SEO program. Updated monthly by the reporting cron. Read by the strategy skill at quarterly review. Contains links to all artifacts — no data duplication.

---

```markdown
# SEO State — {Client Name} ({SHORTCODE})

_Last updated: {YYYY-MM-DD}_

## Current Block

| Field | Value |
|---|---|
| Block | {N} |
| Cluster | {e.g. Hot Water} |
| Start date | {YYYY-MM-DD} |
| End date (projected) | {YYYY-MM-DD} |
| Entry path | {TWG build / Non-TWG / Existing client} |
| Foundation gate | {Complete / In progress — week X} |
| Current pace | {e.g. 2/week / Ramping — 1/week} |

## Artifact Links

| Artifact | Link |
|---|---|
| Client KB | `skills/clients/{shortcode}/SKILL.md` |
| Strategy doc — current block | {ClickUp page URL or page ID} |
| Keyword research sheet | {Google Sheet URL} |
| Content register | {Google Sheet URL} |
| Latest DataForSEO audit | {Date run + any saved report path} |
| Project Hub doc | {ClickUp doc ID} |
| Roadmap Timeline page | {ClickUp page ID} |
| Current Focus page | {ClickUp page ID} |

## Latest Metrics ({Month YYYY})

| Metric | Value | Change (MoM) | Block start baseline |
|---|---|---|---|
| Keywords ranking | | | |
| Page-one rankings | | | |
| Estimated monthly traffic | | | |
| Traffic value | | | |
| Technical health score | | | |
| Referring domains | | | |
| Domain rank | | | |

## AI/LLM Visibility

| Keyword | AI Overview present | Client cited | Last checked |
|---|---|---|---|
| {head keyword 1} | {Yes/No} | {Yes/No} | {YYYY-MM-DD} |
| {head keyword 2} | {Yes/No} | {Yes/No} | {YYYY-MM-DD} |

## Content Published This Block

| Week | Date | Type | Page / Topic | Target Keyword | Status |
|---|---|---|---|---|---|
| 1 | {date} | {service/location/blog} | {title} | {keyword} | {Published / Drafted / Skipped} |

## Rewrites This Block

| Date | Page | What changed | Result |
|---|---|---|---|
| {date} | {URL} | {e.g. expanded thin content, merged duplicates} | {e.g. moved from #18 to #9} |

## Block Goals Progress

| Goal | Status | Evidence |
|---|---|---|
| {Goal from Section 7} | {On track / At risk / Met / Not met} | {specific data} |

## Monthly Snapshots (rolling history)

### {Month YYYY}
- Traffic: {N} sessions ({+/-X% MoM})
- Page-one keywords: {N} ({+/-X})
- Content published: {N} new, {N} rewrites
- Key win: {one-line highlight}
- Flag: {any issue or concern}
- Report link: {URL or path}

### {Previous Month YYYY}
- ...

## Strategy Doc History

| Block | Period | Page ID | Cluster |
|---|---|---|---|
| 1 | {Mon–Mon YYYY} | {ClickUp page ID} | {e.g. Hot Water} |

## Notes

{Anything the next run needs to know — PM decisions, client requests, paused work, upcoming seasonal windows, etc.}
```

---

## Update Rules

1. **Monthly report cron** updates: Latest Metrics, Content Published, Block Goals Progress, Monthly Snapshots, Notes
2. **Strategy skill (quarterly)** updates: Current Block (new block info), Artifact Links (if changed), archives old snapshots
3. **Content scheduler** updates: Content Published rows as tasks are created
4. **KB update** may trigger a note in Notes if services/locations changed mid-block

## What STATE.md is NOT

- Not a duplicate of the strategy doc — it links to it
- Not a duplicate of the keyword sheet — it links to it
- Not a reporting dashboard — it's operational context for Viktor
- Not visible to clients — internal only
