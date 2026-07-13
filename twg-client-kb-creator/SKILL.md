---
name: twg-client-kb-creator
description: Create a structured Client Knowledge Base (CLIENT-KB.md) for TWG clients from onboarding forms and approved materials. Triggers on "create a client KB", "build the KB for [client]", "knowledge base for [shortcode]".
---

## Purpose
Create a structured CLIENT-KB.md from raw onboarding data, discovery notes, website copy, ads notes, SEO notes, or any other approved client material. Used across all service lines — website copywriting, Google Ads, SEO, social media, blogs, landing pages, emails, and ads.

## Workflow

1. **Gather source material** — Download the onboarding form from Google Drive (usually in the client's Admin folder). Check for any other approved materials (discovery notes, existing website, ads notes, SEO notes).

2. **Extract and synthesise** — Don't just copy the form. Synthesise the information into useful copywriting reference. Use Australian English unless the client operates in another country.

3. **Build the KB** using the 8-section structure in `references/kb_template.md`.

4. **Create Google Doc** named `{SHORTCODE} - CLIENT-KB.md` and place it in the client's Admin folder (`{SHORTCODE} - Admin/`) in Google Drive.

5. **Ask for missing info** — After completion, list the task requester in Slack and ask about any missing information that would improve future AI copywriting. Common questions:
   - Are you licensed and insured?
   - Do you offer emergency service?
   - What areas do you prioritise?
   - What warranties do you offer?
   - What brands do you use?
   - What makes your business different?
   - Do you prefer a formal or conversational tone?
   - Are there any claims we should avoid?
   - What are your preferred CTAs?

## Inputs

- **Client name or shortcode** (required) — the TWG client code (e.g. ARP, ZAP). If not provided, ask.
- **Onboarding form / source material** (required) — Google Drive link or uploaded document. If not provided, ask.
- **Google Drive folder** (required) — the client's Admin folder for delivery. If not provided, search for `{SHORTCODE} - Admin/` in Drive.

Missing-input handling: if the client name or onboarding material is not provided, pause and ask. Do not guess or fabricate client details.

## Guardrails

- Output is a draft Google Doc for the project manager to review. Do not use the KB to write client copy until it has been reviewed.
- Use "Not provided" where information is missing — never invent facts about the client's business.
- Separate confirmed facts from assumptions/inferences. Label inferred items as "Likely customer need" rather than confirmed fact.
- Do not over-write or fill gaps with made-up information.
- Keep client-specific data (pricing, internal strategy) inside the KB only — not in anything that could be shared externally.
- Default voice: clear, practical, conversational Australian English.
- See `references/kb_template.md` for the full section structure.
