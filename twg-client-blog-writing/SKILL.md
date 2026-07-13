---
name: twg-client-blog-writing
description: >
  Writes SEO and AIO-optimised blog posts for Tradie Web Guys (TWG) trade
  business clients — plumbing, electrical, solar, roofing, HVAC, and other
  home services. Use this skill whenever a blog post, article, or content
  piece needs to be written for a TWG client's website (not the TWG agency
  blog itself — see twg-blog-publishing for that). Triggers on requests like
  "write a blog for [client]", "blog post about [topic] for [client]", or
  when a user provides a topic, keyword, or brief and asks for client blog
  copy. Always checks the client's existing blog first to confirm the topic
  hasn't already been covered before writing a word. Always use this skill
  before writing any TWG client blog post — do not write from scratch
  without reading this first.
---

# TWG Client Blog Writing

This skill produces SEO- and AIO-optimised blog posts for TWG's trade
business clients, following the **TWG Blog Copy brief format** and the
**TWG Content Creation Guidelines**. It shares its house style with
`twg-service-page-copywriting`, but a blog post is not a service page —
it earns trust and rankings through genuinely useful information, and
converts as a secondary outcome, not the primary one.

---

## Priority Order

Apply these in order. Do not let a lower priority override a higher one.

1. **Topic-uniqueness gate** — never write a post on a topic the client's
   site already covers. This is checked before anything else is drafted.
2. **Writing quality** — every sentence must read naturally and serve the
   reader. Copy that satisfies the checklist but reads robotically has failed.
3. **SEO and AIO compliance** — verify against the checklist after writing,
   not during. Compliance is confirmed at the end, not built sentence by sentence.

---

## Core Principles

- **Australian English** spelling and grammar throughout
- **Third person** — "[Business Name] recommends…" not "we recommend…"
- **Evergreen copy** — no owner-name dependency, no date-specific claims
  that will age badly
- **Educational-first** — a blog post teaches something useful. It is not
  a hard sell. The reader should get real value even if they never call.
  This is the key difference from service page copy: lead with the
  problem, the explanation, the how — not with urgency and a phone number.
- **AIO-ready** — structure content so AI Overviews, ChatGPT, Perplexity
  and similar tools can extract and cite it confidently
- **No fluff** — every sentence must explain, reassure, or inform. Cut
  anything that doesn't.

### Banned Words and Phrases

Do not use: "go to", "top quality", "all in one", "trusted source",
"top-notch", "clogs", "clog", "meticulous", "seamless", "craft", or any
passive voice constructions. Do not begin sentences with "And", "But",
or "At". Do not add "#1" or "best in Australia"-style self-proclaimed
superlative claims (no stats to back them) — use "reliable", "trusted",
or "dedicated" instead.

### No Emojis

No emojis anywhere in blog copy — headings, body, CTAs, or FAQs.

---

## Before Writing — Confirm These Details

Extract from the client knowledge base, onboarding form, or conversation
history first. Only ask if missing:

1. Business name
2. Location (suburb/region the post should be framed around)
3. Blog topic
4. Target audience
5. Primary keyword and secondary keyword(s)
6. Primary CTA type and contact details (phone, form link) — pulled from
   the client knowledge base, not assumed
7. Category tags, if the client's site uses a tagging taxonomy

---

## Edge Case: Topic-Uniqueness Check (Mandatory, Run First)

Before drafting anything, confirm the client's site does not already have
a post covering this topic or a near-duplicate of it. Publishing two posts
that target the same query cannibalises rankings and wastes the client's
content budget.

**Process:**

1. Check the client knowledge base for a content log or list of published
   blog titles/URLs, if one exists.
2. Web search `site:[clientdomain.com] [topic/primary keyword]` to
   surface any existing posts.
3. If the client has a `/blog/` (or similar) index, `web_fetch` it to scan
   titles directly.
4. Treat these as a match, not just an exact title match:
   - Same primary keyword or a close variant already targeted
   - Same core question already answered (e.g. "why is my hot water
     system leaking" vs "hot water system leaking causes")
   - Same service + same angle, even under a different title

**If a match is found:** stop before drafting. Report back to the user
with the URL/title of the existing post and either:
- Suggest a genuinely different angle on the same broad subject that
  wouldn't cannibalise the existing post (e.g. existing post covers
  causes, new post could cover cost/DIY-vs-call-a-pro/seasonal timing), or
- Flag that the brief may need a different topic entirely, and wait for
  direction rather than guessing.

**If no match is found:** note in the delivered doc that the uniqueness
check was run and came back clear, then proceed.

---

## Deliverable Format

Follow the **TWG Blog Copy brief structure** exactly. Default deliverable
is a styled `.docx` using a real Word table for the metadata block —
matching `twg-service-page-copywriting`'s conventions (real paragraph
styles, Word numbering for bullets, real bold via run properties, no
ASCII tables). Filename: `[Client Shortcode] - Blog - [Topic].docx`,
saved to the client's project folder.

**Metadata table (top of doc):**

