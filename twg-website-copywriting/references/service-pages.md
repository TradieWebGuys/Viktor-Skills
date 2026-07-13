# Service Pages - Structure And Rules

Read `SKILL.md` and `client-kb.md` before using this file.

This file covers the structure, section order, and module logic for trade service pages.

The goal is not to fill a rigid template. The goal is to build a page that answers the buyer's real questions in the right order.

---

## Core Service Page Principle

A good service page should quickly answer:

1. Does this business handle the job I need?
2. Why should I trust them?
3. Is there proof?
4. Does this apply to my situation?
5. What happens next?

For most non-emergency services, capability should come before self-identification.

Self-identification moves earlier only when the reader arrives with an urgent symptom, obvious fault, or stressful issue that needs fast confirmation.

---

## Reader State Profiles

Identify the reader state before writing the opening or choosing the page order.

### 1. Emergency / Reactive

**Reader state:** stressed, wants help now  
**Register:** calm, urgent, practical  
**Opening angle:** what to do first, then help available

Examples:

- Emergency plumber
- Burst pipe
- Severe water leak
- Sewage overflow
- No power
- Electrical burning smell
- Exposed wiring
- Storm roof damage
- Active roof leak
- Solar system sparking or smoke

Recommended order:

1. Opening
2. What To Do First or Self-Identification
3. Capability
4. Trust
5. Proof
6. Close
7. FAQs

---

### 2. Diagnostic / Frustrated

**Reader state:** something is wrong and they want a clear fix  
**Register:** direct, diagnostic, solution-focused  
**Opening angle:** what the issue usually turns out to be once properly assessed

Examples:

- Blocked drains
- Hot water faults
- Recurring leaks
- Drainage problems
- Flickering lights
- Tripping circuits
- Poor solar output
- Ongoing roof leaks

Recommended order:

1. Opening
2. Self-Identification or Diagnostic Explanation
3. Capability
4. Trust
5. Proof
6. Process or Decision Support
7. Close
8. FAQs

---

### 3. Educational / Cautious

**Reader state:** researching before committing  
**Register:** considered, clear, evidence-led  
**Opening angle:** what the service involves and why the right method matters

Examples:

- Switchboard upgrades
- EV charger installation
- Pipe relining
- Water filtration
- Solar battery installation
- Smart home systems
- Roof replacement material choice

Recommended order:

1. Opening
2. Capability
3. Trust
4. Proof
5. Process
6. Decision Support
7. Self-Identification, if helpful
8. Close
9. FAQs

---

### 4. Compliance / Safety-Focused

**Reader state:** cautious and wants the job done correctly  
**Register:** serious, practical, certification-led  
**Opening angle:** licensed work, safety, and compliance confidence

Examples:

- Switchboard upgrades
- RCD safety switch installation
- Smoke alarm compliance
- Electrical safety inspections
- Gas appliance installation
- Backflow prevention
- Grid-connected solar
- Working-at-heights services

Recommended order:

1. Opening
2. Capability
3. Compliance / Licensing
4. Trust
5. Proof
6. Process
7. Decision Support
8. Close
9. FAQs

Self-identification can appear earlier only if the page targets a fault or urgent compliance failure.

---

### 5. Consultative / Planning

**Reader state:** planning a larger investment  
**Register:** scope-led, advisory, commercially aware  
**Opening angle:** project scope and capability first

Examples:

- Bathroom renovation plumbing
- Kitchen renovation electrical
- New home electrical
- Full rewire
- Full roof replacement
- Commercial solar system installation
- Drainage redesign
- HVAC system replacement

Recommended order:

1. Opening
2. Capability
3. Trust
4. Proof
5. Process
6. Decision Support
7. Visual Proof, if relevant
8. Close
9. FAQs

---

### 6. Maintenance / Routine

**Reader state:** organised, not usually urgent  
**Register:** practical, reassuring, comprehensive  
**Opening angle:** what is checked, serviced, prevented, or kept compliant

Examples:

