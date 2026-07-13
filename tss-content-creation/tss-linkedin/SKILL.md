---
name: tss-linkedin
description: Write LinkedIn posts promoting The Site Shed podcast episodes — for either the show's brand profile or Matt Jones's personal profile. Use this skill whenever a LinkedIn post needs to be written for a TSS episode. Triggers on: "write a LinkedIn post", "LinkedIn for this episode", "post for Matt's LinkedIn", "social post for LinkedIn", or any request to produce LinkedIn content for The Site Shed or Matt Jones. Always use this skill — do not write TSS LinkedIn posts from scratch without reading this first.
---

# The Site Shed — LinkedIn Post Writer

Write LinkedIn posts promoting a TSS podcast episode. Two post types exist — always confirm or infer which profile the post is for before writing.

## Two post types

| Profile | Voice | Angle |
|---|---|---|
| **Show/brand profile** (`@TheSiteShed`) | Third-person or editorial "we" | Episode-led — stat hook, what listeners get, CTA |
| **Matt's personal profile** (`@MattJones`) | First-person, Matt's own voice | Story-led — personal experience or observation that earns the episode mention |

If the user says "LinkedIn post for this episode" without specifying a profile, write Matt's personal version (it performs better organically). If they ask for both, write both in one file with clear labels.

---

## Inputs

| Input | Required? | Source |
|---|---|---|
| Episode number | Required | Provided by user |
| Guest name + company | Framework doc or transcript |
| Key stats or frameworks | Transcript |
| Episode link | Provided by user (goes in comments note at end) |
| Profile type | Inferred | User-specified, or default to Matt's personal |

Missing-input handling: if the episode number or guest name is not provided, pause and ask. If the transcript is unavailable, say so — do not fabricate quotes or stories.

## Guardrails

- Output is a draft for the team to review before posting to LinkedIn. This skill does not post content directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate quotes, stats, or personal stories not found in the transcript.
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

---

## Post structure

Both post types follow the same structural logic — they just differ in voice and opening angle.

### 1. Hook (1–3 lines)

The first 2 lines are what LinkedIn shows before "see more." Make them impossible to scroll past.

**Brand profile:** Lead with the most striking stat or tension from the episode.
**Matt's personal profile:** Lead with a personal story, observation, or moment that connects to the episode theme. The episode itself is not mentioned until later — earn it first.

Good hooks:
- A stat that surprises ("60% of family business transitions fail.")
- A contradiction ("Nobody did anything wrong, exactly. There was just no structure.")
- A specific personal detail ("One of my best mates growing up — his dad was a plumber in Sydney.")

Never open with:
- "In this week's episode..."
- "I'm excited to share..."
- "Check out my latest podcast..."
- The guest's name

### 2. Body (short paragraphs, 1–3 lines each)

Keep paragraphs short. LinkedIn is read on mobile. White space matters.

**Brand profile body:** Move from the hook stat → introduce guest in one sentence → share 3–5 key takeaways using arrows:

```
→ The insight or concept
→ Another one
→ Another one
```

**Matt's personal profile body:** Tell the story fully before pivoting to the episode. The story should:
- Be specific (names, places, trades where relevant)
- Build to the insight naturally — don't force it
- Connect directly to the episode theme
- Be something Matt actually experienced or observed (pull from the transcript if he shared a personal story during the episode)

The episode mention comes after the story lands. One or two sentences is enough: who the guest is, what the episode is about, and the one thing from it that Matt keeps coming back to.

### 3. Closing line + CTA

End with a reason to listen — one sentence that speaks directly to the reader's situation.

Then the listen line:

```
🎧 Episode [###] — link in the comments.
```

Always put the link in the comments, not the post body. LinkedIn's algorithm suppresses reach on posts with external links in the body.

---

## Writing rules

- **Short paragraphs** — 1 to 3 lines max. Single-line paragraphs are fine and often better.
- **No em dashes** — use a full stop, comma, or rewrite
- **Australian English** — colour, recognise, organise
- **Arrows for lists** — use `→` not bullet points or hyphens
- **Stats over vague claims** — if the transcript has a number, use it
- **No hashtags** — unless the user specifically requests them
- **No tagging the guest** — leave a note that the user can add the tag manually when posting
- **Link in comments** — never in the post body
- **No "excited to share" or "honoured to"** — ever

## Matt's voice (personal profile)

Matt's posts should read like something a smart, experienced tradie business owner would actually write — not a media company. Specific details, plain language, a dry wit where it fits. He's been in and around the trades his whole life and the posts should feel like it.

Pull from the transcript if Matt told a personal story during the episode — those are gold. He often shares observations about clients, mates, or his own experience that translate directly into LinkedIn content.

## What NOT to include

- The episode link in the post body (comments only)
- Hashtag blocks
- "In this episode" as an opener
- Emojis beyond the single 🎧 at the end
- Guest socials or website
- A summary of every point covered — pick the best 3–5 and make them count

---

## Output format

If writing one post type:

```
[POST COPY — ready to copy/paste]

---
Note: Add the episode link as the first comment when posting.
[Optional: tag @GuestName if they're on LinkedIn]
```

If writing both:

```
## BRAND PROFILE POST
[post copy]

---
Note: Add episode link in first comment.

---

## MATT'S PERSONAL PROFILE POST
[post copy]

---
Note: Add episode link in first comment. Tag @GuestName if relevant.
```
