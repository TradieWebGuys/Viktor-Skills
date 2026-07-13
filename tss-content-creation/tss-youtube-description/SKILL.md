---
name: tss-youtube-description
description: Generate the YouTube title, description, playlist tags, and scheduler notes for a full The Site Shed podcast episode upload. Use this skill whenever a YouTube description or video metadata needs to be written for a Site Shed episode. Triggers on: "write YouTube description", "YouTube upload", "YouTube metadata", "schedule YouTube episode", or any request to prepare a full episode for YouTube. Always use this skill — do not write YouTube descriptions from scratch without reading this first.
---

# The Site Shed — YouTube Description Generator

Generate a complete YouTube title, description, and scheduler metadata for a full podcast episode upload.

## Inputs

| Input | Required? | Source |
|---|---|---|
| Episode number | Required | Provided by user |
| Guest name | Framework doc |
| YouTube link | Provided by user |
| Air date | Provided by user |
| Raw transcript | Riverside transcript from Google Drive — used for summary, bio, and content (NOT for timestamps) |
| Edited video captions | YouTube Data API captions from the uploaded edited video — used for KEY CHAPTERS timestamps only. Works on private/scheduled videos via OAuth. |
| Framework/booking doc | Google Drive folder for the episode |
| Approved summary | Inferred | From show notes (reuse if already written) |
| KEY CHAPTERS | Inferred | From show notes (reuse if already written) |

Missing-input handling: if the episode number, guest name, YouTube link, or air date is not provided, pause and ask. Do not guess. If a transcript is unavailable, say so — do not fabricate content.

## Guardrails

- Output is a draft for the team to review before uploading to YouTube. This skill does not publish content directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate quotes, stats, or details not found in the transcript or framework doc.
- If edited video captions are unavailable for timestamps, write all other sections first and note the gap.
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Step 1 — Determine the YouTube title

Use the Content Angle Decision Matrix to identify the correct angle:
📄 `skills/tss-content-angle-matrix.md`

Write a concise, clickworthy title that fits the angle, then apply the naming convention:

