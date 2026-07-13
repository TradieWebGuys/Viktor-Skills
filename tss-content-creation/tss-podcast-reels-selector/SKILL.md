---
name: tss-podcast-reels-selector
description: Identify the best short-form clips from a raw Site Shed podcast transcript and write a production-ready shorts brief with reel titles, timestamps, and social caption copy for YouTube Shorts and Instagram Reels. Use this skill whenever a podcast transcript is provided and the user asks to find clips, shorts, reels, or social media cuts. Triggers on: "find the best shorts", "what clips should we cut", "identify reels from this episode", "clips for social", "what can we pull from this episode", or any request to extract short-form content from a podcast transcript. Always use this skill — do not identify clips or write reel copy from scratch without reading it first.
---

# TSS Podcast Reels Selector

You're creating a production-ready shorts brief from a raw Site Shed podcast transcript. The output is a markdown file that a video editor or social media manager can work from directly — no need to re-watch the episode.

## Inputs

- **Podcast transcript** (required) — raw transcript from Riverside or similar source.
- **Guest name + company** (required) — for credit and file naming.
- **Host name** (required) — typically Matt Jones. Can be inferred.
- **Episode number** (recommended) — for ClickUp task linkage.

Missing-input handling: if the transcript or guest name is not provided, pause and ask. Do not guess.

## Guardrails

- Output is a draft brief for the video editor. This skill does not cut or publish video content directly.
- Pause on missing inputs — ask rather than guessing.
- Never fabricate timestamps, quotes, or moments not found in the transcript.
- Writing: plain, direct, active sentences. Avoid generic filler (delve, leverage, robust, seamless, unlock, streamline, elevate).

## Step 1: Read the full transcript

Read the entire transcript before identifying anything. Note the key themes, the strongest moments, and who's driving the insights. If the host dominates, make a deliberate effort to surface at least one guest-led clip where the guest's own words or story are the main event — not just agreeing with the host.

## Step 2: Identify 4–6 clips

Each clip must be:

- **A complete thought** — starts and ends cleanly, no context required from the rest of the episode
- **Under 3 minutes** — 30s–2min is the sweet spot
- **Viral or valuable** — it does at least one of:
  - Challenges a common belief or calls out a mistake
  - Shares a concrete story or case study with a clear lesson
  - Drops a surprising stat or specific number
  - Captures emotion, humour, or self-awareness
  - Delivers a strong opinion people can agree or disagree with

Strong moments to look for:
- A guest delivers a line that lands better than the host's setup
- The host makes a blunt, punchy summary statement
- A specific anecdote that illustrates a broader point
- A moment where someone says the thing everyone thinks but nobody says

## Step 3: Write the brief

Save the file to the user's project folder as `[guest-name]-[host-name]_shorts-brief_v1.md`.

## Step 4: ClickUp hand-off

When completing the "Reels Clip Selection From Raw Transcript" ClickUp subtask, always mention **@Frean** (ClickUp user ID `95454712`, male) in the completion comment text so he's notified the brief is ready. Include his name visibly in the comment body (e.g. "@Frean — shorts brief is uploaded and ready for editing").

### Format

```
# Shorts Brief — [Host] x [Guest] ([Guest's Business])
**Full Episode:** [2–3 sentences summarising what the episode covers.]

---

## CLIP 1 — [Reel title]

**Timestamps:** [HH:MM:SS – HH:MM:SS]

### Reel Description
[Caption copy — see rules below]

---

[Repeat for each clip]

---

*All clips should end with a lower-third or end card directing viewers to the full episode at thesiteshed.com.*
```

## Reel title rules

The clip heading IS the reel title. Write it as a hook — not a theme label. *7–10 words maximum.*

- ✅ "Most owners call leads 3 times. We call 30."
- ✅ "They were doing $1M measuring the wrong thing."
- ❌ "The Wrong KPI Story" — theme label, not a hook
- ❌ "The Flooded Basement" — same problem
- ❌ "This business was doing $1M/month and measuring the completely wrong thing." — too long (12 words)

Specific numbers, contrarian takes, and incomplete thoughts that demand resolution all work well. No quotes around the title in the markdown.

## Reel description rules

This is the social caption — the only copy needed per clip.

1. **Hook first** — the most interesting line, stat, or question from the clip
2. **Body** — 2–3 short paragraphs building the tension or insight
3. **Guest credit** — include the guest's full name and their @social handle at least once
4. **CTA** — platform-neutral, works for both YouTube Shorts and Instagram. Never write "link in bio" (Instagram-only). Point people to the full episode using the listen link, and where it fits, mention the YouTube channel:
   - Default: "Listen to the full episode at tradie.wiki/listen"
   - When useful (e.g. the clip is posted off-YouTube): add "Now live on our YouTube channel, The Site Shed"
5. **Hashtags** — 6–8 relevant tags on the final line

**Do not include:**
- A "Clip Description" or plot summary section
- Runtime or duration estimates
- "link in bio"
- Quotes around the reel title
