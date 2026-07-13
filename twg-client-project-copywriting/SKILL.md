---
name: twg-client-project-copywriting
description: "Writes client project gallery submissions and case studies for Tradie Web Guys (TWG) trade clients — plumbing, electrical, solar, roofing, bathroom/kitchen renovation, and other home service businesses. Use this skill whenever a case study, project gallery page, project story, or 'client win' write-up needs to be written for a TWG client's own website (not the TWG agency blog). Triggers when a user provides a completed Client Project Gallery Copywriting Brief, a filled-out project form, transcript of a client interview, or raw notes about a completed job and asks for a case study, project page, or gallery submission. Covers the full deliverable — objective, approach, challenges, solution, results, and testimonial, written in the client's own first-person voice. Always use this skill before writing any TWG case study or project gallery copy — do not write one from scratch without reading it first."
---

# TWG Case Study / Project Gallery Copywriting

This skill produces case study and project gallery pages for TWG's trade clients — the "project" pages that sit on a client's own website (e.g. `/project/bathroom-renovation-sydney-cbd/`), not TWG's own agency blog. Every case study tells the story of one real, completed job: what the client wanted, how the business approached it, what got in the way, how it was solved, and what came of it.

This is a sibling skill to `twg-service-page-copywriting`. Read that skill's Core Principles and CTA Guidelines for background — but note the voice is different here (see below), and the two should not be conflated.

---

## What Makes a Case Study Different From a Service Page

A service page sells a service. A case study proves it happened. Keep this distinction in mind throughout:

- **Voice is first person plural** — "we" / "our team", written as though the client business itself is telling the story. This is the opposite of service pages, which use third person. Getting this wrong is the single most common failure mode when reusing service-page habits.
- **It's a story, not a pitch.** Lead with what happened, not with why the reader should book. SEO and conversion goals still apply, but they ride underneath the narrative — they don't drive it.
- **Every fact must be real.** Never invent a client name, a quote, a statistic, a challenge, or a result that wasn't supplied. If a detail is missing (no testimonial, no hard numbers, no named challenge), say so and ask, or write the section honestly without it — a case study with a thin "Challenges" section because the job genuinely went smoothly is more credible than a fabricated obstacle.

---

## Before Writing — Confirm These Details

Pull from the filled-out Client Project Gallery Copywriting Brief, a project form, client interview notes, or conversation history. Only ask if genuinely missing — don't guess at facts, especially the client's name, the specific work performed, results, or quotes.

