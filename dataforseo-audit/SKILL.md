---
name: dataforseo_audit
description: Run a prospect-facing SEO audit on any website using the Tradie Web Guys DataForSEO account. Pulls on-page technical issues, keyword rankings, backlink profile and competitor comparison, then produces a punchy markdown report aimed at trade-business owners with the Impact Roadmap session as the call to action. Trigger on phrases like "audit this site", "run an SEO audit on X", "DataForSEO audit", "prospect audit", "what's wrong with this website's SEO", "compare us to competitor Y", or whenever a domain is dropped into chat with the intent of producing a sales/prospect deliverable.
---

# DataForSEO Audit — Tradie Web Guys

Run an SEO audit on a trade business website using the TWG DataForSEO account. The deliverable is a **markdown report** aimed at a **prospect** — usually a trade-business owner approached by TWG, or someone considering an Impact Roadmap session. The tone matches Matt Jones's voice: plain English, specific numbers, no jargon, no fluff, the data does the heavy lifting.

The audit exists for one reason: give the prospect undeniable evidence that there are gaps in their digital presence costing them booked jobs, and make the **Impact Roadmap session** the obvious next step.

## When to use this skill

Trigger whenever the user asks for any of:
- "Audit [domain]" / "run an SEO audit on [domain]"
- "What's wrong with this website's SEO?"
- "Compare [site A] to [site B]" (competitor audit)
- "Pull rankings / backlinks / on-page for [domain]"
- "Build a prospect audit for [domain]"

Default behaviour when a domain is dropped in chat with sales/prospect framing: run the full audit (all pillars) and produce the markdown report.

## Audit pillars

Every audit covers four pillars. If a pillar's data is unavailable (API timeout, no data returned, subscription not active), note it in the report and continue — don't block the whole audit.

1. **On-page technical** — broken links, missing meta data, duplicate content, speed, schema, crawl issues
2. **Keyword rankings (SERP)** — what they rank for, top opportunities, who's beating them
3. **Backlink profile** — referring domains, anchor profile, toxic/lost link signals
4. **Competitor comparison** — head-to-head against 2–3 competitors (user-supplied or inferred from same locality/trade)

After the four pillars, add a **Recommendations** section that ranks the top 3–5 fixes by impact and ties them to an Impact Roadmap session.

## DataForSEO — authentication and API access

### How we connect

All DataForSEO calls go through our **Pipedream proxy** integration. See `skills/integrations/dataforseo/SKILL.md` for the full function reference.

**Do NOT use direct HTTP Basic auth or `.env` files.** Always use the `pd_dataforseo_*` SDK functions.

### Endpoints mapped to SDK functions

**On-page (technical audit)**
- `pd_dataforseo_create_onpage_task` — kick off a crawl. Args: `target`, `maxCrawlPages=100`, `enableJavascript=True`, `loadResources=True`. This is a draft-required function (needs user approval).
- `pd_dataforseo_proxy_get(url=f"https://api.dataforseo.com/v3/on_page/summary/{id}")` — poll until `crawl_progress == "finished"`. Response is wrapped: parse `json.loads(resp["content"])` → access `data["body"]["tasks"][0]["result"][0]`.
- `pd_dataforseo_proxy_post` for `/v3/on_page/pages` — requires `text_body=json.dumps([{"id": task_id, "limit": 100}])` and `headers={"Content-Type": "application/json"}`. This is also a draft-required call. The crawl summary's `page_metrics.checks` dict already contains aggregate issue counts — often sufficient without pulling individual pages.

**Proxy response format:** All `proxy_get`/`proxy_post` calls return `{"response_role": ..., "content": "<json string>"}`. The content JSON has structure `{"status_code": 200, "body": {<actual DataForSEO response>}, ...}`. Always access `data["body"]["tasks"][0]["result"]`.

**SERP / keyword rankings**
- `pd_dataforseo_get_domain_keywords` — keywords a domain ranks for organically. Use `target`, `locationCode=2036` (Australia), `languageCode="en"`, `limit=100`.
- `pd_dataforseo_get_domain_rank_overview` — domain authority, position distribution, ETV.
- `pd_dataforseo_get_google_organic_results` — spot-check a specific keyword's SERP to show who's outranking them.

