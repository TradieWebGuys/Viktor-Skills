---
name: twg-agency-blog-creation
description: >
  Write and publish blog posts for tradiewebguys.com.au — full workflow from ClickUp task to WordPress draft and scheduling with FAQ schema, feature image, and meta SEO. Use this skill whenever Amanda or the team asks to write a blog post, article, or content piece for Tradie Web Guys (TWG) the agency — including phrases like "write a TWG blog", "write a blog for Tradie Web Guys", "create a blog post for the TWG site", "write a post for tradiewebguys.com.au", or any request to produce content for the TWG agency website. Always use this skill — do not write TWG agency blogs from scratch without reading it first.
---

# TWG Blog Publishing Workflow

## When to Use

- Amanda or team requests a blog post from a ClickUp task
- Any mention of writing/publishing a blog for tradiewebguys.com.au
- Any request to "write a TWG blog", "write a blog for Tradie Web Guys", "create a post for the TWG site", or similar phrasing for the agency blog

## WordPress Credentials

- URL: `tradiewebguys.com.au`
- Username: `amanda@tradiewebguys.com.au`
- App password: stored in thread 1781683172.709199 in #agency-viktor
- API: `https://tradiewebguys.com.au/wp-json/wp/v2`
- Auth: Basic auth with base64-encoded `user:password`

## Google Drive Blog Folder

All completed blog posts must be saved to:
**Folder ID:** `1DzSm72B9fBmoM7Ll4CZUlDanXiLpbj-V`
**Link:** https://drive.google.com/drive/folders/1DzSm72B9fBmoM7Ll4CZUlDanXiLpbj-V

---

## Workflow Steps

### Step 0: Load Brand Context (MANDATORY — before writing anything)

- Pull `TradieWebGuys/Voice_Profile_Matt_Jones` README.md from GitHub (Matt's voice profile — 74KB)
- Pull `TradieWebGuys/Anti_AI_Writing_Guide_Matt_Jones_Edition` README.md from GitHub (anti-AI writing rules — 16KB)
- Load `company/references/brand-guide.md` (TWG brand guide)
- Apply all three as writing constraints throughout the blog
- Key rules: no AI-isms, use Matt's voice markers, follow the banned vocabulary list, em-dashes over semicolons, "pick a fight in the headline, teach in the body"

### Step 1: Read ClickUp Task

- Use `pd_clickup_proxy_get` to fetch task details
- Extract: topic, target LLM queries, writing guidelines, Google Doc link

### Step 2: Research

- Web search TWG website, reviews, podcast, relevant sources
- Pull specific numbers (review count, episode count, client results)
- Check existing blog posts on WordPress for cross-linking opportunities

### Step 3: Write Full Copy (Skip Draft Outline Stage)

- Go straight to final copy — no draft outline
- Minimum 2,500 words
- Brand voice: apply Voice Profile + Anti-AI Guide + brand guide (all loaded in Step 0)
- Q&A subheadings where applicable
- 5-8+ FAQ questions with answers at the end
- Cross-link to existing TWG blog posts (check WordPress for URLs)
- CTA: Impact Roadmap Session with link to `https://go.tradiewebguys.com.au/book`

### Step 4: Generate Feature Image

- Use `coworker_text2im` with `model="gpt-image-2"`, `aspect_ratio="3:2"`
- TWG brand colours: Primary Green #1F9C51, Navy Charcoal #1A1F2E, Warm Cream #F5F4F2, Lime Accent #8DC63F
- Australian context (hi-vis, Sydney landmarks, trade environments)
- Convert webp → PNG for WordPress upload
- LLM-optimised metadata: descriptive alt text with keywords, detailed description field

### Step 5: Create WordPress Draft

- Upload image via `/wp-json/wp/v2/media` with descriptive filename
- Set image alt_text, caption, title, description (all LLM-optimised)
- Create post via `/wp-json/wp/v2/posts` with status "draft"
- Common categories: Blog (22), Marketing (31), Business (34)
- Common tags: Marketing (26), Matt Jones (47), The Site Shed (62), tradie marketing (107), tradies (55), websites (108), SEO (27), Google Ads (25)
- Set featured_media to uploaded image ID
- Set excerpt with blog summary

### Step 6: Add FAQ Schema

- Build FAQPage JSON-LD schema from the FAQ section
- Append `<script type="application/ld+json">` to post content
- Verify schema is present after update

### Step 7: Set Meta SEO

- Try both Yoast REST API fields and standard post meta
- Note: Yoast fields may need manual confirmation in WP editor depending on site config

### Step 8: Save to Google Drive

- Save the final blog content as a Google Doc in the TWG Blog folder
- Folder ID: `1DzSm72B9fBmoM7Ll4CZUlDanXiLpbj-V`
- Use `gdrive_2_gdrive_google_docs_write` with `position="replace"` if updating an existing doc, or create a new doc in the folder
- File name format: `YYYY-MM-DD — [Blog Title]`
- Include the full blog copy (all headings, body, FAQs, CTA)

### Step 9: Update Google Doc (ClickUp-linked doc)

- Use `gdrive_2_gdrive_google_docs_write` with `position="replace"`

### Step 10: Update ClickUp

- Add completion comment via `pd_clickup_proxy_post` to task comment endpoint
- Include WordPress edit URL and summary of what was done

### Step 11: Scheduling

- Default: leave as draft unless told otherwise
- If asked to schedule: use `date` field in post update (ISO 8601 format) with `status: "future"`
- If "after last scheduled post": query recent posts with status=future to find the latest, then add 7 days

---

## Guardrails

- Output is a WordPress draft for Amanda or the team to review before publishing. Do not publish (change status from "draft") without explicit approval.
- Step 0 (loading voice profile, anti-AI guide, and brand guide) is mandatory before writing anything. Skipping it produces off-brand copy.
- Pause on missing inputs. If the ClickUp task ID or topic is not provided, ask rather than guessing.
- Never fabricate stats, client results, or review counts. If a data point cannot be verified, leave it out or flag it for confirmation.
- WordPress username is the full email address, not just "amanda".
- Image must be converted from webp to PNG before WordPress upload.
- Always verify FAQ schema is present after adding it.
- Yoast meta via REST API may not stick — note this to the user.
- Always save the final blog to the Google Drive folder (Step 8) before closing out the task.
- Writing: apply Voice Profile + Anti-AI Guide + brand guide. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).