1. Business name and location
2. Client's name (or a privacy-safe version — first name and last initial is the norm, e.g. "Kathryn B.") and their situation going in
3. Target audience
4. Primary keyword and secondary keywords
5. The service(s) performed — note every service touched if the job spanned multiple trades, since each is an internal linking opportunity
6. Project length / timeframe
7. The objective — what the client wanted, why they chose this business
8. The approach — how the job was actually done, in enough detail to write from (not just "we did great work")
9. Any real obstacles and how they were handled (or confirmation there weren't significant ones)
10. Results — anything measurable (dollars, days, before/after specs) or qualitative (client reaction)
11. A testimonial, if one exists — use it close to verbatim, lightly cleaned up, never paraphrased into something the client didn't say
12. Image and video links/captions, including before/after pairs where available
13. Reference material for brand tone — 2-3 of the client's existing case studies, blog posts, or general site copy, so the voice matches what's already published

**Reading the brand tone:** Before writing, look at how the client's other case studies (or their site generally) sound. A technical/trade-heavy brand (roofing, solar, electrical) leans into equipment, specs, and performance outcomes. A storytelling/lifestyle brand (renovations, bathrooms) leans into the people, the decision-making, and the transformation. Match what's already there rather than defaulting to one register for every client.

---

## Word Count — Scale to the Project

Case studies read best tight and specific — padding a simple job to hit a word count produces filler, and TWG's own published examples (roofing, bathroom, solar, construction case studies) mostly land between 350 and 700 words even on substantial jobs. Scale the target to genuine project complexity, not to a fixed number:

| Project Type | Target Word Count |
|---|---|
| Single-trade, single-visit job (a reroof, an install, a repair) | 400–600 words |
| Standard renovation or multi-stage install | 600–900 words |
| Complex, multi-trade, or long-running project with real scope changes | 900–1,200 words |

Don't pad to reach a bracket. If the honest story is told well in 450 words, 450 words is correct. Only push toward the top of a bracket when the project genuinely has that much real material — multiple phases, several services, a documented before/after journey.

---

## Keyword Density

- **Primary keyword:** roughly once every 250–300 words of body copy, used where it reads naturally (ideally once in the first paragraph, once in the H1, once in at least one subheading)
- **Secondary keywords:** 1–2 mentions each across the piece — enough to signal relevance, not enough to feel inserted
- Every keyword mention must attach to something specific and true about this job. A mention that exists only to hit the density target reads exactly like it was inserted for that reason — rewrite it around a real detail instead (the specific product installed, the specific room, the specific local condition).

---

## Metadata Block

Save as a two-column table at the top of the deliverable for the developer's reference:

| Field | |
|---|---|
| **Business Name** | |
| **Location** | |
| **Client Name (privacy-safe)** | |
| **Target Audience** | |
| **Primary Keyword** | |
| **Secondary Keywords** | |
| **Services Involved** | |
| **Category Tags (WordPress)** | |
| **Project Timeframe/Length** | |
| **Word Count** | Target from the table above |
| **URL Slug** | `/project/[primary-keyword-location]` — under 100 characters including domain |
| **Meta Title** | 50–65 characters, Title Case. Primary keyword + location + business name if space allows |
| **Meta Description** | 150–165 characters. Primary keyword + benefit/outcome + a subtle CTA |

**Category Tags:** Assign the WordPress post to the category (or categories) matching the service(s) actually delivered — e.g. *Bathroom Renovation*, *Laundry Renovation*, *Roof Replacement*, *New Roof*, *Blocked Drains*, *Switchboard Upgrade*, *Solar Installation*. Use the client's existing WordPress category taxonomy where it's known rather than inventing a new one — check a couple of their published case studies or service pages first. If the site's category list isn't available, propose the most natural category name(s) in Title Case and flag them for the developer/PM to confirm against the live site before publishing. A job spanning multiple trades gets a tag for each trade actually performed, not just the primary one.

---

## SEO Checklist (apply to every case study)

- Primary keyword in the first paragraph
- Primary keyword in the H1 (50–60 characters, Title Case)
- Primary keyword in at least one H2/H3
- Proper heading hierarchy — H1 → H2 → H3, no skipped levels
- 2–3 internal links to relevant service or location pages (more on longer pieces — see Internal Linking below)
- 1 external authoritative link only if there's a genuine reason (a product manufacturer, a standards body) — don't force one in

---

## H1

Title Case, 50–60 characters, includes the primary keyword. Unlike a service page H1, a case study H1 can and should carry some narrative — look at how the client's real pages do this:

- *How HDK Transformed Jenny's Leaky Roof with Heavy-Duty Coloursteel*
- *From Tight Spaces to Functional Luxury Bathroom Renovation in Sydney CBD*
- *Kellyville Home Gains Savings and EV Readiness with a Solar Battery Upgrade*

A flat literal H1 ("Bathroom Renovation Sydney CBD") is acceptable when nothing else fits, but a narrative or outcome-led H1 that still contains the keyword and location performs better and matches the standard TWG has already set with published clients. If writing several case studies for the same client in one sitting, vary the H1 construction across them (outcome-led, transformation-led, results-led) so they don't read like a filled-in template.

---

## Body Structure

The brief's default section order works for most jobs. Follow the client's filled-out form if they've already organised it a different way, or adapt the order to whichever structure tells this specific story best — the sections below are jobs to do, not a rigid template.

### 1. Intro / About the Project

Two sentences max. A catchy summary of what happened and what was achieved — this is the hook, not a full recap. Follows immediately with the first CTA.

**AIO tip:** these two sentences should be self-contained enough to answer "what was this project?" without needing the rest of the page.

### 2. Quick Overview

A short, scannable snapshot placed right after the intro (as a styled sidebar block if the client's site supports one — this is what every published TWG project page already includes). Always state all three explicitly, even when they feel obvious from the story above:

- **Location:** suburb + state/region (or city + country for NZ clients)
- **Services Delivered:** every service actually performed on this job, listed plainly — should match Services Involved in the metadata block
- **Timeline:** the real project duration, in whatever unit reads naturally for the job (e.g. "4 days", "3 weeks", "2 months") — never soften this into something vague ("a short timeframe") when a real duration was supplied

This lets a reader confirm at a glance whether this case study matches their own job before committing to reading the full story — and gives the developer a clean, consistent block to style as a sidebar.

### 3. The Objective

~100 words (600 characters) max. What the client wanted from working with this business — the problem, the goal, why they chose this business over alternatives if that detail exists. This is where the reader's own situation gets mirrored back to them.

### 4. Our Approach

~100 words max, though this can run to a short numbered process (3–5 steps) for a staged project — see the Better Bathrooms Sydney CBD example for a clean numbered-steps execution. If the job touched more than one service, give each service 1–2 sentences — this is the main internal-linking opportunity on the page, so link the service name through to its dedicated service page.

### 5. The Challenges

~100 words max. The real obstacle(s) and how they were handled. If the job genuinely had no significant obstacles, don't invent one — either fold a minor logistical note in here (parking, access, timing around the client's schedule) or shorten this section honestly rather than manufacturing drama. A believable "nothing major came up, here's the one small thing we managed" reads better than a stretched crisis.

### 6. The Solution

~100 words max. What was actually done to complete the job — specific products, methods, or paid packages/add-ons and why they mattered. This is the section that needs the most earned detail: a specific material, brand, or technique that couldn't be copy-pasted onto a competitor's case study.

### 7. Results / Final Thoughts

~200 characters max (shorter still if a video is embedded). State the outcome plainly — and use real numbers if they exist (energy savings, dollar figures, time saved, before/after specs). If a client quote is available, this is often the natural place for it, though it can also stand alone as its own Testimonial block.

### 8. Testimonial (if available)

Use the client's actual words, lightly cleaned up for readability (remove filler, fix grammar) but never rewritten into something they didn't say. Attribute with a first name or the privacy-safe name used throughout.

### 9. Images / Video

List image and video links/captions supplied, noting Before/After pairs explicitly. Flag descriptive alt text for each image (subject + service + location, e.g. "Bathroom renovation, Sydney CBD — after") for the developer.

---

## Optional Modules

Add if the source material supports it — don't force these:

- **What We'd Do Differently** — a short, honest note on one thing that could be improved next time (parking logistics, timeline buffer). Builds trust precisely because it's not a sales point. Only include if there's a genuine, minor learning — never a real complaint or anything reflecting badly on quality of work.
- **Standout Moments** — 2–3 short labelled highlights (a fast turnaround, a specific technical win, client delight) when the job has more good material than fits neatly into Solution or Results.
- **Local-SEO Close** — a short closing paragraph positioning the business as the go-to for this service in this location, e.g. "Your Go-To Reroofing Experts in Mount Albert, Auckland." Optional; use when the piece needs a stronger local-search anchor before the final CTA.

---

## CTAs

Case studies are story-first, not conversion-first — don't apply the service-page CTA-every-200-words rule here. Space CTAs at natural high-conviction moments instead:

1. **After the intro** — low-friction ("Enquire Now", "Start Your [Service] Today")
2. **After the approach or challenges section** — mid-piece, optional on shorter pieces
3. **Final close** — after the last section, restating the outcome and inviting the reader to get the same result

2–4 CTAs total depending on length. Wording should reflect what the reader just read, not be pasted identically at each spot. No emojis in CTAs or anywhere else in the copy.

---

## Internal Linking

| Word Count | Internal Links |
|---|---|
| 400–700 | 2–3 |
| 700–1,000 | 3–5 |
| 1,000–1,200 | 5–7 |

Link every named service to its dedicated service page the first time it's mentioned in a way that supports linking (usually in Our Approach). Provide an "Internal Links — Suggested" reference table at the foot of the deliverable for the developer.

---

## Writing Quality

- **Sentence rhythm:** vary sentence length — a short declarative followed by a longer explanatory sentence reads naturally; three same-length sentences in a row don't.
- **Earned detail:** every section should contain at least one specific, non-generic fact — a product name, a technique, a measurement, a real complication — that couldn't be copy-pasted onto a different client's case study of the same service.
- **No mechanical keyword insertion:** if a sentence was clearly built around fitting in a keyword rather than around a real idea, rewrite it.
- **Match the register to the brand:** technical clients get equipment/spec/performance language; storytelling clients get people/challenge/transformation language. See "Reading the brand tone" above.
- **No banned filler:** avoid "top quality", "all in one", "trusted source", "top-notch", "meticulous", "seamless", "craft", and passive voice constructions where an active one is natural. Don't open sentences with "And", "But", or "At".
- **Spelling convention:** match the client's own country — Australian English for AU clients, New Zealand English for NZ clients, and so on. Check the client's existing site copy if unsure.
- **No emojis** anywhere in the deliverable.

---

## Deliverable Format

Default deliverable is a styled `.docx` file, matching the convention used for TWG service pages:

- Use real Word paragraph styles — `Heading 1`, `Heading 2`, `Heading 3`, body
- Metadata block and Internal Links table as real Word tables (not ASCII)
- Real bold via run properties, real bullet/numbering definitions where used
- Filename: `[Client Shortcode] - Case Study - [Project Name].docx`
- Saved to the client's project folder

Use the `docx` skill to build the file, and run it through that skill's unpack/repack flow so `[Content_Types].xml` is the first file in the archive (some viewers fail to open DOCX files otherwise).

---

## Quality Audit

Run through this before marking a case study done.

**Voice and facts**
- [ ] Written in first person plural ("we"/"our team"), not third person
- [ ] No invented client name, quote, statistic, challenge, or result — everything traces back to the brief or source material
- [ ] Tone matches the client's existing case studies/site (technical vs storytelling)
- [ ] Testimonial (if used) is the client's real wording, only lightly cleaned up

**Writing quality**
- [ ] Sentence rhythm varies — no three consecutive same-length/same-construction sentences
- [ ] Every section has at least one earned, specific detail
- [ ] No mechanical keyword insertion
- [ ] No banned filler words; no passive voice where active reads naturally
- [ ] No emojis

**SEO**
- [ ] Primary keyword in H1, first paragraph, meta title, meta description, and at least one subheading
- [ ] H1 → H2 → H3 hierarchy intact
- [ ] Word count matches the scaled target for this project's complexity
- [ ] Keyword density on target (primary ~1 per 250–300 words; secondaries 1–2 each)
- [ ] Internal links added per the word-count table
- [ ] 2–4 CTAs placed at natural story beats, worded to match the moment

---

## Reference

See `references/example-breakdown.md` for an annotated walkthrough of how four published TWG client case studies (roofing, bathroom renovation x2, solar) structure their Objective/Approach/Challenges/Solution/Results sections in practice — useful when the brief is thin on structure guidance and you need to see the pattern in action.