**[Clickworthy Title] | ft. [Guest Name] | Ep. [###]**

## Step 2 — Thumbnail text

Brainstorm 3–5 thumbnail text options (3–4 words, max 5). The thumbnail text and the video title work as a pair — they must not repeat the same key words, stats, or phrases.

Rules:
- If the title contains a stat (e.g. "60%"), do not use that stat in the thumbnail text
- If the title names the outcome (e.g. "Business Transitions Fail"), the thumbnail should focus on the emotional hook or personal challenge instead
- Fear/loss aversion outperforms aspiration — "Your X Will Fail" consistently outperforms "Achieve Your X"
- Use "Your" or "You" where possible — personal address drives highest CTR
- The thumbnail should make someone stop scrolling; the title should confirm the click was right

Rank the options and recommend one, explaining why it will outperform the others.

Output format:
```
THUMBNAIL TEXT OPTIONS:
1. [option] ← Recommended
2. [option]
3. [option]

Why #1 wins: [1–2 sentences on CTR reasoning]
```

The YouTube title should be punchy and front-loaded. Aim for the core hook in the first 60 characters. The `| ft. [Guest Name] | Ep. [###]` portion trails at the end.

Examples:
- `The Real Reason Business Transitions Fail | ft. Andrea Carpenter | Ep. 505`
- `Why Most Tradies Undercharge (And How to Fix It) | ft. Jane Smith | Ep. 488`

## Step 3 — Select playlists

Every full episode gets added to **two or more** playlists:

**Always include:**
- The Site Shed Podcast | Systems, Strategy and Growth for Tradies and Contractors

**Then select all topic playlists that apply:**

| Playlist | Use when the episode covers... |
|---|---|
| Leadership & Management | Leadership, team management, delegation, culture, hiring, accountability |
| AI & Technology | AI tools, software, automation, tech adoption, digital transformation |
| Finance | Business finances, pricing, exit strategy, business transitions, succession, selling a business, tax, cash flow |
| Operations & Systems | Business systems, processes, workflows, operations, SOPs, scaling |
| Sales | Sales process, quoting, conversion, follow-up, lead qualification, closing |
| Success Stories | Non-TWG client stories — tradies or contractors sharing their journey or results |
| Marketing Case Studies - Tradie Web Guys | TWG client success stories with marketing results |
| Marketing | Marketing strategy, SEO, social media, advertising, content, brand |
| Safety & Compliance | WHS, safety, licensing, compliance, insurance, legal obligations |

Select 1–2 topic playlists per episode. If genuinely cross-category, include up to 3.

## Step 4 — Write the description

Produce the description in this exact order:

---

🎯 Free Tools for Growing Trade Businesses: https://tradie.wiki/pod
🫱🏻‍🫲🏼 Book a Free Strategy Call with Tradie Web Guys: https://tradie.wiki/tssyt

[SUMMARY — 2 paragraphs. Reuse from show notes if already written. Same voice and style rules apply.]

KEY CHAPTERS
00:00 - Introduction
[MM:SS] - [Chapter Title]
...
[MM:SS] - Closing Remarks and Resources

About the Guest: [First Last]
[Bio paragraph — same as show notes]

[Include all available guest links from the framework doc in this order:]
Website: [guest website]
[Free resource link if mentioned in the episode]
LinkedIn: [guest LinkedIn]
Instagram: [guest Instagram URL — if available]
Facebook: [guest Facebook URL — if available]
YouTube: [guest YouTube channel — if available]

CONNECT WITH THE SITE SHED!
Website: https://www.thesiteshed.com
YouTube: https://www.youtube.com/@TheSiteShed?sub_confirmation=1
Facebook: https://www.facebook.com/thesiteshed
Instagram: https://www.instagram.com/thesiteshed/
LinkedIn: https://www.linkedin.com/company/the-site-shed/
Matt's LinkedIn: https://www.linkedin.com/in/iamthemattj/

CONNECT WITH THE TRADIE WEB GUYS!
Website: https://www.tradiewebguys.com.au/
YouTube: https://www.youtube.com/@TradieWebGuysOfficial?sub_confirmation=1
Facebook: https://www.facebook.com/TradieWebGuysOfficial
Instagram: https://www.instagram.com/tradiewebguys/
LinkedIn: https://au.linkedin.com/company/tradie-web-guys
Matt's LinkedIn: https://www.linkedin.com/in/iamthemattj/

If you enjoyed this podcast, please take a moment to leave us a review:
⭐ https://lovethepodcast.com/TheSiteShed

Love the audio version of this podcast? Subscribe to the link below:
⭐ https://followthepodcast.com/TheSiteShed

#podcast #thesiteshed #tradiewebguys [topic hashtags]

---

## Output format

Deliver the full output in this structure so it's ready to copy into YouTube Studio:

```
YOUTUBE TITLE:
[Clickworthy Title] | ft. [Guest Name] | Ep. [###]

PLAYLISTS:
- The Site Shed Podcast | Systems, Strategy and Growth for Tradies and Contractors
- [Topic playlist(s)]

MADE FOR KIDS: No

TAGGING NOTES:
[List every platform where the guest can be tagged, with their handle. Only include platforms where they have a confirmed presence from the framework doc.]
YouTube: @[handle] (if they have a YouTube channel)
Instagram: @[handle] (if available)
Facebook: @[page name or handle] (if available)

---

DESCRIPTION:
[full description as above]
```

The TAGGING NOTES section is for the person scheduling the video — it tells them who to tag in the description or pinned comment on each platform. If the guest has no taggable presence on a platform, omit that line.

## Summary writing rules

- Reuse the approved show notes summary if it has already been written for this episode
- If writing fresh: two paragraphs, Matt's voice, Australian English, no em dashes
- Never start with "In this episode..." or "Today we're talking about..."
- Open with the listener's problem or a punchy hook
- Name Matt and the guest in the first or second sentence: "Matt Jones sits down with [Guest] from [Company]"
- Do not include the YouTube watch link (the viewer is already on YouTube)

## What NOT to include

- The 🎥 YouTube watch link (show notes only)
- A single CTA — YouTube always gets BOTH (Free Tools + Strategy Call)
- Guest socials other than LinkedIn
- Guest website unless it's a specific resource mentioned in the episode
- Any section headers or labels beyond what is shown in the output format
- "Made for kids: Yes" — always No