**Backlinks** (active as of June 2026)
- `pd_dataforseo_proxy_post` to `/v3/backlinks/summary/live` — total backlinks, referring domains, domain rank.
- `pd_dataforseo_proxy_post` to `/v3/backlinks/referring_domains/live` — top linking domains.

**Competitor comparison**
- `pd_dataforseo_get_competitor_domains` — find competing domains by keyword overlap. Use `target`, `locationCode=2036`, `languageCode="en"`, `limit=5`.
- Run `pd_dataforseo_get_domain_rank_overview` and `pd_dataforseo_get_domain_keywords` for each competitor to populate the comparison table.
- `pd_dataforseo_get_bulk_traffic_analytics` — bulk organic traffic estimates for multiple domains at once.

### Cost discipline

DataForSEO is paid per call. For a prospect audit:
- Use **`live` endpoints** wherever available (no polling, faster, cheaper).
- Cap on-page crawls at **100 pages** unless the user explicitly asks for more.
- Cap ranked keywords at **100 rows** for the prospect report (only show top 10–20 in the deliverable).
- Don't run competitor on-page crawls — only their SERP and domain metrics. Saves money.

## Inputs

- **Domain** (required) — the website URL to audit.
- **Target country/location** (inferred) — defaults to Australia for `.com.au`, New Zealand for `.co.nz`. Otherwise ask.
- **Competitors** (optional) — user-supplied or auto-discovered from DataForSEO. If the client named specific competitors during onboarding (e.g. via VideoAsk), those MUST be included even if they don't rank as top SEO competitors. Verify transcribed business names before using — AI transcription often mangles names.

Missing-input handling: if the domain is not provided, ask. If the location cannot be inferred from the TLD, ask. Do not guess.

## Guardrails

- Output is a branded PDF draft for Matt to review and personalise (fill in Impact Roadmap spot count) before sending to the prospect. This skill does not send the audit to anyone.
- Always crawl the site's sitemap before running DataForSEO analysis. Do not claim a site has "no landing pages" based on keyword data alone — the pages may exist but rank poorly.
- For existing clients (not cold prospects), describe the current state accurately — what's already built, what's working, what needs enrichment. Do not frame it as "build from scratch" when pages already exist.
- Schema findings must be specific and evidence-based — show the exact JSON-LD blocks found, not just "wrong schema."
- Never fabricate traffic numbers, revenue projections, or ranking data. Use ranges or "this would close roughly X of the gap" language.
- Cap on-page crawls at 100 pages unless explicitly asked for more (cost discipline).
- Do not include the $550 Impact Roadmap price in the audit document — pricing belongs on the booking page.
- Keep internal integration details (API keys, endpoints, credentials) out of the deliverable.
- **Classify every finding by evidence level and impact** before it reaches the report. Read `skills/seo_knowledge_base/references/evidence-impact-framework.md`. DataForSEO's own severity scores are L5 evidence — reclassify them. Never present an L3/L4/L5 recommendation as a Google requirement. Order "What we'd fix first" by impact, not by what the tool flagged loudest.
- **Drop Informational + L5 findings from the prospect report.** Padding an audit with cosmetic issues buries the findings that matter.

## Process

0. **Read the SEO knowledge base** — `skills/seo_knowledge_base/references/evidence-impact-framework.md` and `references/seo-rules-reference.md`. These govern which findings are real, how they're ranked, and what language is allowed. Do not skip this — the rules change (FAQ schema, word count minimums, freshness) and stale claims damage credibility with prospects who check.
1. **Confirm inputs** — domain, target country/location (default: Australia), and competitors (default: ask DataForSEO for top 3 organic competitors). If the user didn't specify a location and the domain is `.com.au`, default to Australia. If `.co.nz`, default to New Zealand. Otherwise ask.
2. **Run the pillar calls in parallel where possible.** The on-page crawl is the long pole — kick it off first so it can finish while the other pillars run.
3. **Pull the data into structured variables** — counts, top issues, top rankings, top backlinks, competitor comparison rows.
4. **Translate the data into the prospect-facing report** using the template below. Stick to Matt's voice: short sentences, specific numbers, no jargon, no fluff.
5. **Save the report** as a `.md` file named `seo-audit-{domain}-{YYYY-MM-DD}.md` in `/work/temp/`.
6. **Upload the report to Slack** using `coworker_upload_to_slack` and share it. Give a 2–3 sentence summary in the chat message: headline finding, biggest opportunity, and the file. Do not dump the full report into chat.

