# Contact Page — Structure & Rules

Read the parent `SKILL.md` and the client's `client-kb.md` first. This file covers what is unique to the Contact page.

---

## Rules

- **Max 300 words** of body copy (excluding the contact details table itself).
- Short CTA paragraph at the top — pull wording from `client-kb.md`.
- All details must be pulled from `client-kb.md` — do not assume or infer contact details.

## Required Elements

- Business name
- Phone number
- Email address
- Service area
- ABN
- All licence numbers (see Licences below)
- Operating hours
- Google Maps embed placeholder
- Web enquiry form placeholder
- Primary CTA button

## Licences

Always display all client licences on the Contact page.

- Format: `[Licence Type] LIC: [Number]` — e.g. `Plumbing LIC: 123456`
- Pull all licence types and numbers from `client-kb.md`
- If any licence number is missing from `client-kb.md`, flag it as outstanding before writing — do not proceed with a placeholder

## NAP Consistency

All NAP details (Name, Address, Phone) must be identical to every other page on the site. Any drift breaks the LocalBusiness schema. Cross-check against `client-kb.md` before finalising.

## Developer Notes Block

Include a Developer Notes block at the foot of the deliverable covering:

- Schema type (LocalBusiness, plus any trade-specific type — Plumber, Electrician, RoofingContractor, etc.)
- Business hours in schema-compatible format
- Geo coordinates if known (pull from `client-kb.md`)
- Form routing email
- Click-to-call setup on phone number
- Callback CTA preference (omit if `client-kb.md` says no callback CTA)
- Any other implementation details relevant to the developer