- Electrical safety checks
- Smoke alarm testing
- Roof inspections
- Gutter cleaning
- Solar panel cleaning
- HVAC servicing
- General plumbing maintenance

Recommended order:

1. Opening
2. Capability
3. Trust
4. Proof
5. Process
6. Decision Support, if helpful
7. Close
8. FAQs

---

## Opening Entry Point Rotation

Use a different opening entry point across batches so pages do not feel cloned.

1. **Symptom-led:** opens with the problem the reader notices
2. **Consequence-led:** opens with what can happen if the issue sits too long
3. **Diagnostic-led:** opens with what the issue often turns out to be
4. **Reassurance-led:** opens by removing a fear or misconception
5. **Local context-led:** opens with a property type, infrastructure era, climate, network, or local condition
6. **Decision-led:** opens with the choice the reader is trying to make

The first sentence must still be reader-first. Technical detail should not lead unless the audience is highly technical.

---

## H2 Tagline Variation

The H2 directly under the H1 should give a strong reason to keep reading.

Rotate construction across batches.

- **Outcome-led:** Safer Power, Modern Protection, And Clear Certification
- **Question-led:** Not Sure If The Existing Board Is Still Safe?
- **USP-led:** Level 2 Electrical Work, Full Testing, And Written Certification
- **Specificity-led:** Ceramic Fuse Boards, RCD Protection, And Supply-Side Upgrades
- **Planning-led:** Upgrade The Board Before Adding Higher-Load Appliances
- **Compliance-led:** Licensed Electrical Upgrades For Safer, Compliant Properties

Do not force the location into this line unless it reads naturally.

For cautious or educational readers, the H2 tagline should be benefit-first before it becomes technical.

Avoid turning the tagline into a list of components, regulations, or technical inclusions. One specific detail is useful. Three or more technical details can make the page feel dense before the reader has settled into the copy.

Better:

- Safer Power, Modern Protection, And Clear Certification
- RCD Protection, Level 2 Support, And Clear Certification

Too dense:

- Ceramic Fuse Board Replacement, RCD Protection, Essential Energy Coordination, Testing, And Certification

---

## Page Structure

### Metadata Block

Add this table at the top of every deliverable for developer reference.

| Field | Detail |
|---|---|
| Page Title |  |
| Business Name | Pull from `client-kb.md` |
| Location | Pull from `client-kb.md` |
| Target Audience | Pull from brief or `client-kb.md` |
| Reader State | Emergency, Diagnostic, Educational, Compliance, Consultative, or Maintenance |
| Primary Keyword | Pull from brief or `client-kb.md` |
| Secondary Keywords | Pull from brief or `client-kb.md` |
| Word Count Target | Match service complexity |
| URL Slug | Use primary keyword and location where natural |
| Meta Title | Primary keyword + location + business name if space allows |
| Meta Description | Benefit-led, includes primary keyword and location naturally |
| Visual Module | Yes, no, or conditional placeholder |
| Proof Module | Review widget, testimonial, project snippet, gallery, or placeholder |

---

### H1

Use Title Case. Include the primary keyword and primary location.

The H1 is the main place to use the exact service and location pairing. Do not rely on repeated H2 location mentions to create relevance.

---

### H2 Tagline

Place directly under the H1.

Use one sentence. Make it benefit-led, specific, and readable. The tagline can mention a licence, warranty, method, result, or buyer concern.

---

### Opening Paragraph

50-90 words.

The opening should:

- Start with the reader's situation
- Introduce the business, service, and location naturally
- Include one earned local, technical, or compliance detail
- Avoid overloading the first sentence with keywords
- Lead directly into the first CTA

Follow with the first CTA.

### Opening Softness Rule

For Educational, Cautious, Compliance, Upgrade, and Planning reader states, the opening should create confidence before introducing risk.

Do not open with a worst-case consequence, technical component, regulation, historical era, or fault scenario unless the reader is in an emergency or reactive state.