## Report template

Use this structure verbatim. Fill in the bracketed placeholders. If a section has no data, write "Data not available — flagging this as a gap in itself: the fact we can't pull this signals the site isn't being measured."

```markdown
# SEO Audit — {Domain}

**Prepared by:** Tradie Web Guys
**Date:** {YYYY-MM-DD}
**Domain audited:** {domain}
**Location:** {country/region}

---

## The short version

{2–3 sentences. What's the headline finding? What's the single biggest opportunity or biggest hole? Plain English, no list — this is the bit they read first.}

---

## 1. On-page technical health

Crawled {N} pages. Here's what's broken or missing.

| Issue | Count | What it means |
|---|---|---|
| Broken internal links | {N} | Pages on the site pointing to dead URLs. Bad for users, bad for Google. |
| Pages missing title tags | {N} | Google has nothing to show in search results. |
| Pages missing meta descriptions | {N} | The site is leaving the click-through copy up to Google. |
| Duplicate titles | {N} | Multiple pages competing for the same search result. |
| Slow pages (>3s load) | {N} | Mobile users bounce before the page loads. |
| Pages with schema errors | {N} | Missing or broken structured data — limits rich results in Google. |
| Redirect chains | {N} | Multi-step redirects waste crawl budget and slow the site down. |

{1–2 paragraphs of plain-English commentary. What does this picture say about the site? Is this a "quick fix" site or a "rebuild" site?}

---

## 2. Where you rank (and where you don't)

The site currently ranks for **{N} keywords** in Google {country}. Here are the top ones that actually drive traffic.

| Keyword | Position | Monthly searches | Notes |
|---|---|---|---|
| {keyword 1} | {pos} | {volume} | {short note — e.g. "Brand term — should be #1"} |
| {keyword 2} | {pos} | {volume} | {note} |
| ... | | | |

**Money keywords where you're missing:**

{Pick 3–5 keywords from the data where the site ranks position 11–30, or doesn't appear at all, but the search volume and intent suggest it should. For each: keyword, current position (or "not ranking"), monthly searches, and one line on why it matters.}

{1–2 paragraphs of commentary. Are they ranking for "near me" / suburb terms? Brand vs non-brand split? Are they getting traffic from the right keywords or just brand searches?}

---

## 3. Backlink profile

| Metric | Value | What it tells us |
|---|---|---|
| Referring domains | {N} | Number of unique websites linking to the site. |
| Total backlinks | {N} | Total individual links. |
| Domain rank | {N}/1000 | DataForSEO's authority score. |
| Broken backlinks | {N} | Links pointing to dead pages — wasted authority. |
| Dofollow / nofollow split | {%} / {%} | Higher dofollow % means more SEO value flowing in. |

**Top 5 referring domains:**
1. {domain 1} — {rank}
2. {domain 2} — {rank}
3. ...

{1–2 paragraphs. Is the link profile thin, healthy, or spammy? Are they earning links from local press, industry bodies, suppliers — or is it mostly directories?}

---

## 4. Competitor comparison

Compared against {competitor 1}, {competitor 2}, {competitor 3}.

| Metric | You | {comp 1} | {comp 2} | {comp 3} |
|---|---|---|---|---|
| Keywords ranking | {N} | {N} | {N} | {N} |
| Top 10 rankings | {N} | {N} | {N} | {N} |
| Referring domains | {N} | {N} | {N} | {N} |
| Domain rank | {N} | {N} | {N} | {N} |
| Estimated organic traffic / mo | {N} | {N} | {N} | {N} |

{2–3 sentence commentary. Where's the gap biggest? Who's eating the lunch and why?}

---

## 5. What we'd fix first

Based on this audit, here are the top {3–5} priorities, in order of impact.

1. **{Priority 1 — punchy title}**
   {1–2 sentences. What's the issue, what's the fix, and what's the expected impact in plain terms — "this would put roughly X pages back in play" / "this would close the gap with {competitor} on Y keywords".}

2. **{Priority 2}**
   {Same format.}

3. **{Priority 3}**
   {Same format.}

{Optional 4 and 5.}

---

## Where to from here

This audit shows you what's broken and what's costing you booked jobs. The Impact Roadmap session is where we sit down with you for 90 minutes, walk through this in plain English, and build a documented 6–12 month plan to fix it — whether you end up working with us or not.

It's a paid working session — not a sales call, not a discovery call. You leave with the strategy in writing.

Book your Impact Roadmap session here: https://go.tradiewebguys.com.au/book

[X of 8 spots left this month]

— Matt Jones, Tradie Web Guys
```

