---
name: tss_newsletter
description: Build TSS podcast newsletter emails matching the GHL template. Takes a YouTube URL, episode number, and guest name, produces paste-ready HTML for GoHighLevel.
---

## When to use
When asked to create a newsletter email for a The Site Shed podcast episode. Trigger phrases: "newsletter for episode", "podcast email", "TSS email", "build the newsletter".

## Sending Details
- **GHL sub-account:** Tradie Web Guys (TWG sub-account — NOT a separate TSS sub-account)
- **Sender name:** Matt Jones
- **Sender email:** info@tradiewebguys.com.au

## Template Reference
Saved at `references/tss_ep504_template.html` — the canonical MJML-based email template exported from GHL.

## Template Structure
1. **Hero image** — YouTube thumbnail: `https://img.youtube.com/vi/{VIDEO_ID}/maxresdefault.jpg`, linked to YouTube URL
2. **Two side-by-side CTAs** — "Watch on Youtube" (→ YouTube link) + "Listen On Your Device" (→ tradie.wiki/listen). Black bg (#000000), white text, 0px border-radius
3. **Body copy** — Montserrat 16px. Episode summary in Matt's conversational voice. Bold bullet-point takeaways
4. **Episode link** — 🎧 "Listen to Episode X here:" → tradie.wiki/listen
5. **TWG CTA footer** — TWG logo (GCS-hosted), soft pitch, "Book a time with the team" button → tradiewebguys.com.au
6. **TSS branding** — "The Site Shed is proudly a product of Tradie Web Guys" + description
7. **Legal footer** — Black bg, white text. GHL variables: `{{right_now.year}}`, `{{location.name}}`, `{{location.email}}`, `{{email.unsubscribe_link}}`

## Design Specs
- Page bg: #EAF0F6
- Container: #FFFFFF, 650px max-width
- Primary font: Montserrat (fallback: arial, helvetica, sans-serif)
- Headings font: also Montserrat
- Body text: 16px
- CTA buttons: #000000 bg, #FFFFFF text, 0px border-radius
- Footer: #000000 bg, #FFFFFF text, 14px
- Border-radius: 0px throughout (sharp corners)

## Inputs

| Input | Required? | Source |
|---|---|---|
| YouTube video URL or ID | Required | Provided by user |
| Episode number + guest name | Required | Provided by user |
| Episode topic / key talking points | Required | Transcript or user-provided |

Missing-input handling: if the YouTube URL, episode number, or guest name is not provided, pause and ask. Do not guess. If talking points or a transcript are unavailable, ask for a brief summary of the episode.

## Guardrails

- Output is a draft HTML file for the team to review before sending via GoHighLevel. This skill does not send emails directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate quotes or episode details not confirmed by the transcript or user.
- Keep all GHL template variables intact — breaking them breaks the email delivery.
- Writing: plain, direct, active sentences in Matt's voice. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Workflow

1. Read the reference template HTML from `references/tss_ep504_template.html`
2. Swap the YouTube video ID (thumbnail + links)
3. Update preheader text (one-liner teaser)
4. Write body copy in Matt's voice with bold bullet takeaways
5. Update episode number references
6. Keep all GHL template variables intact
7. Deliver final HTML file

## Key URLs (static across episodes)
- Listen link: https://tradie.wiki/listen
- Subscribe link: https://tradie.wiki/tssyt
- TWG website: https://www.tradiewebguys.com.au
- TWG logo: https://storage.googleapis.com/msgsndr/cuS7M6EnfbXM2s2VJ4I8/media/8dd08bc0-3e56-421d-9f05-c6af2a12c35d.png
- UTM pattern: `?utm_source=newsletter&utm_medium=email&utm_campaign=tss`

## Notes
- The HTML uses MJML-generated table-based layout with Outlook conditionals — do NOT simplify to div-based layout
- Keep all `<!--[if mso]>` blocks intact for Outlook compatibility
- Preheader text goes in the hidden div at top of body
- GHL delivers via their email infrastructure; we just provide the HTML content