The first sentence should be simple and buyer-facing. Technical or compliance details can appear in the second or third sentence, but only one earned technical detail should appear in the opening paragraph.

Better opening pattern:

1. Start with the reader's situation, concern, or decision.
2. Introduce the business, service, and location.
3. Add one useful technical, local, or compliance detail.
4. Move into a low-pressure CTA.

Avoid stacking multiple technical or risk details in the opening, such as board age, fault risk, RCD protection, network authority requirements, and certification all in one paragraph.

---

## Heading SEO Rules

Optimise headings without making them sound repetitive.

### Required

- Primary keyword in H1
- Primary keyword or close variant in at least one H2
- Location in H1
- Location in at least one H2 only if useful
- FAQ heading includes the service topic
- Natural service variants in H3s where needed

### Avoid

- Repeating `[service] in [location]` across multiple H2s
- Adding the location to a heading when the heading already works better without it
- Stuffing every H2 with the primary keyword
- Writing headings for search engines instead of readers

### Better Heading Patterns

- Switchboard Upgrade Services
- Why Choose Electric East For Switchboard Upgrades
- What Happens During A Switchboard Upgrade?
- Is It Worth Replacing An Old Switchboard?
- Signs Your Switchboard Needs Replacing
- Switchboard Upgrade FAQs

### When Location Belongs In A Heading

Use the location in a heading when it helps clarify service area, pricing, local infrastructure, local compliance, or local availability.

Good examples:

- Switchboard Upgrades In Ballina And The Northern Rivers
- How Much Does A Switchboard Upgrade Cost In Ballina?
- Level 2 Electrical Work Across The Northern Rivers

Weak examples:

- Why Choose Electric East For Switchboard Upgrades In Ballina
- Book Your Switchboard Upgrade In Ballina Today
- Signs You Need A Switchboard Upgrade In Ballina

---

## Core Modules

A service page is built from modules. Use the order that best matches the reader state.

### Local Density Check
- Primary location remains dominant when the page targets one suburb or town
- Regional and nearby area mentions are contained to useful sections, not scattered through the page

---

### Module 1 - Capability

**Purpose:** show the reader the business handles their job.

For most services, capability should appear before self-identification.

Use:

- 1-2 sentence intro with earned detail
- A scannable list of 5-7 services, inclusions, or scenarios
- H3s for sub-services if the page covers multiple service types
- Plain explanations of what the business actually does

Example structure:

## Switchboard Upgrade Services

The right upgrade depends on the age of the existing board, the number of circuits, and whether the property needs metering or supply-side work. Electric East Electricians can assess the current setup, replace outdated components, install modern protection, and complete the required testing and certification.

- **Full switchboard replacement** - old boards replaced with modern circuit protection and clearer circuit organisation.
- **RCD safety switch installation** - protection added where the board can safely support it.
- **Circuit additions** - dedicated circuits added for higher-load appliances where required.
- **Level 2 electrical work** - metering and supply-side work handled by an accredited provider where applicable.

---

### Module 2 - Trust Benefits

**Purpose:** make the reader confident enough to keep considering the business.

Use scannable benefit points instead of one dense paragraph when the client has several strong USPs.

Recommended format:

## Why Choose [Business Name] For [Service]

- **Licensed and accredited** - explain what the licence allows the business to handle.
- **Clear written quotes** - explain how the reader avoids confusion.
- **Warranty or certification** - explain what documentation is provided.
- **Relevant experience** - connect years, trade background, or project type to the service.
- **Local service coverage** - mention the service area without forcing the heading.

Rules:

- Each point needs a short benefit, not just a label.
- Keep each point to one concise line where possible.
- Aim for 8-16 words after the bold lead-in.
- Do not turn each USP into a full explanatory sentence.
- Use 4-5 points for most pages. Use 6 only when every point is genuinely strong.
- Do not include a USP unless it is confirmed.
- Avoid repeating the same sentence structure across every point.

### Trust Benefit Length Rule

Keep the Why Choose section tight.