## Voice rules

Follow the TWG Brand Guide tone (see Brand Guide Integration section above). In summary:

- Direct, not fluffy. The numbers do the work.
- Specific over general — name the keywords, name the competitors, give the counts.
- Australian phrasing where it fits. "GBP" for Google Business Profile. "Bonnet" not "hood".
- No marketing words: synergy, leverage, supercharge, unlock, game-changer, transformative, omnichannel.
- No emojis, no exclamation marks, no ALL CAPS in body copy.
- Short sentences. Short paragraphs.
- Confident, not braggy. "This is the kind of gap we close in the first 90 days" — not "We are the leading SEO experts."
- Don't tell the reader how they feel. Show them the data.
- Use brand language: "predictable lead flow", "makes the phone ring", "booked work", "digital systems", "step off the tools".
- Frame findings structurally — talk about systems, architecture, foundations — not quick fixes or hacks.

## The Impact Roadmap CTA — non-negotiable

Every audit ends with the Impact Roadmap CTA paragraph + the `[X of 8 spots left this month]` capacity line + `Matt Jones, Tradie Web Guys` sign-off. The booking link is always `https://go.tradiewebguys.com.au/book`.

**Do NOT mention the $550 price in the audit document.** Pricing belongs on the booking page. Reference it as a "paid working session" only.

Acceptable phrasing variants for the capacity line (default to the first):
- `[X of 8 spots left this month]`
- `[X out of 8 Impact Roadmap spots left this month]`
- `[X spots left for this month's Impact Roadmaps]`

Leave the `X` as a literal placeholder — Matt fills it in before the audit is sent.

## Brand Guide Integration

All audits must follow the Tradie Web Guys brand guide. This applies to both the written voice and the visual presentation.

### Visual Identity (PDF output)

Audits are delivered as **branded A4 PDF reports**, not raw markdown. Use WeasyPrint to render HTML → PDF with the following brand tokens:

| Element | Value |
|---|---|
| Primary Green | `#1F9C51` — buttons, highlights, accent bars |
| Navy Charcoal | `#1A1F2E` — dark backgrounds, primary text, cover page |
| Warm Cream | `#F5F4F2` — stat card backgrounds, light fills |
| Lime Accent | `#8DC63F` — logo block, secondary highlights, section eyebrows on dark bg |
| Heading font | `Outfit` — weights 800–900 for headings, 700 for subheadings |
| Body font | `Inter` — weights 400 (regular) and 600 (semibold) |

**PDF structure (7–8 pages):**
1. **Cover** — Navy background, large domain name in Outfit 900, "SEO SITE AUDIT" eyebrow in lime, TWG brand name bottom-left, tagline bottom-right. Decorative green arc in top-right.
2. **SEO Snapshot** — Stat cards (keywords, page-1 rankings, ETV, traffic value), ranking distribution bar, bottom-line callout, new/lost keyword trend.
3. **Keywords That Are Working** — Table of strong rankings (top 10, vol ≥ 50), "What's Working" callout highlighting specific wins.
4. **Untapped Opportunities** — Page-two keywords ready to move, missing high-intent keywords with priority badges.
5. **Technical Health** — On-page score bar, infrastructure table, pass/fail checklist, stat cards for key metrics.
6. **Issues to Fix** — Severity-tagged issue table (CRITICAL/WARNING badges), Priority Actions callout.
7. **Competitive Landscape** — Local SERP presence table, competitor advantage breakdown.
8. **What We'd Fix First** — Navy background, phased roadmap (Month 1–2, 2–3, 3–6, 6+), Impact Roadmap CTA in lime green.

Import Google Fonts for Outfit and Inter via `@import url()`. Load with WeasyPrint's `url_fetcher` wrapper (see `skills/pdf_creation/SKILL.md`).

### Voice & Tone (brand guide rules)

