---
name: seo-strategy
description: "Create and maintain SEO strategy docs for TWG clients. First strategy during onboarding, quarterly reviews at block boundaries. PM-triggered, produces ClickUp doc drafts for approval. Use when someone says \"create the SEO strategy for [client]\", \"run the quarterly review for [client]\", \"build the strategy doc\", \"next block for [client]\", or \"quarterly SEO review\". Output is a draft for the PM to review before publishing."
---

# SEO Strategy

Create and maintain SEO strategy documents in each client's ClickUp Project Hub. The strategy doc is the plan that drives 3-month content blocks — what to write, in what order, for which keywords and locations.

## Two Jobs

**First strategy (onboarding):** Build the strategy doc from scratch after all prerequisites are met. Runs a fresh DataForSEO audit (not the prospect audit), populates all 7 sections, creates STATE.md.

**Quarterly review:** At the end of each 3-month block, read the last 3 monthly reports + STATE.md, run a fresh audit, draft the next block's content plan, and update roadmap/focus. Each block creates a new ClickUp page — previous blocks stay as read-only history.

## Triggers

| Job | Command | When |
|---|---|---|
| First strategy | `@Viktor create the SEO strategy for [SHORTCODE]` | After keyword research completes — PM triggers manually |
| Quarterly review | `@Viktor run the quarterly review for [SHORTCODE]` | Monthly report cron flags final month of block — PM triggers when ready |

## Service Confirmation (pre-strategy)

After the KB is created, Viktor automatically creates a **"Confirm Services & Locations"** ClickUp task with:
- **Services** — straight extraction from the questionnaire, listed as-is (no AI elaboration)
- **Locations** — two-tier: client-stated regions + proposed suburb expansion ranked by search demand from DataForSEO

The PM confirms, edits, or trims. On completion, a ClickUp automation notifies Viktor to update the KB. See `references/service-confirmation-workflow.md` for the full process including suburb expansion logic.

## Prerequisites (first strategy)

All 4 must exist before proceeding. If any are missing, tell the PM what's not ready.

1. **Client KB** — `skills/clients/{shortcode}/SKILL.md` with confirmed services, locations, competitors, brand voice
2. **Services/locations confirmed** — "Confirm Services & Locations" ClickUp task completed
3. **Content register** — Google Sheet with crawled site pages
4. **Keyword research sheet** — Google Sheet with per-page keyword assignments

The prospect-facing DataForSEO audit is NOT a prerequisite — the strategy skill runs its own fresh audit aligned to the client's confirmed services.

## Flow

Read `references/first-strategy-flow.md` for the full onboarding flow and `references/quarterly-review-flow.md` for the quarterly review flow.

**High-level onboarding flow:**
1. Validate all 4 prerequisites
2. Run fresh DataForSEO audit — pre-access, DataForSEO only (on-page + SERP + backlinks + competitors from KB). GSC/GA/GBP not available yet at this point in onboarding.
3. Pull AIO/LLM visibility data from DataForSEO SERP features
4. Read keyword research sheet, content register, client KB
5. **Score existing content quality** — every page scored on two axes (content quality 0–16, SEO performance 0–6) → Keep/Monitor/Rewrite/Replace verdict. See `references/content-quality-evaluation.md`
6. **Run content gap analysis** — cross-reference content register + keyword sheet + services × locations matrix + competitor keywords → prioritized gap list. See `references/content-gap-analysis.md`
7. Populate strategy doc template (all 7 sections) — see `references/strategy-doc-template.md`
8. Apply content planning methodology to gap list → Section 4 content plan. See `references/content-planning-methodology.md`
9. Create strategy page in client's ClickUp Project Hub as draft
10. Post to Slack for PM review
11. On approval: publish, create STATE.md, update roadmap/focus, trigger content scheduler

## STATE.md

Rolling working memory at `skills/clients/{shortcode}/seo/STATE.md`. Updated monthly by the reporting cron, read by the strategy skill at quarterly review. Links to all artifacts — no data duplication. See `references/state-md-template.md` for format.

## Roadmap & Current Focus Updates

**Conditional — only at block boundaries:**
- New engagement starts → roadmap entry + current focus update
- Block completes + new block approved → roadmap entry + current focus update
- Major strategic shift mid-block → roadmap entry

Between blocks, the Fathom meeting processor handles roadmap/focus updates from client meetings. The strategy skill does NOT touch roadmap/focus for mid-block edits.

Uses `clickup-roadmap-focus` skill with a specific payload — milestone text, focus priorities, KPI updates.

## Integrations

| Tool | What for | Used in |
|---|---|---|
| DataForSEO | Fresh audit, keyword rankings, backlinks, AIO/LLM visibility, SERP features | Both jobs |
| Google Search Console | Organic clicks, impressions, CTR, position by query/page | Quarterly review only (not available at onboarding — access set up after strategy doc) |
| Google Analytics 4 | Sessions by channel, landing pages, conversion events | Quarterly review only |
| Google Business Profile | Calls, clicks, directions, reviews, posts | Quarterly review only |
| ClickUp | Strategy doc, roadmap/focus, task creation | Both jobs |
| Google Sheets | Keyword research, content register (read-only) | Both jobs |

## Guardrails

- **Draft + human review.** Strategy doc is always a ClickUp draft. PM approves before publishing.
- **Fresh audit, not prospect audit.** The sales audit may not match the client's confirmed services. Always run a new one.
- **Don't fabricate metrics.** If data is unavailable, say so.
- **Section 6 technical priorities are ordered by impact, with evidence levels.** Read `skills/seo_knowledge_base/references/evidence-impact-framework.md`. Never rank a finding high because DataForSEO flagged it high.
- **Content planning methodology governs Section 4.** Follow velocity (2/week), ramp periods, foundation gate, and new-vs-rewrite rules exactly.
- **Block goals ≠ vision restated.** Section 7 targets specific movements this block creates, not smaller versions of Section 1.
- **Competitors from KB only.** Section 5 uses named competitors from the client KB, not DataForSEO overlap lists (which surface aggregators, not competitors).

## Reference Files

| File | Purpose |
|---|---|
| `references/first-strategy-flow.md` | Step-by-step onboarding flow with data sources and outputs |
| `references/quarterly-review-flow.md` | Step-by-step quarterly review flow |
| `references/state-md-template.md` | STATE.md format and update rules |
| `references/content-planning-methodology.md` | Amanda's content methodology — velocity, ramp, sequencing, new vs rewrite |
| `references/strategy-doc-template.md` | The 7-section strategy doc template (also lives in ClickUp template hub) |
| `references/strategy-doc-template-original.md` | Amanda's original template before Section 3 keyword-duplication adjustment |
| `skills/seo_knowledge_base/` | Evidence hierarchy, impact framework, and the audited SEO rule set — read before writing Section 6 or scoring content |
| `references/content-quality-evaluation.md` | Two-axis scoring of existing pages (content quality × SEO performance) → Keep/Monitor/Rewrite/Replace verdicts |
| `references/content-gap-analysis.md` | Four-type gap analysis methodology (matrix, quality, competitor, intent) with prioritization scoring |
| `references/service-confirmation-workflow.md` | Service extraction + suburb expansion workflow with DataForSEO, ClickUp task format, PM confirmation loop |