Each point should be a short benefit statement, not a full paragraph. Aim for 8-16 words after the bold lead-in. Expand only when the detail genuinely changes the buyer's decision.

The section should be easy to scan in under 10 seconds.

Better:

- **Level 2 ASP accredited** - metering and supply-side work handled in-house.
- **Written quotes** - clear scope and pricing before work begins.
- **Compliance paperwork** - certificates issued where required after testing.

Too long:

- **Level 2 ASP accredited** - metering, supply-side work, and Essential Energy applications handled in-house. The full scope of the upgrade stays with one licensed team from assessment to certification.

---

### Module 3 - Proof

**Purpose:** back up the trust claims.

Proof should appear on most service pages.

Use the strongest available proof type:

1. Review widget placeholder
2. Testimonial placeholder
3. Project gallery placeholder
4. Case study snippet
5. Before and after placeholder, if visually relevant
6. Accreditation, warranty, or certification proof

Recommended heading examples:

- Recent Customer Feedback
- Reviews From Local Property Owners
- Recent [Service] Projects
- See The Difference A Proper Upgrade Makes

Example placeholder:

## Recent Customer Feedback

[Reviews Widget Placeholder]

Property owners across [service area] use [Business Name] for [service], safety work, and related electrical projects. Add recent reviews here to support the service claims and give visitors confidence before they enquire.

Do not invent testimonials. Use placeholders when live website assets will be added later.

---

### Module 4 - Visual Proof, Conditional

**Purpose:** show a visible result when imagery helps the buyer decide.

Only include before and after, gallery, or project image placeholders when the service has a visible outcome.

Strong fit:

- Renovations
- Re-roofing
- Solar installations
- Switchboard upgrades
- EV charger installations
- Landscaping
- Concrete and paving
- Shop fit-outs
- Bathroom, laundry, and kitchen work

Usually not required:

- Fault finding
- Leak detection
- Compliance testing
- Backflow testing
- Gas servicing
- Minor repairs
- Emergency attendance

Example placeholder:

## Recent [Service] Work

[Project Gallery Placeholder]

Use this section only if project photos help the buyer understand the standard of the finished work, the type of properties serviced, or the before and after difference.

---

### Module 5 - Self-Identification

**Purpose:** help the reader recognise whether the service applies to them.

Self-identification does not always need to appear before capability. Place it based on the reader state.

Use early when:

- The reader arrives with an urgent symptom
- The problem is stressful or disruptive
- The service is fault-based
- The reader needs fast confirmation

Use later when:

- The service is planned
- The service is compliance-based
- The reader is comparing providers
- The page needs to prove capability first

Recommended format:

## Signs Your [System] May Need [Service]

Intro sentence, then 4-6 clear warning signs.

Rules:

- Each item should stand alone.
- Avoid fear-heavy wording unless the risk is real and confirmed.
- Mention inspection where the issue cannot be confirmed visually.
- Do not repeat the same point in the FAQs.

---

### Module 6 - Decision Support

**Purpose:** help the reader make a better choice.

This replaces mandatory pricing or objection sections.

Use this module only when it benefits the reader.

Good decision-support angles:

- Is repair or replacement the better option?
- Is the upgrade worth doing now?
- What affects the cost?
- What changes if the property is rented?
- What should be done before adding EV charging, solar, air conditioning, or higher-load appliances?
- Which system type suits the property?

Cost can appear here when it helps. Do not invent numbers. Do not use dollar figures or ranges unless the client has confirmed fixed pricing in writing. For variable-scope trade work, the only correct framing is what affects the quote, not what it costs.

Better than a generic cost section:

## What Affects The Cost Of A Switchboard Upgrade?

The cost depends on the board's condition, the number of circuits, whether asbestos backing is present, and whether network-side work is required. A written quote should confirm the scope before work begins, including testing, certification, and any required supply authority coordination.

---

### Module 7 - Process

**Purpose:** remove uncertainty about what happens next.

Useful for:

- Upgrade services
- Installation services
- Compliance work
- Larger jobs
- Services with downtime, access needs, staged work, or certification