| Field | Rule |
|---|---|
| Business Name | |
| Location | |
| Target Audience | |
| Primary KW Density | Primary keyword 2–3 times naturally |
| Secondary KW Density | 1–2 times each — avoid stuffing/repetition |
| Primary KW | |
| Secondary KW | |
| Word Count | **1,000–1,500 words** |
| Slug | Include primary keyword, under 100 characters including domain |
| Page/SEO/Meta Title | 50–65 characters, Title Case, primary keyword + location + business name if space allows |
| Meta Description | 150–165 characters, primary keyword, benefit/outcome focus, subtle CTA |
| Category Tags | If applicable (client site taxonomy) |

**Body structure (below the table):**

1. **H1 Headline** — 50–70 characters, Title Case, must include primary keyword
2. **Body** — see SEO Enhancements Checklist and Writing Quality Rules below
3. **Closing CTA paragraph** — 3–4 lines, persuasive tone, at the very end
4. **Closing summary + CTA line** — one short punchy line, e.g. "Ready to
   sort your hot water once and for all? Call [Business Name] today."
5. **FAQs** — minimum 4, maximum 6

End the doc with a client sign-off line: "Client Has Reviewed ☐" and the
note to email `support@tradiewebguys.com.au` once reviewed — matching the
brief template exactly.

---

## Writing Quality Rules

These apply to every section of every post.

### Sentence Rhythm

Vary sentence length within every paragraph. A short declarative followed
by a longer explanatory sentence followed by a mid-length close is the
natural reading rhythm.

### No Mechanical Keyword Insertion

Location and service keywords must fit naturally into a sentence that
would be well-written without them.

**Mechanical:** "For hot water repairs in Frankston, quick service matters."
**Natural:** "Frankston's older weatherboard homes often still run on
undersized electric storage tanks, which struggle the moment a second
bathroom gets added."

### One Earned Detail Per Section

Every H2 section must contain at least one specific, non-generic detail
— a method, a material, a timeframe, a local condition, a diagnostic
step — that couldn't be copy-pasted onto a competitor's blog.

### Section Openers and Closing Lines

The first sentence of a section must not restate the heading. The last
sentence of a section is the highest-value sentence in it — don't waste
it on a generic wrap-up.

---

## Scannability and Digestibility

Blog readers skim before they read. A post that's technically accurate
but arrives as a wall of text loses the reader before the earned detail
in paragraph three ever gets seen. Structure the page so the shape of
it — headings, short paragraphs, bullets — carries as much meaning as
the words do.

- **Answer first, then unpack.** Every H2 should open with a 1–2
  sentence direct answer to what the heading promises, before any
  supporting detail. A reader who only reads that first line should
  still walk away with the point.
- **Paragraph cap.** No paragraph runs longer than 3–4 sentences. If a
  section is naturally covering more than one idea — multiple causes,
  multiple factors, multiple steps — that's the signal to break it into
  H3 subheadings or a bullet list, not to keep it as one long paragraph.
- **Default to bullets for anything list-shaped.** Factors, signs,
  steps, questions to ask — if it's enumerable, it's a bulleted list,
  not a sentence stuffed with "and" and commas.
- **H3s for sub-points inside a bigger topic.** A section covering
  several sizing factors, several climate considerations, or several
  causes of a problem should be a short H2 intro (2–3 lines) followed by
  H3s per sub-point, rather than one dense paragraph trying to cover
  all of them at once.
- **Scan test.** Before marking a post done, check whether any single
  block of text runs more than roughly 5–6 lines uninterrupted on the
  page. If it does, break it up — new paragraph, H3, or bullets,
  whichever fits the content.

**Worked example — before and after:**

**Before (dense, one paragraph doing too much work):**
> Canberra sits in one of the widest daily and seasonal temperature
> ranges of any Australian capital — 35°C summer afternoons and
> sub-zero winter mornings within the same week aren't unusual. That
> matters because a split system's heating performance at low outdoor
> temperatures isn't fixed by its cooling rating. Two units with an
> identical 5kW cooling figure can differ in heating output by as much
> as 30% once the outdoor temperature drops toward freezing. A system
> sized purely on how well it will cool the room in January can
> genuinely disappoint in July.

**After (short intro, then split by sub-point):**
> Canberra sits in one of the widest daily and seasonal temperature
> ranges of any Australian capital. That swing changes what "right
> size" actually means — it's not just a summer question.
>
> **Summer Cooling and Winter Heating Aren't the Same Calculation**
> A split system's heating performance at low outdoor temperatures
> isn't fixed by its cooling rating. Two units with an identical 5kW
> cooling figure can differ in heating output by as much as 30% once
> the outdoor temperature drops toward freezing.
>
> **Size for the Whole Year, Not Just Today's Phone Call**
> A system sized purely on how well it cools the room in January can
> genuinely disappoint in July.

Same information, same word count roughly — but the reader can scan the
bolded H3s and get the shape of the argument before deciding which part
to actually read closely.

---

## Keyword and Heading Guidelines (from TWG Content Creation Guidelines)

