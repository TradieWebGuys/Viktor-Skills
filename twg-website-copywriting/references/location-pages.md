---
name: twg-location-page-copywriting
description: "Writes SEO and AIO-optimised location/service-area page copy for TWG trade business clients (plumbing, electrical, solar, roofing, and other home services). Use this skill whenever a location page, suburb page, or service-area page needs to be written or rewritten — these are broader hub-style pages covering a business's presence and full service range in a suburb, region, or service area, distinct from single-service pages. Triggers when a user provides client details, a location brief, keywords, or an onboarding form and asks for location page copy, suburb page copy, or service-area copy. Always use this skill before writing any TWG location page — do not write from scratch without reading this first. For single-service pages (one trade service in one location, e.g. 'Blocked Drains Frankston'), use twg-service-page-copywriting instead."
---

# TWG Location Page Copywriting

This skill produces conversion-focused, SEO and AIO-optimised **location/service-area page** copy for TWG trade clients, built from the official TWG Location Page template and Content Creation Guidelines.

A location page is a hub page — it establishes the business's presence and full service range across a suburb, region, or service area. This makes it structurally different from a service page: longer (1000–1500 words vs 500–1100), covers multiple services rather than one, and carries a lighter keyword density spread across the whole page rather than concentrated repetition. If the brief is actually about one service in one suburb (e.g. "Hot Water Repairs Frankston"), that's a service page — use `twg-service-page-copywriting` instead.

---

## Priority Order

Apply these in order. Do not let a lower priority override a higher one.

1. **Writing quality** — every sentence must read naturally and serve the reader. Copy that hits every checklist item but reads like a template has failed.
2. **Differentiation** — earned local detail throughout, not decorative suburb-dropping. See Writing Quality Rules below.
3. **SEO and AIO compliance** — verify against the checklist after writing, not while writing.

---

## Core Principles

- **Australian English** spelling and grammar throughout
- **Third person** — "[Business Name] provides…" not "we provide…"
- **Evergreen copy** — no owner-name dependency; must stay valid if the business grows or adds staff
- **Hub, not pitch** — a location page earns trust by demonstrating breadth and local familiarity across the whole service area, then converts. It reads differently to a service page, which leads harder and faster on one job
- **AIO-ready** — structure content so AI Overviews, ChatGPT, Perplexity, and similar tools can extract and cite it confidently (see AIO section below)
- **No fluff** — every sentence must reassure, inform, or convert

### Self-Proclaimed Claims

Never use "#1 in Australia," "best in [location]," or similar unverifiable superlative claims — TWG doesn't hold the data to back them and they read as false claims. Use grounded alternatives instead: "trusted," "reliable," "dedicated," "experienced," "established." Anchor these to something specific wherever possible (years active, number of local jobs, licensing) rather than leaving them as unsupported adjectives.

### Heading Formatting

- No full stop at the end of any heading
- Title Case on all headings — capitalise the initial letter of important words; leave minor words (the, and, for, a, with, etc.) lowercase unless they open the heading

---

## Deliverable Format

The default deliverable is a styled `.docx` file saved directly into the client's project folder on the local file system.

- Use real Word paragraph styles — `Heading 1`, `Heading 2`, `Heading 3`, body
- Use Word's numbering definitions for bullets (not `•` characters typed inline)
- Use a proper Word table for the metadata block and the suggested-links table (not ASCII) — but never for the Trust Signals block or any body content, which stay as bullet lists (see CTA Guidelines and Body Structure)
- Build the call-CTA phone button as a small shaded single-cell table (or equivalent block) with centred, bold, contrasting-colour text, sitting directly under its bold question line — this is a deliberate visual device, not a data table, so it's exempt from the "no tables in body content" rule above
- Use real bold via run properties (not asterisks)
- Filename follows `[Client Shortcode] - Location Page - [Location Name].docx`

For multi-suburb batches, a consolidated build script (Node.js + docx-js) with shared helpers and one array of page configs is the most efficient approach. Pack every `.docx` through the docx skill's unpack/repack flow so `[Content_Types].xml` is the first file in the zip archive — some viewers fail to open DOCX files otherwise.

**Do not deliver via Google Docs upload.** The Drive API does not auto-convert HTML or DOCX to native Google Docs format, and routing through Drive's converter loses styling and can create duplicates. The client can drag the DOCX into Drive themselves if they want a Google Docs copy.