Recommended format:

## What Happens During A [Service]?

1. Existing system assessed
2. Scope and quote confirmed
3. Work completed by the licensed trade
4. Testing and checks completed
5. Documentation, warranty, or certificate provided where applicable

Keep it short. Process sections should reduce uncertainty, not slow the page down.

---

### Module 8 - Compliance / Licensing

**Purpose:** explain safety, certification, licensing, or authority requirements.

Use when the service involves legal, electrical, gas, solar, roofing safety, plumbing, or rental compliance requirements.

Rules:

- Only include confirmed licences and accreditations.
- Do not overstate what a licence allows.
- Mention certificates or warranties only when confirmed.
- Explain why the detail matters to the property owner.

---

### Module 9 - Close

**Purpose:** bring the reader to the final decision.

Use 2-3 sentences.

The close should:

- Restate the reader's problem or goal
- Show the outcome of acting
- Reinforce one major trust or proof point
- Lead into the final CTA

Avoid summarising the page. End with a clear reason to act.

---

## Optional Module Selection Guide

Use optional modules based on the service, not because the template needs more content.

| Service Type | Recommended Optional Modules |
|---|---|
| Emergency | What To Do First, Self-Identification |
| Fault-based | Self-Identification, Process |
| Installation | Process, Visual Proof, Decision Support |
| Upgrade | Process, Decision Support, Visual Proof |
| Compliance | Compliance / Licensing, Process, Proof |
| Renovation | Capability, Process, Visual Proof, Proof |
| Solar | Decision Support, Process, Visual Proof |
| Roofing | Visual Proof, Process, Decision Support |
| Maintenance | Process, Proof |

---

## Pricing And Objections

Do not include a pricing section by default.

Include pricing only when:

- The keyword set includes cost terms
- The reader genuinely needs cost context to decide
- The client has approved pricing language
- The section explains what affects the quote rather than pretending every job is the same

Do not use dollar figures or ranges unless the client has confirmed fixed pricing in writing. Trade work is variable by nature — scope, materials, site conditions, and client choices all affect the final cost. The correct approach is always to explain what influences the quote and direct the reader to request one.

Use headings such as:

- What Affects The Cost Of [Service]?
- What Should Be Included In A [Service] Quote?
- Is It Worth [Repairing/Replacing/Upgrading]?

Do not use pricing as filler.

---

## CTA Placement

Place CTAs where they match conviction points.

Recommended placements:

1. After the opening
2. After capability
3. After trust and proof
4. After process or decision support
5. Final close

Use fewer CTAs on shorter pages if the page flows better. Repetition can reduce trust.

CTA wording should vary based on the moment.

Examples:

- Request A Switchboard Assessment
- Book A Licensed Electrician
- Ask For A Written Quote
- Speak With A Level 2 Electrician
- Arrange A Safety Check

Use the client's preferred CTA wording and contact method from `client-kb.md`.

### CTA Channel Variation

Use a mix of phone-based and form-based CTAs where the client supports both.

For cautious, educational, compliance, planning, or higher-cost services, include at least one lower-pressure form CTA because the reader may not be ready to call immediately.

Examples:

- Enquire Now
- Request A Quote
- Request A Switchboard Assessment
- Send An Enquiry
- Ask For A Written Quote
- Book An Assessment

Use phone CTAs when urgency, safety, or fast action matters.

Use form CTAs after the opening, after decision-support sections, or in the final close when the reader may want to provide details before speaking with the business.

---

## FAQs

Include 4-6 FAQs at the end of every service page.

Heading examples:

- Switchboard Upgrade FAQs
- Frequently Asked Questions About Switchboard Upgrades
- Questions About [Service]

### FAQ Research Method

Research real buyer questions before writing FAQs. Do not write from memory or default to a fixed template.

Research steps:

1. Search "[service] frequently asked questions Australia" and review the People Also Ask results in Google.
2. Check the client's keyword sheet — ungrouped long-tail keywords often represent question-based searches.
3. Review competitor FAQ sections in Australian markets for the same service.
4. Select the 4-6 questions with the highest real-world relevance to this specific service.

Use the recommended topics below as a fallback only — when research returns fewer than four strong questions, fill remaining slots from this list.

### FAQ Rules

- Write questions the way real customers ask them.
- Keep answers to 2-3 sentences.
- Avoid repeating the body content word for word.
- Answer extra buyer questions that were not fully covered earlier.
- Do not invent pricing, warranty terms, review counts, or response times.
- Cost questions must always be answered as process — explain how the reader gets a confirmed price, what influences the scope, and what to expect from the quoting process. Never use dollar figures or ranges in FAQ answers unless the client has confirmed fixed pricing in writing.

### Recommended FAQ Topics (Fallback)

Use these when research does not produce enough strong questions for the specific service.

- How long the service usually takes
- Whether the service causes disruption
- Whether repair or replacement is more suitable
- How the quoting process works and what influences the final cost
- Whether certification or warranty applies
- Whether the business services nearby areas
- What the customer should prepare before the visit

The quoting process topic should be added as a tie-breaker if research does not already surface a cost or process question that covers the same ground.

---

## Internal Links Section

Add an internal link table at the foot of every deliverable.

| Anchor Text | Suggested Target URL | Placement Context |
|---|---|---|
|  |  |  |

Use related services, parent service categories, nearby location pages, and supporting educational pages.

Do not force links into the copy where they interrupt the flow.

---

## Proofreading Notes

Add a Proofreading Note only when needed.

Use it for:

- Review widget placeholder required
- Gallery placeholder requires client images
- Service claim needs client confirmation
- Equipment, method, or certification not confirmed
- Same-day or emergency claim not confirmed
- Warranty language needs review
- Pricing language needs approval

Example:

**Proofreading Note**

- Review widget placeholder included. Developer or client to add live review feed before publishing.
- Thermal imaging claim removed because it was not confirmed in the client KB.

---

## Service Page Quality Audit

Run before delivery.

### Structure

- [ ] Reader state identified
- [ ] Section order matches the reader state
- [ ] Capability appears early enough
- [ ] Self-identification is placed where it makes sense
- [ ] Trust section uses scannable benefits where appropriate
- [ ] Why Choose bullets are short, scannable, and not mini paragraphs
- [ ] Proof module is included or omission is justified
- [ ] Visual module is conditional and relevant
- [ ] Decision support replaces generic pricing or objections where suitable
- [ ] Process section appears only where it helps

### Writing

- [ ] Opening is reader-first
- [ ] Opening creates confidence before introducing technical risk
- [ ] Opening contains no more than one technical or compliance detail
- [ ] First sentence is not technical unless the audience requires it
- [ ] Every main section has earned detail
- [ ] No generic trust claims
- [ ] No overused opening phrases
- [ ] No repeated sentence patterns
- [ ] Strong closing line before each CTA
- [ ] FAQs add value instead of repeating the page

### SEO And AIO

- [ ] Primary keyword in meta title, meta description, H1, opening, and at least one natural H2
- [ ] Location appears in H1, opening, metadata, and other natural places
- [ ] Headings are not overloaded with service and location repetition
- [ ] FAQ heading includes the service topic
- [ ] Paragraphs are self-contained
- [ ] Verified factual claims are present
- [ ] Internal links are included
- [ ] Page can support LocalBusiness, Service, Review, and FAQ schema where assets exist

### Conversion

- [ ] The reader can quickly tell the business handles the work
- [ ] The reader can see why the business is credible
- [ ] Proof appears before the reader is asked to make a final decision
- [ ] CTAs are clear but not excessive
- [ ] CTA mix includes a form/enquiry option where the service is not urgent
- [ ] Pricing or objection content only appears where useful
- [ ] Page feels like a helpful sales page, not a technical article
- [ ] No dollar figures or ranges appear unless client has confirmed fixed pricing