Follow these tone pillars from the brand guide:
- **Direct** — no fluff, no jargon. Numbers do the work. Short sentences.
- **Structural** — focus on the underlying architecture of their digital presence.
- **Guiding** — tell them what they need, don't ask what they want.
- **Earned Authority** — speak from lived experience, not theoretical knowledge.

**Don't say → Say:**
- "Synergistic omnichannel lead generation" → "A system that makes the phone ring"
- "We'll get you more clicks" → "We build predictable lead flow"
- "Contact us today for a free consultation" → "Book an Impact Roadmap session. We'll map your gaps and build a 12-month plan to fix them."

**Contrarian positions to weave in where natural:**
- "Marketing won't fix a broken business." — if the site has foundational issues, say so directly.
- "We don't do free proposals." — the Impact Roadmap is a paid working session, not a sales call.

### Photography guidelines (if images used)

No staged stock photos. Authentic, natural light, real work environments. This usually won't apply to SEO audits but note it for any future visual additions.

## Output

Save the PDF to `/work/temp/` as:

```
{Business_Name}_SEO_Audit_{MonthYear}.pdf
```

e.g. `Malvern_Physio_SEO_Audit_May2026.pdf`

Upload to Slack via `coworker_upload_to_slack` and share it. In the chat reply, give a 2–3 sentence summary: the headline finding, the biggest opportunity, and the file. Do not dump the full report into chat — it lives in the file.

## When data is missing or partial

Note it as a finding in the report — missing data is itself a signal. The bias is: **ship the draft, let Matt edit.** Don't ask clarifying questions if the domain and country are clear.

## DataForSEO API notes

- `pd_dataforseo_get_domain_keywords` uses `targetType="site"` (not `"domain"`)
- Backlinks API is active — use `pd_dataforseo_proxy_post` to `/v3/backlinks/summary/live` and `/v3/backlinks/referring_domains/live`
- WordPress sitemaps: try `/sitemap_index.xml` first (Rank Math uses this), then fall back to `/sitemap.xml`

## Anti-patterns — never do these

- Don't recommend "boost your social media engagement" or anything that isn't SEO/site-related. This audit is scoped.
- Don't promise specific traffic / revenue numbers. Use ranges or "this would close roughly X of the gap" language.
- Don't bury the lead. The "short version" section is where the biggest finding goes — not section 5.
- Don't pad the report with definitions of what SEO is, what Google is, etc. The reader runs a business; they know.
- Don't include screenshots or charts in the markdown — text + tables only.
- Don't sign off as "The Tradie Web Guys Team" or "Tradie Web Guys Marketing" — sign as `Matt Jones, Tradie Web Guys`.
- Don't include the raw DataForSEO JSON in the report. Strip it down to the metrics the prospect cares about.
- Don't leak credentials or API details. Internal integration details stay internal.
- **Don't recommend FAQ schema as a priority task.** As of May 2026, Google no longer displays FAQ rich results for ordinary local businesses. Visible FAQ content on pages is still valuable, but FAQPage schema markup itself is optional/low-priority. Don't present it as a meaningful visibility feature.
- **Don't flag cosmetic formatting issues** (e.g. lowercase H1 tags) as audit findings. These are not SEO issues and create busywork tasks with no value.
- **Don't list lead aggregators or industry platforms as competitors.** DataForSEO "competitor overlap" measures keyword overlap, not business competition. Platforms like SolarQuotes, SolarChoice, HiPages, ServiceSeeking, Oneflare etc. are marketplaces/aggregators — not competitors. Always verify and filter. Ask the client or check onboarding data for actual named competitors first.
- **Don't claim structured data is required for AI search.** Google has stated structured data is not required for AI Overviews or AI Mode. Existing SEO fundamentals apply. Don't recommend schema specifically for AI visibility.

## Related skills

- `skills/integrations/dataforseo/SKILL.md` — API functions, available modules, cost notes
- `email-creator` — for turning a finding from the audit into a promotional email
- `linkedin-post` — for turning a finding into a LinkedIn post

## Known limitations

- On-page crawls require draft approval (write operation).
- Location defaults: `.com.au` → Australia (2036), `.co.nz` → New Zealand (2554). Otherwise ask.
- `domain_rank_overview` returns N/A for paid metrics on smaller AU domains.
