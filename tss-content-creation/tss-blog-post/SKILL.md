---
name: tss-blog-post
description: Write and prepare a WordPress blog post for a The Site Shed podcast episode. Use this skill whenever a blog post needs to be written or published for a TSS podcast episode. Triggers on: "write blog post", "blog for episode", "WordPress blog", "publish to blog", or any request to produce blog content for thesiteshed.com. Always use this skill — do not write TSS blog posts from scratch without reading this first.
---

# The Site Shed — Podcast Blog Post Generator

Write a complete, SEO-optimised blog post for a podcast episode, plus all metadata and publishing instructions for WordPress.

## Inputs

| Input | Required? | Source |
|---|---|---|
| Episode number + title | Required | Provided by user or framework doc |
| Guest name + company | Framework doc |
| YouTube link | Provided by user (stored in ACF field `youtube_video_link`) |
| Air date | Provided by user |
| Transcript | Riverside transcript from Google Drive (primary), or YouTube captions via YouTube Data API for scheduled/private videos, or ElevenLabs transcription of audio file (fallback) |
| Focus keyword(s) | Research based on episode topic — aim for trade business search intent |
| Approved show notes summary | Reuse if already written |
| Buzzsprout episode ID | Inferred | Fetch via Buzzsprout API (see below) |

Missing-input handling: if the episode number, guest name, YouTube link, or air date is not provided, pause and ask. Do not guess. If a transcript is unavailable from any source, say so — do not fabricate quotes or content.

## Guardrails

- Output is a draft for the team to review before publishing to WordPress. This skill does not publish content directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate quotes, stats, or details not found in the transcript or source material.
- If the Buzzsprout episode cannot be found, note the gap and deliver the rest of the content.
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Fetching the Buzzsprout embed code

The embed code can be constructed automatically using the Buzzsprout API. Do this before writing the post.

**Podcast ID (static):** `2198439`
**API endpoint:** `GET https://www.buzzsprout.com/api/2198439/episodes.json`
**Auth:** `Authorization: Token token={api_token}`

Steps:
1. Call the episodes endpoint
2. Find the episode by matching `episode_number` or `title`
3. Grab the `id` field (e.g. `19405280`)
4. Slugify the Buzzsprout episode title using these exact rules:
   - Lowercase everything
   - Remove: `|` `%` `(` `)` `.`
   - Replace apostrophes `'` with hyphens (e.g. "It's" → "it-s")
   - Replace spaces with hyphens
   - Collapse multiple consecutive hyphens into one
5. Construct the embed code:

```html
<div id="buzzsprout-player-{id}"></div>
<script src="https://www.buzzsprout.com/2198439/episodes/{id}-{title-slug}.js?container_id=buzzsprout-player-{id}&player=small" type="text/javascript" charset="utf-8"></script>
```

**Example (Ep. 505):**
```html
<div id="buzzsprout-player-19405280"></div>
<script src="https://www.buzzsprout.com/2198439/episodes/19405280-why-60-of-business-transitions-fail-and-it-s-not-the-tax-strategy-ft-andrea-carpenter-ep-505.js?container_id=buzzsprout-player-19405280&player=small" type="text/javascript" charset="utf-8"></script>
```

Insert the constructed embed code in the blog output where the Buzzsprout placeholder appears.

## Step 1 — Keyword research

