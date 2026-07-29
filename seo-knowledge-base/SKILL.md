---
name: seo_knowledge_base
description: TWG's SEO ground truth — the evidence hierarchy, impact framework, and the audited list of which SEO rules are Google-documented vs convention vs outdated. Read before making or ranking any SEO recommendation in an audit, report, strategy doc, or content brief.
---

# SEO Knowledge Base

This is a **reference skill, not an action skill**. It holds the standards every other TWG SEO skill applies. It contains no client data.

## What's in here

| File | Purpose |
|---|---|
| `references/evidence-impact-framework.md` | The 5-level evidence hierarchy and 5-tier impact framework, plus how to apply and display them |
| `references/seo-rules-reference.md` | Full audited SEO rule set — what's Google-documented, what's convention, what's outdated, and what's genuinely uncertain |

## When to read it

| Situation | Read |
|---|---|
| Producing an SEO audit (prospect or client) | Both files |
| Writing a monthly SEO report | `evidence-impact-framework.md` |
| Building a strategy doc's technical priorities | `evidence-impact-framework.md` |
| Scoring existing content quality | `seo-rules-reference.md` (schema and word count sections) |
| Writing service pages, location pages, or blogs | `seo-rules-reference.md` if an SEO claim is being made in the copy or brief |
| Anyone asks "is X still an SEO best practice?" | `seo-rules-reference.md` section 3 |

## The two rules that matter most

**1. Every recommendation carries an evidence level.** A Level 3, 4, or 5 recommendation is never described as a Google requirement. If evidence is mixed or absent, say so rather than inventing a rule.

**2. Findings are ordered by impact, never by tool severity.** SEO tools (Screaming Frog, DataForSEO, Ahrefs, PageSpeed) score issues on their own scales that don't map to business impact. A tool flagging something "critical" is not evidence it matters. Cross-reference against the impact framework before it reaches a report.

## Consuming skills

These skills read this knowledge base. If the frameworks change here, check them:

- `dataforseo_audit` — prospect-facing audits
- `seo-monthly-report` — client monthly reporting
- `seo-strategy` — strategy docs, technical priorities, content quality evaluation
- `twg_website_copywriting` — service/location/home page copy
- `twg_client_blog_writing` — client blog posts

## Maintenance

Google changes what it supports. Re-verify before presenting anything as fact:

- Schema rich-result eligibility changes regularly (FAQ was cut back in 2023 and again May 2026). Check Google's [supported structured data types](https://developers.google.com/search/docs/appearance/structured-data/search-gallery) before calling any schema a rich-result driver.
- Section 8 of `seo-rules-reference.md` lists the known knowledge gaps and volatile areas.
- When a rule is found to be stale, update `seo-rules-reference.md` and note the date — don't leave the correction only in a Slack thread.