---

## Before Writing — Confirm These Details

Extract from the client knowledge base, onboarding form, or conversation history first. Only ask if missing:

1. Business name
2. Location / service area this page covers (suburb, region, or broader area — confirm the exact scope and spelling from the client knowledge base, not assumed)
3. Target audience (homeowners, strata, commercial)
4. Primary keyword and secondary keywords
5. The range of services this business offers that should be represented on the page (a location page typically touches most or all of a client's core services, briefly, rather than going deep on one)
6. USPs — guarantees, years experience, response times, licences
7. CTA type and all contact details required for it — phone number, form link, or both
8. Any copy-restricted items — pricing specifics, call-out fees, promotions that shouldn't appear in public copy

Location details are project-specific. Never carry a suburb name, spelling, or boundary assumption over from another client or another page.

---

## Metadata Block

Open the deliverable with this table, exactly as specified in the TWG Location Page template:

| Field | |
|---|---|
| **Business Name** | |
| **Location** | |
| **Target Audience** | |
| **Primary KW Density** | Primary keyword 2–3 times naturally |
| **Secondary KW Density** | 1–2 times each. Avoid keyword stuffing / repetition |
| **Primary KW** | |
| **Secondary KW** | |
| **KW Density (scale proportionally for longer pieces, readability first)** | Primary: 1x every 250–300 words. Secondary: 2–3x combined across all secondary keywords, every 1500 words |
| **Word Count** | 1000–1500 words |
| **URL Slug** | Include the primary keyword. Must be under 100 characters including the domain |
| **Meta Title** | 50–65 characters, Title Case. Primary keyword + location + business name if space allows |
| **Meta Description** | 150–165 characters. Primary keyword, clear description, benefit/outcome-focused, subtle CTA |

### Keyword Density in Practice

The density figures above are targets, not formulas to force. On a 1200-word page, that's roughly 4–5 natural primary keyword mentions and a handful of secondary mentions spread thin — nowhere near the concentration expected on a single-service page. If a paragraph needs the primary keyword inserted to hit the count, the paragraph is wrong, not the count. Every secondary keyword provided should appear at least once somewhere on the page if it can be worked in naturally; it's fine if not every one makes it in — never force one to satisfy coverage.

### Title and Meta Title Construction

For local pages, build the title as **Modifier + Keyword**, layered with a descriptive statement or sentiment that fits the business — not a bare keyword stuffed in.

**Example:** *Local Plumbing Company with Reliable Plumbers in Melbourne* — this naturally hits "plumbers in Melbourne," "local plumbing company," "plumbing company," and "plumbers/plumber" without reading like a keyword list.

### Meta Description Construction

Every meta description does three jobs in 150–165 characters:
1. **Keyword** — hit the primary keyword, and for local clients, the geo-modifier at least once — but only where it adds value, not just to tick the box
2. **Descriptive statement** — what the page offers: the service range, the quality angle, or the area covered
3. **Call to action + value proposition** — a clear next step (Call Now, Get a Free Quote, Contact Us) paired with a real value proposition (free inspection, fast response) where the client offers one. A phone number here is a plus.

**Example:** *Expert Los Angeles Plumber Company Ready to Handle All Your Home Plumbing Needs. Call Our Plumbers in Los Angeles at 123-456-7890 for FREE Inspection.*

### URL Slug Rule

If part of the primary keyword is already in the domain name, don't repeat it in the slug.

**Incorrect:** `harrisonplumbing.com/sutherland-shire-plumbing`
**Correct:** `harrisonplumbing.com/sutherland-shire-plumbers`

---

## Page Structure

### H1

- 50–70 characters, Title Case
- Must include the primary keyword
- Only one H1 on the page — if a second heading of similar weight is needed, it drops to H3 (with a keyword) or stays bold with no heading tag if it carries no keyword

**Example:** *Plumbing Problems Resolved By Licensed Melbourne Plumbers*

### H2 Subheading (Directly Under H1)

- One sentence, reflects the H1, carries the keyword, can include the location
- Title Case, no full stop
- Outcome or trust-led — this is the reader's second confirmation they've landed in the right place

**Example:** *Providing On-Time, Long-Lasting Plumbing Solutions to Sydney Residents for 15 Years*

### Opening Paragraph

- Introduce the business, the location/service area, and the range of trade services covered in the first 2–3 sentences
- **AIO:** the first 2 sentences must be self-contained and directly answer the implied query ("who covers [location] for [trade] work")
- Establish the earned local detail early — something specific to the area (property era, common local conditions, growth corridor, coastal exposure) rather than a decorative suburb mention
- Follow with the first CTA

### Body

The body is where the location page's hub nature matters most — it isn't a deep dive on one job, it's a tour of the business's presence and capability across the area. Build it from these modules, **in this order**. Every H2/H3 should carry the primary keyword or a close variant wherever it reads naturally (see Heading SEO below).

**1. Services Offered in [Location]** — Comes first, straight after the opening paragraph and CTA. Lead with capability, not backstory — the reader wants to know fast whether this business does what they need before they'll read anything else. **Always a bulleted list**, not prose paragraphs — a wall of service paragraphs is hard to skim, and skimmability is the point of this section. This is also the section doing the heavy lifting on the client's secondary keywords — each service named is a natural home for its own keyword.

**Keep every service bullet the same depth.** Two sentences per service is the standard: one sentence on what the service covers, one earned detail (a method, material, or local condition specific to this business or this location). Don't give some services three sentences and others one line — an uneven page reads like some services were an afterthought, even when that's not the intent. If a particular service genuinely needs more room (a complex or highly technical offering), that's a sign it might deserve its own section rather than special-cased bullet length.

**Link the service name (or a relevant keyword phrase) once within each bullet**, worked into the sentence rather than bolted on as a separate "click here." If the client's sitemap or knowledge base gives a confirmed URL for that service, use it directly in the docx as an actual hyperlink (see Internal Linking below).

**2. Why Choose [Business Name] in [Location]** — Trust and local familiarity, once capability has already been established. Open with the strongest verifiable credential, answer-first (see AIO Rule 1). Years serving the area, licensing, guarantees, local reviews/reputation if available. Anchor superlative claims to something specific (see Self-Proclaimed Claims above).

Directly under this heading, include a **Trust Signals block** — **a tight bullet list of label/value pairs** (Years Active, Licence/Registration, Warranty, Memberships/Certifications), pulling only confirmed facts from the client knowledge base or the client's site. Use a bold label followed by an em dash and the value, one per bullet — not a table. Tables read as cold and clinical in a "Why Choose" section where the goal is still to build trust with a human reader, not just hand AI extraction tools a data block; a bullet list gives the same scannability without that effect. This gives both human readers and AI extraction tools a single scannable block of the business's core credentials, rather than requiring them to piece it together from prose. See AIO Rules 2 and 3 for what counts as a usable signal and how to verify it before publishing.

**3. Local Overview** — What makes this location itself worth writing about, now that the reader knows what the business can do for them. This is where the strongest earned local detail lives: property types common to the area, growth corridors, older vs newer housing stock, coastal or bushfire-zone considerations, anything that could not be copy-pasted onto a page for a different suburb. This section comes after services and trust, not straight after the opener — a reader who hasn't yet confirmed the business does what they need doesn't want a suburb history lesson first.

**4. Also Servicing [Nearby Suburbs / Region]** (where relevant) — If the business serves this location plus surrounding suburbs, list them here, later in the page once the primary location's case has been made. Avoid a heading built around "Areas Near [Location] [Business] Also Services" — stacking location name, business name, and "also" back-to-back reads awkwardly out loud. Prefer a cleaner construction: *Also Servicing Nearby Suburbs*, *[Business Name]'s Wider Service Area*, or *Suburbs Near [Location] We Also Cover*. This section is often the most natural home for secondary location keywords.

**5. Pricing / How It Works** (optional but recommended on longer pages) — A short, honest section on how quoting and pricing work. Never state specific prices — route to a quote CTA.

### Closing CTA Paragraph

Three to four lines, persuasive tone, sitting just before the FAQs. This is a required element of every location page, not optional. Summarise the value of choosing this business in this location and create a clear, low-friction next step. Add a sense of urgency where it's genuinely earned by the service (not manufactured).

**Example tone:** *"It's crucial to have a reliable [trade] on your side. For fast, dependable [service] across [Location], contact [Business Name] today and get the job done right the first time."*

Follow immediately with a **Closing Summary + CTA** line — one short, direct sentence.

**Example:** *"Ready to upgrade your home's lighting? Call us today!"*

### FAQs

4–6 questions, phrased exactly as a person would type or say them. See FAQ Research Process below — do not write these from memory alone.

---

## Heading SEO Rules

- Primary keyword in the H1 (required)
- Primary keyword in at least one further H2 or H3 (minimum — on a page this length, aim higher where it reads naturally, similar to the density guidance above)
- Proper heading hierarchy: H1 → H2 → H3, no skipping levels
- Every heading avoids a full stop and uses Title Case
- The FAQ heading should carry the service or location keyword, not just "FAQs"

---

## CTA Guidelines

There are two distinct CTA formats. Which one to use depends on where the CTA sends the reader — never mix the two treatments together.

### Form-Directed CTAs

Use this format when the CTA sends the reader to a contact page, quote form, or booking page rather than triggering a call.

- **Text only** — a short, bold, hyperlinked line. No phone number attached.
- Link straight to the confirmed contact/quote page URL from the client's site or knowledge base
- Vary the wording across every instance on the page — don't reuse the same phrase twice. Examples: *Get a Fast, No-Obligation Quote* / *Book a [Location] Site Visit* / *Discuss Your Renovation Plans* / *Request a Tailored Quote*
- Outcome-focused and specific — never a bare "Contact Us"

### Call CTAs

Use this format when the CTA's purpose is to get the reader to pick up the phone.

- A short, bold **question** immediately above the number — e.g. *"Ready to Get Started on Your [Location] Renovation?"* or *"Want to Lock In a Site Visit?"*
- The phone number sits on its own line directly under the question, styled to stand out as a button (shaded background block, centred, bold) — not folded into a sentence like "Call us on 0401 762 108 today"
- Never embed the phone number in body copy prose elsewhere on the page — it belongs only inside this button element

### General Rules

- **Minimum two CTAs** across the page — this is a hard floor for location pages, lighter than the frequency expected on a shorter, faster-converting service page
- One of the two must be the **Closing CTA Paragraph** (three to four lines, persuasive tone, see above)
- Use a mix of both formats across the page rather than defaulting to one — e.g. a call CTA after the opener, a form CTA after Services, a form CTA after Why Choose, a call CTA after the quote-process section
- No emojis in CTAs or anywhere else on the page

---

## Internal Linking

| Word Count | Internal Links |
|---|---|
| 500 or fewer | 2–3 |
| 501–999 | 4–5 |
| 1000–2000 | 6–10 |
| 2001–4000 | 11–15 |

A 1000–1500 word location page should land in the 6–10 link range.

**Link every service named in "Services Offered" inline, not just in a reference table.** Each service bullet or descriptor should carry a real hyperlink on its service name straight to that service's page, using descriptive anchor text (the service name itself, not "click here" or "learn more"). If the client's sitemap or knowledge base gives a confirmed URL for that service, use it directly in the docx as an actual hyperlink. Link any neighbouring location pages named in the "Also Servicing" section the same way where URLs are known.

Only fall back to a suggested-links table at the foot of the deliverable for links whose destination page doesn't exist yet or can't be confirmed — that table exists so the developer knows what still needs linking once the target page is built, not as a substitute for linking what's already known. On a page where every service link is confirmable, the table should be short or empty.

Add 1–2 external links to reputable local-area sources — a council website or a suburb demographic/community profile are the standard picks. These strengthen the page's earned local detail (see Writing Quality Rules) and give AI extraction tools an authoritative source to associate with the location claims. Source these yourself via web search — don't ask the user to supply them. Search for the relevant council site and a suburb profile (e.g. a `.id community` profile or equivalent), verify the URL actually resolves, and use it to check or source a genuine local-area fact (housing era, population, boundaries) rather than linking decoratively. Flag every external link in the suggested-links table for the team to verify before publishing — sourcing them doesn't replace a human check.

An external link isn't required on every page if nothing genuinely strengthens a claim, but for a location page specifically, a council or suburb-profile link is the norm rather than the exception, since the earned local detail these pages depend on usually benefits from a citable source.

---

## Secondary Keyword Usage

- Aim to include every secondary keyword provided at least once — not mandatory for every single one, but target as many as will sit naturally
- Never force a secondary keyword into a sentence that wasn't going to say that anyway — this is the same mechanical-insertion problem covered below, just at the secondary-keyword level
- Secondary keywords belong most naturally in the "Services Offered" and "Area Coverage" sections, and in headings (H2–H3) where they fit

---

## Writing Quality Rules

These govern how the copy reads at the sentence level. SEO compliance does not excuse poor writing — a sentence that satisfies a keyword rule but reads awkwardly must be rewritten until it does both.

### Sentence Rhythm

Vary sentence length within every paragraph. A short declarative, then a longer explanatory sentence, then a mid-length close is the natural reading rhythm.

**Flat:** "Melbourne has many older homes. These homes often have ageing pipework. This can cause plumbing issues."
**Better:** "Melbourne's older suburbs are full of character homes — and ageing pipework to match. In streets where clay or galvanised steel pipe is still common underground, plumbing issues tend to surface as properties pass the 40- and 50-year mark."

### No Mechanical Keyword Insertion

Keyword and location mentions must fit a sentence that would already be well-written without them.

**Mechanical:** "For plumbers in Melbourne, plumbing issues should be handled quickly because they can affect the home."
**Natural:** "In Melbourne's inner suburbs, where much of the housing stock predates the 1970s, ageing pipework is one of the most common reasons homeowners call in a plumber."

### Earned Local Detail

Every location mention must attach to something specific and useful — not exist purely to satisfy an entity-consistency count.

**Decorative (avoid):** "For homeowners in Carrum Downs, this service is available today."
**Earned:** "In Carrum Downs, established tree coverage in older streetscapes is a common source of root intrusion into clay sewer lines."

### Section Openers and Closing Lines

The first sentence of a section shouldn't restate the heading — open with the most useful or specific thing the reader needs to know. The last sentence of a section is the highest-value sentence in it — don't waste it on a generic "the team is here to help." Advance the reader's thinking or pivot naturally to a CTA.

### USP Repetition

Every core credential (years active, warranty terms, licensing, memberships) should have exactly one home on the page — the Trust Signals block under Why Choose. Don't restate the same USP in the opening paragraph, then again in Why Choose, then again in the closing paragraph — that's the most common repetition failure on these pages, because the same handful of standout facts feel too good not to mention everywhere. Once a fact has been stated in the Trust Signals block, the opening paragraph and closing paragraph should draw on different material: service breadth, the quote process, or a location-specific detail, not the same credential restated in slightly different words. Before finalising a page, scan it specifically for phrases that reappear (a warranty length, a founding year, a certification name) and cut all but the strongest instance.

---

## AIO Optimisation Rules

Apply to every page — this is what gets a location page surfaced and cited correctly by Google AI Overviews, ChatGPT Search, Perplexity, and similar tools. AI systems extract and cite in very specific ways: they pull isolated facts, they favour content already broken into scannable structure, and they weight verifiable credentials over adjectives. The rules below are written to that behaviour.

### 1. Answer-First Structure

The first sentence of every section — H2, H3, and FAQ answer alike — must contain the actual fact or answer, not lead-up. If a reader (or an AI model) only ever read first sentences down the page, they should walk away with the core facts of the business's Maidstone-equivalent offer intact.

**Answer-first (do this):** "SilverPeak Construction has held Master Builders Victoria membership since 2012 and completes bathroom renovations under a written four-week guarantee."
**Buried (avoid):** "When it comes to choosing a renovation partner, there's a lot to consider, but one thing that sets SilverPeak apart is their Master Builders Victoria membership."

This applies at the section level (don't build up to the point across three sentences) and at the page level (don't save the strongest trust signals for the last paragraph).

### 2. Factual Stats and Trust Signals

Every location page needs a set of specific, checkable facts — not adjectives standing in for them. Pull these from the client knowledge base or the client's own site; never invent a number, a year, or a credential that isn't confirmed. At minimum, surface:

- **Time in business** (years active, founding year)
- **Warranty or guarantee terms** (exact length and what it covers)
- **Licensing and registration** (licence number and issuing body, e.g. Victorian Building Authority, NDIS registration)
- **Industry memberships** (e.g. Master Builders Association/Victoria)
- **Specific certifications** (e.g. "certified wedi installer" — a named, checkable qualification beats a generic "quality tradespeople" every time)
- **Scale/volume signals where available** (e.g. "55+ bathroom renovations a year") — only if the client has actually provided or confirmed the figure

These signals shouldn't all live in one paragraph — spread them across Why Choose, the opening paragraph, and the closing CTA paragraph so each section carries at least one concrete, citable fact rather than a general trust statement.

### 3. Structured Formatting

AI extraction tools favour content that's already broken into a scannable shape over dense prose, because it's easier to lift cleanly. On every location page:

- Use the **bullet list** in Services Offered rather than folding services into a paragraph
- Include a **Trust Signals block** directly under the Why Choose heading — a tight bullet list of label/value pairs (Years Active, Licence/Registration, Warranty, Memberships) so the page's core credentials sit in one extractable block rather than scattered through prose. Bullet list only, never a table — see the Why Choose module for the exact format.
- Keep the **FAQ section** as clean question/answer pairs — this is naturally the highest-value structured content on the page for AI extraction, so don't compress it into fewer, denser questions to save space
- Any comparison or feature list (e.g. what's included in a bathroom renovation) should be an actual bulleted list, not a run-on sentence

### 4. E-E-A-T and Verification

Every trust claim on the page should be traceable to something real — this is what separates a page AI models are willing to cite from one they treat as unverifiable marketing copy.

- Prefer **named, specific credentials** over general trust adjectives: "NDIS-registered builder" and "certified wedi installer" carry verification weight; "trusted and reliable" doesn't, on its own
- Where the client has a licence number, membership number, or registration ID, include it (in the deliverable, flag to the PM whether it's safe to publish this publicly or whether it should be confirmed first)
- Attribute claims accurately — years active, service area breadth, and guarantee terms should match what's confirmed in the client knowledge base or the client's live site, not be rounded up or embellished
- If a fact can't be verified from the client knowledge base, onboarding form, or the client's own site, leave it out rather than writing around it with a vaguer claim

### 5. Entity Consistency

Mention business name, service range, and location together at least once every 150–200 words, and make sure every instance passes the earned-detail test above (Writing Quality Rules) — a fact-dense page still needs to read naturally, not like a citation list.

### 6. Question-Based Headings

At least 1–2 headings phrased as real search queries — this is lighter than a service page's 2–3, since a location page carries more sections overall, and it doesn't need to apply to every section. Pick the sections where a question genuinely fits the content (Why Choose and How Quotes Work are natural candidates) and leave the rest as statements — forcing every heading into question form reads gimmicky.

**Statement:** *Why Choose SilverPeak Construction for Renovations in Maidstone*
**Question, answered first:** *Why Choose SilverPeak Construction for Your Maidstone Renovation?* followed immediately by the strongest verifiable credential as the first sentence — not a rhetorical build-up.

Self-contained paragraphs — each one should make sense read in isolation, without needing the paragraph before it for context.

### 7. FAQ Optimisation

Phrase every question as a person would type or say it; each answer complete in 2–3 sentences, answer-first per Rule 1; no pricing specifics, always route cost questions to a quote CTA.

---

## FAQ Research Process

Before writing FAQs, conduct web research to identify the most commonly searched questions for this trade and location combination in Australia. Do not write FAQs from memory alone.

1. Web search: "[trade] frequently asked questions [location/region] Australia"
2. Review competitor location pages in the same area for the questions they're answering
3. Cross-reference against the client's keyword list — question-based or long-tail terms often signal a real FAQ opportunity
4. Select the 4–6 questions with the strongest real-world relevance to this location and this business's service range

**FAQ writing rules:**
- Phrase every question exactly as a person would type or speak it
- Each answer: 2–3 sentences, complete and standalone
- Naturally integrate the primary keyword and location into at least 2–3 answers
- No specific pricing — route cost questions to a quote CTA
- Cover as a minimum: response time/coverage, service range, how pricing and quotes work, and one local-relevance question specific to the area

---

## Client Review

Every location page deliverable ends with a sign-off line, matching the TWG template:

> **Client Has Reviewed (please tick):** ☐

Note in the deliverable that once the client has completed their review of all pages in a batch, TWG emails support@tradiewebguys.com.au to confirm.

---

## Final Output Checklist

Run through every item below before marking any location page done and before it goes to the client for review. In a batch, complete it for each location before moving to the next — don't batch the check at the end. If any box can't be ticked, fix the page, don't note the exception and move on.

### Structure and Order

- [ ] Services Offered comes first in the body, straight after the opener — before Why Choose, Local Overview, and Also Servicing
- [ ] Why Choose (with Trust Signals block) comes before Local Overview
- [ ] Also Servicing / wider service area sits later in the page, not straight after the opener
- [ ] The nearby-suburbs heading avoids stacking location + business name + "also" into one awkward phrase
- [ ] Closing CTA Paragraph (three to four lines) sits just before the FAQs
- [ ] Client review sign-off line included at the foot of the deliverable

### Services Offered

- [ ] Presented as a bulleted list, not prose paragraphs
- [ ] Every service bullet is the same depth — two sentences each, no service given three sentences while others get one
- [ ] Each service name (or a relevant keyword phrase) is linked once within the body of its own bullet, not bolted on separately
- [ ] Each linked service points to a confirmed, real URL — never a guessed or invented one

### Why Choose / Trust Signals

- [ ] Trust Signals block is a bullet list (bold label — value), never a table
- [ ] Every fact in it is confirmed from the client knowledge base or the client's own site — nothing invented, assumed, or rounded up
- [ ] Named, specific credentials used instead of generic trust adjectives wherever a real credential exists (e.g. "NDIS-registered provider," not just "trusted")
- [ ] No self-proclaimed superlative claims ("#1," "best in [location]") anywhere on the page

### CTAs

- [ ] Minimum two CTAs, including the Closing CTA Paragraph
- [ ] Form-directed CTAs are text-only, bold, linked to a confirmed contact/quote URL, with no phone number attached
- [ ] Call CTAs pair a short bold question with the phone number styled as a standalone button — never folded into a sentence
- [ ] CTA wording varies across every instance — no phrase reused twice
- [ ] Phone number appears only inside call-CTA button elements, never elsewhere in body copy

### Repetition and Writing Quality

- [ ] Every paragraph varies in sentence length
- [ ] No mechanical keyword insertions — every keyword and location mention is attached to a specific, useful idea
- [ ] The Local Overview section contains at least one earned detail that couldn't be copy-pasted to a different suburb's page
- [ ] No section opener restates its heading; no section closer is a generic wrap-up
- [ ] Core credentials (years active, warranty, licensing, memberships) appear once, in the Trust Signals block — not restated in the opener, Why Choose prose, and closing paragraph
- [ ] Scanned the full page for any other repeated phrase or fact and cut all but the strongest instance

### Headings

- [ ] 1–2 headings phrased as genuine questions, applied only where it fits naturally — not forced onto every section
- [ ] Every question-based heading is answered directly in its first sentence, not built up to
- [ ] Every section (not just question headings) opens with the answer or key fact, not a lead-up (Answer-First)
- [ ] No full stops on headings; Title Case throughout
- [ ] Primary keyword in H1 and at least one further H2/H3
- [ ] FAQ heading carries the service or location keyword, not just "FAQs"

### Links

- [ ] Internal links added per the word-count table (6–10 for a typical 1000–1500 word page)
- [ ] Every service named in Services Offered carries an actual inline hyperlink — not just an entry in the suggested-links table
- [ ] 1–2 external links to a reputable local-area source (council site, suburb/community profile) sourced via web search, with URLs verified to actually resolve
- [ ] Every external link is tied to a genuine local fact it supports, not placed decoratively
- [ ] Suggested-links table only lists links that couldn't be confirmed yet — not used as a substitute for linking what's already known
- [ ] All external and uncertain links flagged for team verification before publishing

### SEO Fundamentals

- [ ] Primary keyword in meta title and meta description
- [ ] Primary keyword in the first paragraph
- [ ] Primary keyword density roughly 1x per 250–300 words
- [ ] Secondary keywords used 1–2 times each, spread across the page, not stuffed
- [ ] Word count in the 1000–1500 range
- [ ] URL slug under 100 characters, doesn't repeat a keyword already in the domain

### AIO and E-E-A-T

- [ ] Opening paragraph answers the implied search query in the first 2 sentences
- [ ] Each paragraph is self-contained and readable in isolation
- [ ] Business name + service range + location appear together every 150–200 words, each instance earning its place
- [ ] Every trust claim is traceable to the client knowledge base or the client's own site
- [ ] FAQs formatted as clean, distinct question/answer pairs — not compressed to save space
- [ ] FAQs phrased as natural search queries with complete, answer-first standalone answers

### Final Polish

- [ ] No emojis anywhere — headings, bullets, CTAs, or body text
- [ ] No passive voice, no filler
- [ ] Australian English throughout
- [ ] Evergreen framing throughout (no owner-name dependency)
