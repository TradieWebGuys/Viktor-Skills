---
name: content_register
description: "Crawl a client website and produce a 3-tab Content Register Google Sheet (Published Content, Content Pipeline, Strategy & Notes). Use when someone says \"create a content register\", \"build the content register for [client]\", \"crawl the site and list the pages\", \"audit what content [client] has\", or when onboarding a new SEO client or auditing existing site content."
---

# Content Register

Crawl a client website's sitemap, scrape every page, classify content, and produce a formatted Google Sheet in their Drive folder.

## Trigger Prompt

```
@Viktor Create a Content Register for [CLIENT NAME].
Website: [URL]
Trade: [trade type]
Primary location: [location]
Service area: [service area description]
Google Drive folder: [folder link]
```

## Inputs

- **Client name** (required) — the TWG client name or code.
- **Website URL** (required) — the client's website domain.
- **Trade type** (required) — the type of trade business.
- **Primary location** (required) — main service area.
- **Service area** (recommended) — broader service area description.
- **Google Drive folder** (required) — link or ID for the client's folder where the sheet will be saved.

Missing-input handling: if the website URL or Google Drive folder is not provided, pause and ask. Do not guess URLs or create sheets in arbitrary locations.

## Guardrails

- Output is a draft Google Sheet for the project manager to review. It does not publish or update any website content.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate page data. If a page cannot be scraped (error, timeout), log it and skip rather than estimating content.
- Scrape at a maximum of 10 concurrent connections to avoid rate limiting the client's site.
- Keep client-specific data inside the sheet only — not in anything shared externally.

## Workflow

### Step 1 — Crawl Sitemap
- Fetch `sitemap_index.xml` → nested sitemaps → collect all URLs
- Fallback: try `/sitemap.xml`, `/wp-sitemap.xml`

### Step 2 — Scrape Pages
- Batch scrape all URLs (async, 10 concurrent max)
- Extract: title, H1, meta description, word count, headings, schema, published/modified dates, author
- WordPress/Elementor sites: extract content from `[data-elementor-type]` containers, not `<article>` tags
- Site-wide form headings (e.g. "Get Started Form") appear inside Elementor content areas — strip these before word counting

### Step 3 — Classify & Build CSV
- Page types: Homepage, Core Page, Service Page, Location Page, Blog, Product Page, CTA/Landing Page, etc.
- Extract: primary keyword (estimated from URL + title), target location, topic tags
- Quality flags: thin content (<1000w for blogs), missing H1, low heading count
- Detect topic overlaps (same topic × same location = potential cannibalisation)
- Classify based on URL structure, not content headings

### Step 4 — Create Google Sheet (3 tabs)

**Tab 1 — Published Content**
| Column | Description |
|--------|-------------|
| Title | Page title |
| Type | Core Page / Service Page / Location Page / Blog / Product Page / CTA / etc. |
| URL | Full URL |
| Primary Keyword (est.) | Estimated target keyword from URL slug + title |
| Location | Target location if applicable |
| Word Count | Content word count |
| H2/H3 Count | Number of subheadings |
| Published Date | From meta or sitemap |
| Has FAQ Schema | Yes/No |
| Quality Flags | Thin content, missing H1, low headings, etc. |
| Notes | Empty for manual notes |

**Tab 2 — Content Pipeline**
Empty template with headers:
Topic, Type, Target Keywords, Location, Priority, Status, Due Date, Publish Date, ClickUp Task Link, Notes

**Tab 3 — Strategy & Notes**
Pre-filled where possible:
- CLIENT, SHORTCODE, WEBSITE, TRADE, PRIMARY LOCATION, SERVICE AREA
- CONTENT PILLARS (derived from service pages found)
- LOCATION PRIORITIES (derived from location pages found)
- COMPETITORS (blank — needs manual input)
- SEO STRATEGY NOTES (blank)
- CONTENT RULES (Write in Australian English, refer to business as [name])

### Step 5 — Format & Upload
- Header row: bold, blue background, white text, frozen
- Auto-resize columns
- Move to client's Google Drive folder
- Share link in Slack

## Reference Sheets

- ATS example (gold standard format): `https://docs.google.com/spreadsheets/d/1K8p0pYRh6FMH2KDIQ5ehddo1OIlbGagxq7cyIG-gCIo/edit`
- TWG audit: `https://docs.google.com/spreadsheets/d/1YNBooodC25rPzciSFg9Vol7sYxyLBIjU-FM0ZJzInCg/edit`
