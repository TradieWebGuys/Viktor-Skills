---
name: tss-buzzsprout-shownotes
description: Generate complete show notes for The Site Shed podcast audio episodes. Use this skill whenever show notes need to be written for a podcast episode. Triggers on: "write show notes", "create show notes", "draft show notes", "show notes for episode", or any request to produce the description/notes for a Site Shed podcast episode. Always use this skill — do not write show notes from scratch without reading this first.
---

# The Site Shed — Show Notes Generator

Generate complete, publish-ready show notes for a The Site Shed podcast episode.

## Inputs

Collect all of the following before writing anything:

| Input | Required? | Source |
|---|---|---|
| Episode number | Required | Provided by user |
| Episode title | Framework doc or provided by user |
| Guest name | Framework doc |
| YouTube link | Provided by user |
| Air date | Provided by user |
| Raw transcript | Riverside transcript from Google Drive — used for summary, bio, and content (NOT for timestamps) |
| Edited video captions | YouTube Data API captions from the uploaded edited video — used for KEY CHAPTERS timestamps only. Works on private/scheduled videos via OAuth. |
| Framework/booking doc | Google Drive folder for the episode |

The framework doc contains the guest's socials, website, and any listener resources. Use it only for contact details and links — never pull Q&A content from it into the show notes.

Missing-input handling: if the episode number, guest name, YouTube link, or air date is not provided, pause and ask. Do not guess. If a transcript is unavailable, say so — do not fabricate content.

## Guardrails

- Output is a draft for the team to review before publishing. This skill does not publish show notes directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate quotes, stats, or details not found in the transcript or framework doc.
- If edited video captions are unavailable for timestamps, write all other sections first and note the gap.
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Episode title naming convention

Before writing anything, determine the episode title using the Content Angle Decision Matrix:
📄 `skills/tss-content-angle-matrix.md`

The matrix walks through whether the episode is a success story or expert/educational, then identifies the correct angle (e.g. Contrarian Take, Step-by-Step Insight, Results-Driven Hook).

Once the angle and title are confirmed, apply this naming convention:

**[Title] | ft. [Guest Name] | Ep. [###]**

Example: `Why 60% of Business Transitions Fail (And It's Not the Tax Strategy) | ft. Andrea Carpenter | Ep. 505`

This title is the first line of the show notes output.

## Output format

Produce the show notes in this exact order. Do not add section headers or labels beyond what is shown.

---

[Title] | ft. [Guest Name] | Ep. [###]

🫱🏻‍🫲🏼 Book a Free Strategy Call with Tradie Web Guys: https://tradie.wiki/tssyt

[SUMMARY — 2 paragraphs]

🎥 Watch the full episode: [YouTube link]

KEY CHAPTERS
00:00 - Introduction
[MM:SS] - [Chapter Title]
...
[MM:SS] - Closing Remarks and Resources

About the Guest: [First Last]
[Bio paragraph]

Website: [guest website]
[Additional resource link if mentioned in episode — e.g. free consult page]
LinkedIn: [guest LinkedIn]

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

## Writing the summary

Two paragraphs. No header label. Written in Matt's voice — direct, specific, experience-grounded.

**Paragraph 1:** Open with the listener's problem or a punchy hook. Never start with "In this episode..." or "Today we're talking about...". Name Matt and the guest (with their company) in the first or second sentence using "Matt Jones sits down with [Guest] from [Company]". Cover the core problem the episode addresses and why it matters to trade business owners.

**Paragraph 2:** Cover what listeners will walk away with — specific insights, frameworks, or decisions the episode helps them make. End with a reason to listen that feels personal, not generic.

Style rules:
- Australian English throughout (colour, organise, systemise)
- No em dashes
- Short paragraphs, varied sentence rhythm
- Specific over vague — use real numbers, real concepts from the transcript
- Reader benefit over guest credentials
- Do not repeat the episode title verbatim

**Example (use as style reference, not a template):**

> 60% of business transitions fail — and it's rarely the tax strategy that kills them. The real culprit is the stuff nobody wants to talk about: unclear expectations, poor communication, and the relationships between the people involved. In this episode, Matt Jones sits down with Andrea Carpenter from The Transition Strategists to unpack why so many family business successions fall apart, and what trade business owners can do to make sure theirs doesn't.
>
> Whether you're thinking about stepping back in 2 years or 20, Andrea breaks down the three generations of transition thinking, the Transition Compass tool, and why starting the conversation 7 to 10 years out isn't too early — it's just smart. If you've ever thought about selling, handing down, or stepping away from your business, this one's for you.

## Generating KEY CHAPTERS

⚠️ Timestamps MUST come from the edited video captions (YouTube Data API), NOT the raw Riverside transcript. The raw transcript timestamps won't match the published episode because editing changes the timing. If the edited video hasn't been uploaded yet, write all other sections first and add timestamps once the edited captions are available.

Read the edited video captions and identify 14–18 natural topic shifts. Convert `offset` (milliseconds) to MM:SS:
- seconds = offset / 1000
- minutes = floor(seconds / 60)
- remaining = floor(seconds % 60)
- Pad both to 2 digits

Rules:
- Always start: `00:00 - Introduction`
- Always end: `[MM:SS] - Closing Remarks and Resources`
- Include a "Meet [Guest Name]" chapter near the start
- Skip sponsor/ad reads — do not make them a chapter
- Titles: Title Case, 3–6 words, topic-specific

## Writing the guest bio

2–3 sentences. Cover: role, company, location (if mentioned), and what makes them relevant to trade or home service business owners. Pull from the transcript and framework doc — not from generic descriptions.

Do not use the guest's own Q&A answers from the framework doc as bio content.

## Guest links

Include only what is available and relevant:
- Guest website (always include if provided)
- A specific resource link if the guest mentioned one during the episode (e.g. free consult, book, tool)
- Guest LinkedIn (always include)
- Do not include Instagram, Facebook, TikTok, or YouTube for the guest

## Hashtags

Always include: `#podcast #thesiteshed #tradiewebguys`

Add 4–6 topic-specific hashtags based on the episode theme. Examples:
- Business transitions: `#businesstransition #familybusiness #exitstrategy #successionplanning`
- Sales: `#salesprocess #tradesbusiness #closingdeals`
- Marketing: `#tradimarketing #digitalmarketing #tradesbusiness`
- Systems/operations: `#businesssystems #tradiebusiness #scaleup`

Keep hashtags lowercase, no spaces.

## What NOT to include

- A second CTA (no tradie.wiki/pod or other links above the summary)
- Guest social accounts other than LinkedIn
- Q&A table content from the framework doc
- The episode number in the summary text
- Any commentary or explanation around the show notes — output only the show notes themselves