Before writing, identify the primary focus keyword and 2–3 secondary keywords. The keyword should reflect:
- What a trade business owner would search for
- The core topic of the episode (not just the guest's name)
- A realistic search volume opportunity (specific > broad)

Examples:
- "business succession planning for tradies"
- "how to sell a trade business"
- "exit strategy for trade business owners"

Use the focus keyword naturally in: the title, first paragraph, at least one subheading, and the meta description.

## Step 2 — Research internal links

Before writing, search thesiteshed.com for related content to interlink within the post.

Use web search: `site:thesiteshed.com [topic keyword]`

Find 2–4 relevant existing posts or episodes that relate to the episode topic. These will be linked naturally within the blog content — not listed at the end, but woven into the body where contextually relevant.

Example: for a business transitions episode, search for existing TSS content on exit strategy, business valuation, or succession planning, then link to those posts where the topic is mentioned.

If the guest has a relevant website or resource that was mentioned in the episode, link to it in the content where contextually appropriate (not just in the guest bio section).

## Step 3 — Determine category and tags

**Category — always select two:**
1. `Podcast` ← ALWAYS included, no exceptions
2. One additional category based on episode content:

| Category | When to use |
|---|---|
| HR | Hiring, team, staff, training, onboarding, retention |
| Sales | Pricing, quoting, conversion, client relationships, service agreements |
| Marketing | Lead generation, SEO, social media, branding, ads, content |
| Strategic Planning & Development | Business growth, exit strategy, succession, selling business, mindset, goals |
| Finance | Cash flow, tax, accounting, margins, invoicing, P&L |
| Systems | Automation, job management, processes, project management, SOPs |
| Health | Mental health, wellbeing, OH&S, ergonomics, injury prevention |
| Feature | Non-evergreen content, timely topics that will date |
| Success Story | "A to B" journey episodes — guest shares their transformation |

**Tags — select all that apply from this list:**

HR tags: Customer Service, Firing, Hiring, Incentives, KPIs, Meetings, Onboarding, Organisation, Org Chart, Outsourcing, Productivity, Recruitment, Retention, Staff, Staffing, Team, Training

Sales tags: Client, Coaching, Cold Calling, Customer, Database, Discounts, Flatrate pricing, Rebooking, Re-Engaging Customers, Service Agreements

Marketing tags: Adwords, Automation, Branding, Content Creation, Copywriting, Customer Experience, Email marketing, Facebook, Funnels, Google Ads, Google Apps, Google Drive, Instagram, Lead Generation, Lead nurturing, Leads, LinkedIn, Membership Programs, Memberships, Networking, Outsourcing, Referral Marketing, Referrals, Reviews, SEO, Social Media, Video, Vlog, Vlogging, Youtube

Strategic Planning & Development tags: Acquisition, Coaching, Courses, Database, Goals, Goal Setting, Growth, Insurance, Intellectual Property, IP, Meetings, Mindset, Patents, PR, Productivity, Selling Business, Trademark, Training, Valuation

Finance tags: Bookkeeping, Accounting, Accountant, Xero, MYOB, Invoicing, Tracking Costs, Systems, Budget, Cashflow, Expenses, Finance Options, Margins, P&L, Profit and Loss, Money Management, Reporting, Tax, Turnover

Systems tags: Automation, Job Management, Metric Tracking, Organisation, Org Chart, Productivity, Project Management, Reporting, Time Management, Tracking Costs

Health tags: Ergonomics, Injury Prevention, Meditation, Mental Health, OH&S, Wellbeing

No limit on tags. Add anything not on this list that accurately describes the episode.

## Step 4 — Write the blog post

### Title (WordPress post title)

**[###] - [Title] | ft. [Guest Name]**

Example: `505 - Why 60% of Business Transitions Fail (And It's Not the Tax Strategy) | ft. Andrea Carpenter`

This is the post title only — it differs from the SEO/meta title.

### SEO title (RankMath)

Should include the focus keyword. Can differ from the post title. Max 60 characters.

Example: `Business Transition Planning for Trade Business Owners | Ep. 505`

### Slug

Lowercase, hyphens only, focus keyword prominent. Finished with `ep-###`.
Example: `business-transition-planning-trade-business-owners-ep-507`

### Meta description (RankMath)

1–2 sentences. Include focus keyword. Summarise what the reader gets from the post. Max 155 characters.

### Blog post content structure

Write a full SEO article — not just show notes. Aim for 800–1,200 words. Use the transcript as the primary source.

```
[INTRO — 2–3 paragraphs]
Hook: open with the problem or tension the episode addresses.
Introduce Matt and the guest (name, company, relevance to trade business owners).
Tell the reader what they'll get from reading/listening.
Include focus keyword naturally in the first paragraph.

[YOUTUBE EMBED PLACEHOLDER]
<!-- ACF field: youtube_video_link -->

[SECTION 1: Main topic/framework — H5 subheading]
[150–200 words]
Link to guest website if relevant context exists.
Link to related TSS content where topic is mentioned.

[SECTION 2: Key insight or turning point — H5 subheading]
[150–200 words]
Link to related TSS content where topic is mentioned.

[SECTION 3: Practical application or advice — H5 subheading]
[150–200 words]

[SECTION 4: Additional key point if warranted — H5 subheading]
[100–150 words]

[BUZZSPROUT EMBED PLACEHOLDER]
<!-- Buzzsprout audio embed code goes here -->

[KEY TAKEAWAYS — H5 subheading]
3–5 dot points. Specific and actionable — not generic summaries.

[CLOSING CTA — 1–2 paragraphs]
Direct the reader to listen to the full episode or book a call.
Include: 🫱🏻‍🫲🏼 Book a Free Strategy Call: https://tradie.wiki/tssyt
```

### Writing rules

- Matt's voice: direct, specific, experience-grounded, Australian English
- No em dashes
- Subheadings use H5 (Heading 5 in Elementor)
- Specific over vague — use real concepts, frameworks, and numbers from the transcript
- Don't repeat the episode title verbatim in the intro
- Don't start with "In this episode..." or "Today we're talking about..."
- Focus keyword appears in: intro paragraph, at least one H5, meta description
- Internal links: woven naturally into body copy, not listed or forced
- Guest website: link in body copy where contextually relevant, not just in bio

## Output format

Deliver everything in one block:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BLOG METADATA
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Post Title: [###] - [Title] | ft. [Guest Name]
SEO Title (RankMath): [focus keyword-optimised, max 60 chars]
Slug: [lowercase-hyphenated-focus-keyword-ep-###]
Meta Description (RankMath): [max 155 chars, includes focus keyword]
Focus Keyword: [primary keyword]

Categories: Podcast | [Additional category]
Tags: [comma-separated list]

Comments: OFF

Featured Image: Use episode thumbnail from Canva — filename: TSS[###]-thumbnail
Schedule: [air date, align with YouTube publish time]
ACF Field — youtube_video_link: [YouTube URL]
Buzzsprout Embed: [constructed embed code]

Internal links used:
- [URL] — [anchor text / context]
- [URL] — [anchor text / context]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BLOG POST CONTENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[full article as per structure above]
```

## WordPress publishing checklist

Once the content is ready, the person publishing follows these steps:

1. Clone a recent published podcast post in WordPress → Posts → Clone
2. Open the draft → update **Post Title** and **Permalink** → Save Draft
3. Update ACF field **`youtube_video_link`** with the YouTube URL → Save Draft
4. Scroll to **RankMath SEO** → paste **SEO Title**, confirm **Slug**, paste **Meta Description**, set **Focus Keyword** → Save Draft
5. Set **Featured Image** (upload episode thumbnail from Canva) → Save Draft
6. Apply **Categories** (Podcast + additional) and **Tags** → Save Draft
7. Turn **Comments OFF** in the Discussion settings for the post → Save Draft
8. Click **Edit with Elementor**:
   - YouTube embed auto-loads from the ACF field — confirm it loads
   - Paste the Buzzsprout embed code into the HTML element
   - Paste blog post content into the text editor
   - Format subheadings as **Heading 5**
   - Verify internal links are live and correct
   - Preview before saving
9. Exit to WordPress → set **Publish date** to align with YouTube air date → Schedule

**Final checks before scheduling:**
- [ ] Post title matches episode format (`### - Title | ft. Guest`)
- [ ] RankMath: SEO title, slug, meta description, focus keyword complete
- [ ] ACF field `youtube_video_link` populated
- [ ] Featured image set
- [ ] YouTube and Buzzsprout embeds working
- [ ] Categories: Podcast + one additional
- [ ] Tags applied
- [ ] Comments: OFF
- [ ] Internal links verified
- [ ] Formatting consistent (H5 subheadings, no leftover content from cloned post)
- [ ] Post is **Scheduled**, not Published immediately