- **Meta title:** primary keyword included, Modifier + KW format for
  local relevance, plus a descriptive statement or sentiment keyword that
  fits the page (e.g. "Local Plumbing Company with Reliable Plumbers in
  Melbourne").
- **Meta description:** primary keyword (with geo-modifier at least once
  for local clients) + a descriptive statement about the service/offer +
  a call to action with value proposition. Business phone numbers are a
  plus if there's room.
- **H1:** one per page only, 50–70 characters, primary keyword included,
  at least one geo-modifier for local clients. Lower headings drop to H2/H3.
- **Heading capitalisation:** Title Case on every heading (capitalise
  each important word; skip "with", "the", "and", "for", "a", etc). No
  full stop at the end of a heading.
- **Slug/URL:** don't repeat a keyword fragment that's already in the
  domain name (e.g. don't add "-plumbing" to a slug on a domain that
  already contains "plumbing").
- **Secondary keywords:** use all provided secondary keywords at least
  once where it reads naturally (not mandatory if it would force it).
  Never keyword-stuff. Place them in headings (H2–H6) where it fits.

---

## CTA Guidelines

Blog posts get one CTA, not several. This is a content asset the reader
is working through for the information, not a landing page they're
scanning for the next conversion prompt — a CTA dropped mid-body
interrupts that and reads as a sales insert rather than part of the
piece.

- **Exactly one CTA**, positioned at the very end: the **closing CTA
  paragraph** — three to four lines, persuasive tone, at the end of the
  article (before the FAQs, or after, per the brief template above).
- Do not place a CTA at the opening, mid-body, or after any individual
  section. If a draft has more than one CTA, that's a signal to remove
  all but the closing one, not to make the others smaller.
- A sense of urgency is a bonus if it's earned by the content (e.g. a
  seasonal angle), not manufactured.
- CTA wording must be outcome-focused and specific, in the client's
  voice, matching the CTA type in the client knowledge base.
- Don't embed the phone number repeatedly through body copy — save it
  for the CTA element.

---

## Internal Linking

| Word Count | Internal Links |
|---|---|
| 500 or less | 2–3 |
| 501–999 | 4–5 |
| 1,000–2,000 | 6–10 |
| 2,001–4,000 | 11–15 |

Blog posts default to 1,000–1,500 words, so aim for **6–10 internal
links** as standard. Link to relevant service and location pages on the
client's site. Provide an "Internal Links — Suggested" reference table
at the foot of the deliverable.

Add 1 external authoritative link where it strengthens a factual claim
(e.g. a manufacturer spec sheet, an Australian standards body).

---

## FAQ Research Process

Don't write FAQs from memory. Before drafting:

1. Web search "[topic] frequently asked questions [trade] Australia"
2. Review competitor blog posts or FAQ sections covering the same topic
   in Australian markets
3. Cross-reference against the client's keyword sheet if one exists —
   ungrouped/question-based keywords often belong here
4. Select the 4–6 questions with the highest real-world relevance

**FAQ writing rules:**
- Phrase every question exactly as a person would type or speak it
- Each answer: 2–3 sentences, complete and standalone
- Naturally work the primary keyword and location into 2–3 answers where
  it reads correctly
- No specific pricing — route cost questions to: "Contact [Business
  Name] directly for an accurate quote — all pricing is confirmed before
  any work begins, with no obligation to proceed"

---

## SEO Enhancements Checklist

- [ ] Primary keyword in the first paragraph
- [ ] Primary keyword in the H1 (20–70 characters)
- [ ] Primary keyword in at least one subheading (H2/H3)
- [ ] Headings structured H1 → H2 → H3, no skipped levels
- [ ] 6–10 relevant internal links (scaled to word count — see table above)
- [ ] 1 external authoritative link, where it strengthens a claim
- [ ] Primary keyword used 2–3 times naturally across the body
- [ ] Secondary keywords used 1–2 times each, no stuffing

## AIO Checklist

- [ ] At least 2–3 H2s phrased as questions
- [ ] Opening paragraph answers the implied search query in the first
      2 sentences
- [ ] Each paragraph is self-contained and readable in isolation
- [ ] 2–3 specific, citable factual statements included
- [ ] FAQs phrased as natural search queries with complete standalone answers
- [ ] No passive voice, no filler, no banned words
- [ ] Australian English and evergreen framing throughout

---

## Final Quality Audit — Run Before Marking Any Post Done

1. **Topic-uniqueness check was run and documented** (see Edge Case above)
2. All Writing Quality Rules satisfied
3. All Scannability and Digestibility rules satisfied — no paragraph
   exceeds 3–4 sentences without breaking to a list, H3, or new
   paragraph; multi-point sections use H3s or bullets, not one dense
   paragraph
4. All SEO Enhancements Checklist items satisfied
5. All AIO Checklist items satisfied
6. Word count is 1,000–1,500
7. **Exactly one CTA present** — the closing CTA paragraph, positioned
   at the end. No CTA at the opening or mid-body.
8. 4–6 FAQs present, researched (not written from memory)
9. Internal Links — Suggested table included at the foot of the doc
10. Metadata table fully completed (no blank fields)
11. Client sign-off line present at the end of the doc
