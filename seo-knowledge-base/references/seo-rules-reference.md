# SEO Knowledge Audit — Viktor

**Prepared for:** Amanda Jones, Customer Success  
**Date:** 2026-07-20  
**Purpose:** Audit of current SEO knowledge, rules, benchmarks, and assumptions before any playbook is created.

---

## 1. SEO Benchmark — Authoritative Sources

### Primary Sources (Level 1 evidence)

These are the sources I treat as definitive when making SEO recommendations. If a primary source contradicts a secondary source, the primary source wins.

| Source | What it covers | How I use it |
|---|---|---|
| [Google Search Central documentation](https://developers.google.com/search/docs) | Crawling, indexing, ranking systems, structured data, site-specific guidelines | Definitive reference for what Google requires, recommends, or explicitly does not require |
| [Google Search Essentials](https://developers.google.com/search/docs/essentials) (formerly Webmaster Guidelines) | Technical requirements, spam policies, key best practices | Baseline compliance — any recommendation must not contradict these |
| [Google Structured Data documentation](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) | Schema markup types, required/recommended properties, eligibility for rich results | Source of truth for which schema types produce rich results and what properties are required vs optional |
| [Google Search Status Dashboard](https://status.search.google.com/products/rGHU1u7kqx6rbpV0kaw0sEofWJkE/history) | Confirmed algorithm updates, ranking system changes | Verification of whether a specific update actually occurred and what it targeted |
| [Schema.org specifications](https://schema.org) | Vocabulary definitions for structured data | Reference for valid properties and types — but Google's documentation takes precedence for search-feature eligibility |
| [Bing Webmaster documentation](https://www.bing.com/webmasters/help) | Bing-specific crawling, indexing, and ranking guidance | Secondary reference — used when the recommendation applies beyond Google (e.g. IndexNow, meta tags that Bing reads differently) |
| [Google Search Central Blog](https://developers.google.com/search/blog) | Official announcements, feature launches, deprecations | Primary for recent changes — e.g. the FAQ rich result eligibility change, helpful content system updates |
| [Google's SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide) | Foundational SEO practices as documented by Google | Useful for confirming what Google explicitly recommends vs what the industry assumes |

### Secondary Sources (Level 2 evidence)

These are recognised research platforms and industry resources. I use them for data, testing results, and implementation guidance — but never as a substitute for a primary source on what Google requires.

| Source | What it covers | How I use it |
|---|---|---|
| Ahrefs blog and studies | Backlink research, keyword data, ranking factor correlation studies | Data and methodology — not treated as Google-confirmed requirements |
| SEMrush studies and sensor data | Ranking volatility, SERP feature tracking, competitive analysis | Trend identification and benchmarking — same caveat as Ahrefs |
| Moz research and Whiteboard Friday archives | Domain authority concepts, local SEO research, algorithm analysis | Useful for local SEO methodology — but "Domain Authority" is a Moz metric, not a Google ranking factor |
| Search Engine Journal, Search Engine Land | Industry news, practitioner guides, Google spokesperson quotes | Good for staying current — but quotes from Google employees on X/Twitter or at conferences are not official documentation unless corroborated by Search Central |
| Screaming Frog documentation | Crawl analysis methodology, technical audit procedures | Implementation reference for technical audits |
| Web.dev / PageSpeed Insights documentation | Core Web Vitals thresholds, performance guidance | Google-authored but focused on web performance — CWV thresholds are confirmed ranking signals |
| Chrome UX Report (CrUX) | Real-user performance data | Field data source for CWV assessment |

### Sources NOT Treated as Authoritative (Level 5 or worse)

| Source type | Why it is not authoritative |
|---|---|
| Unverified blog posts and listicles | No evidence base, often recycled from older posts, frequently contain outdated or invented "ranking factors" |
| Old SEO checklists (especially pre-2020) | Many practices have been deprecated, superseded, or never worked as claimed |
| SEO tool warnings without supporting evidence | Tools flag issues based on their own scoring algorithms, not Google's ranking systems. A tool score is not an SEO metric. |
| Forum opinions (Reddit, Quora, BlackHatWorld, WebmasterWorld) | Anecdotal, often contradictory, no quality control |
| Outdated ranking-factor studies | Correlation ≠ causation. Many widely cited studies (e.g. Backlinko's "200 ranking factors") mix confirmed signals with speculation |
| Assumptions carried over from earlier SEO practices (pre-Helpful Content, pre-SpamBrain) | Keyword density targets, exact-match anchor ratios, minimum word counts — these were either never confirmed or have been explicitly walked back |
| Unofficial Google employee statements on social media | John Mueller, Gary Illyes, and Danny Sullivan frequently clarify on X/Twitter, but these are not official documentation. They can inform interpretation but should not be cited as definitive rules. |

### Knowledge Verification Date

My training data has a cutoff, but I have access to live web search and can verify current documentation before making recommendations. For this audit, I have cross-referenced my knowledge against Google Search Central documentation as of July 2026.

**Areas where I can confidently verify current state:**
- Google structured data eligibility (including FAQ schema status changes — confirmed deprecated for non-authoritative sites as of May 2026)
- Core Web Vitals thresholds (LCP, INP, CLS — current thresholds)
- Google's stated position on AI-generated content
- Current algorithm and ranking system documentation
- Schema.org vocabulary and Google's supported types

**Areas requiring live verification before any recommendation:**
- Specific SERP feature availability in Australian market
- Current Google Business Profile feature set and requirements
- Any recommendation about a specific tool's current capabilities
- Competitor landscape data (always pulled live from DataForSEO or similar)

---

## 2. SEO Rules Currently Applied

The following table documents the rules I currently apply during SEO audits. Each rule includes its classification, source, confidence level, likely impact, currency, and exceptions.

**Classification key:**
- **GR** = Confirmed Google Requirement
- **GRec** = Google Recommendation (not required, but advised)
- **IC** = Industry Convention
- **AR** = Accessibility Recommendation
- **CR** = Conversion Recommendation
- **IP** = Internal Preference (TWG-specific)

### Title Tags

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Include the primary keyword in the title tag | GRec | Google SEO Starter Guide | Current (2024 revision) | High | High — title is a confirmed ranking signal | Yes | Brand-only pages where the keyword is the brand name |
| Keep titles under 60 characters (display) | IC | Industry testing (Moz, Ahrefs pixel-width studies) | Ongoing | Medium | Medium — longer titles are truncated in SERPs, not penalised | Yes | Google rewrites titles frequently regardless; the 60-char guideline is about display, not ranking |
| Each page should have a unique title | GRec | Google SEO Starter Guide | Current | High | Medium — duplicate titles cause confusion in SERPs and waste crawl differentiation | Yes | Paginated series may share a base title with page numbers |
| Title should accurately describe the page content | GR | Google Search Essentials | Current | High | High — misleading titles may trigger Google's title rewrite system or be flagged as deceptive | Yes | None |
| Include location modifier for local service pages | IC / IP | Industry convention for local SEO | Ongoing | Medium | Medium — helps geo-intent matching but is not a requirement | Yes | National service pages, pages targeting broad regions where a single suburb doesn't apply |

### Meta Descriptions

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Write a unique meta description for each page | GRec | Google SEO Starter Guide | Current | High | Low for rankings — meta descriptions are NOT a ranking signal. Impact is on click-through rate (search-result appearance). | Yes | Google rewrites meta descriptions ~70% of the time (Ahrefs 2024 study). Still worth writing for the 30% and for social sharing previews. |
| Keep meta descriptions between 150–160 characters | IC | Industry convention based on SERP display testing | Ongoing | Medium | Low — this is a display guideline, not a ranking factor | Yes | Google may show longer snippets (up to ~320 chars on desktop) depending on the query |
| Include primary keyword in meta description | IC | Industry convention | Ongoing | Low | Low — Google bolds matching terms in snippets, which may improve CTR, but meta description keyword content does not affect rankings | Yes | If including the keyword makes the description read unnaturally, skip it |

### H1 Headings

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Each page should have an H1 | GRec / AR | Google SEO Starter Guide, WCAG | Current | High | Medium — the H1 helps Google understand the page's main topic. Accessibility requirement for screen readers. | Yes | Google has confirmed multiple H1s are fine (John Mueller, 2019 and reiterated since). One H1 is convention, not a hard requirement for ranking. |
| Include primary keyword in the H1 | GRec | Google SEO Starter Guide (headings section) | Current | Medium | Medium — heading content is a ranking signal, but not a make-or-break one | Yes | If the keyword doesn't fit naturally, a close variant or semantically equivalent phrasing works |
| H1 should accurately describe the page content | GRec / AR | Google, WCAG 2.1 | Current | High | Medium | Yes | None |

### H2–H6 Structure

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use headings in a logical hierarchy (H1 → H2 → H3, no skipping) | AR / GRec | WCAG 2.1 Level A (1.3.1 Info and Relationships), Google SEO Starter Guide | Current | High | Low for rankings — important for accessibility and content comprehension. Google uses heading structure to understand content organisation. | Yes | Skipping levels (H2 → H4) is an accessibility violation but will not directly harm rankings |
| Include secondary keywords in H2/H3 headings where natural | IC | Industry convention | Ongoing | Medium | Low to Medium — heading content contributes to topic relevance signals | Yes | Never force a keyword into a heading where it reads unnaturally |
| Use headings to break up content for readability | GRec / AR | Google SEO Starter Guide, WCAG | Current | High | Low for rankings — high for user experience and accessibility | Yes | Very short pages may not need subheadings |

### Heading Capitalisation

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use Title Case on headings | IP | TWG internal style guide | Internal | Medium | None for SEO — this is a brand consistency / style decision | Yes (as a style rule) | There is NO evidence that heading capitalisation affects rankings. Google does not distinguish title case from sentence case for ranking purposes. This is purely a brand/design choice. |

### Keyword Placement

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Primary keyword in title, H1, opening paragraph, and URL | GRec / IC | Google SEO Starter Guide, industry convention | Current | High | High collectively — these are the strongest on-page relevance signals | Yes | If the keyword doesn't fit naturally in the opening paragraph, a close variant in the first 100 words is sufficient |
| Secondary keywords in H2s and body content | IC | Industry convention | Ongoing | Medium | Medium — contributes to topical depth | Yes | Only where they fit naturally |
| Keywords should read naturally in context | GRec | Google Search Essentials (spam policies — keyword stuffing) | Current | High | Critical — unnatural keyword insertion can trigger spam classification | Yes | None |

### Keyword Density

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| There is NO target keyword density percentage | Clarification | Google (multiple statements by John Mueller, Gary Illyes; Google spam policies) | Current | High | N/A — keyword density as a metric has no confirmed relationship to rankings. Google does not use a keyword density threshold. | Yes | I do NOT apply a keyword density target. My current practice is "use the primary keyword 2–3 times naturally" which is a readability guideline, not a density target. I should clarify this distinction in all future work. |

### URL Structure

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use descriptive, readable URLs | GRec | Google SEO Starter Guide | Current | Medium | Low — URL content is a very minor ranking signal at best. Primary benefit is user comprehension and click-through. | Yes | CMS-generated URLs with IDs are not inherently harmful |
| Include primary keyword in URL slug | IC | Industry convention | Ongoing | Low | Low — Google has stated URLs are a very minor signal. The keyword in the URL helps users, not algorithms significantly. | Yes | Don't change existing URLs solely to add a keyword — redirects have their own costs |
| Keep URLs short and avoid unnecessary parameters | GRec | Google SEO Starter Guide | Current | Medium | Low for rankings — aids crawl efficiency and user readability | Yes | E-commerce sites with filter parameters are a legitimate exception |
| Don't repeat words already in the domain | IP | TWG keyword research skill | Current | Medium | None for SEO — prevents redundant slugs like `plumbingco.com.au/plumbing-repairs` | Yes | If the keyword phrase naturally includes the domain word and volume is significant, it may still be worth including |

### Internal Linking

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Link between related pages using descriptive anchor text | GRec | Google SEO Starter Guide | Current | High | High — internal links are a confirmed mechanism for distributing PageRank and helping Google discover and understand page relationships | Yes | None |
| Scale internal links with content length (2–3 for short pages, 7–10 for 1,200+ word pages) | IP | TWG service-page-copywriting skill | Internal | Medium | Medium — reasonable scaling, though no fixed formula exists from Google | Yes | The specific numbers are internal guidelines, not Google requirements |
| Use descriptive anchor text, not "click here" | GRec / AR | Google SEO Starter Guide, WCAG 2.4.4 | Current | High | Medium — anchor text helps Google understand the target page's topic. Accessibility requirement for screen readers. | Yes | None |

### Image Alt Text

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Every meaningful image should have descriptive alt text | GR / AR | Google Images best practices, WCAG 2.1 Level A (1.1.1) | Current | High | Medium — alt text is confirmed as used for Google Images ranking and general page understanding. Required for accessibility compliance. | Yes | Decorative images should have empty alt attributes (`alt=""`) per WCAG — not keyword-stuffed alt text |
| Alt text should describe the image accurately | GRec / AR | Google Images best practices, WCAG | Current | High | Medium | Yes | None |
| Include keywords in alt text only where they naturally describe the image | GRec | Google Images best practices | Current | Medium | Low — keyword-stuffed alt text is a spam signal. Natural descriptions that happen to include the keyword are fine. | Yes | If the image doesn't depict the keyword's subject, don't force it in |

### Schema Markup (General)

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use structured data where it is supported by Google and relevant to the page content | GRec | Google Structured Data documentation | Current | High | Medium — schema can enable rich results and help Google understand entities, but is NOT required for ranking or for appearing in AI search features | Yes | Do not add schema types that Google doesn't support for rich results unless there's a specific non-search reason |
| Only populate schema properties with accurate, verifiable data | GR | Google Structured Data policies | Current | High | Critical — fabricated or misleading structured data violates Google's policies and can result in manual actions | Yes | None |
| Schema markup is NOT required for AI Overviews or AI Mode | Clarification | Google (confirmed in official documentation) | Current (2026) | High | N/A — this is a correction to a common misconception. Google has stated structured data is not required for AI search visibility. | Yes | Still useful for traditional rich results, but should not be recommended as an "AI search visibility" tool |

### LocalBusiness Schema

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Include LocalBusiness (or more specific subtype) schema on relevant pages | GRec | Google Structured Data — Local Business | Current | High | Medium — supports local search features and knowledge panel accuracy | Yes | Only for businesses with a physical location or defined service area |
| Required properties: name, address, telephone | GRec | Google Structured Data — Local Business | Current | High | Medium | Yes | Service-area businesses without a storefront may omit full address per Google's guidelines |
| Only populate properties with verified, current information | GR | Google Structured Data policies | Current | High | Critical | Yes | Do NOT populate fax numbers, multiple phone numbers, or other fields just because they exist in the schema vocabulary. Only add what is accurate and useful. |

### FAQ Schema

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| FAQ schema will NOT produce FAQ rich results for ordinary local business websites | Clarification (updated) | Google Search Central Blog — FAQ rich results eligibility change | May 2026 | High | Low — Google restricted FAQ rich results to well-known, authoritative government and health websites. Local trade businesses will NOT see FAQ rich results from this markup. | Yes | **Still write visible FAQ content on the page** — it's valuable for users, for AI snippet extraction, and for featured snippet eligibility. The schema *markup* itself is optional/low-priority. |

### Service Schema

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Google does not currently support a "Service" rich result type | Clarification | Google Structured Data documentation (supported types list) | Current | High | Low — Service schema (schema.org/Service) exists in the vocabulary but Google does not generate rich results from it. Adding it may help entity understanding but has no visible SERP feature. | Yes | Can be included for semantic clarity if it's accurate, but should not be described as producing a SERP feature or as a high-priority SEO task |

### Review / AggregateRating Schema

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| First-party review markup on a business's own homepage is not eligible for review rich results | GR | Google Structured Data — Review snippet policies | Current | High | N/A — Google explicitly prohibits self-serving reviews marked up on the business's own site for rich result eligibility | Yes | Third-party review platforms (Google Reviews, ProductReview, etc.) can mark up reviews on their own sites. Businesses should link to or embed these, not mark up their own testimonials with AggregateRating. |

### Location Pages

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Location pages should contain unique, genuinely useful content specific to that location | GRec | Google SEO Starter Guide, Google helpful content system | Current | High | High — thin, template-only location pages with just the suburb name swapped are at risk under Google's helpful content and spam policies | Yes | None |
| Location pages rank because of relevance, authority, and content quality — not because a suburb name appears repeatedly | Clarification | Google (multiple sources, including helpful content guidance) | Current | High | N/A — location keyword repetition alone does not drive rankings. Local relevance comes from content quality, GBP signals, backlinks, citations, and genuine local detail. | Yes | None |

### Duplicate Content

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Avoid substantive duplicate content across pages | GRec | Google Search Central — Duplicate content | Current | High | High — Google consolidates duplicate URLs and may choose the wrong canonical, reducing visibility for the intended page | Yes | Syndicated content with proper canonical tags, printer-friendly versions, legitimate cross-posting with attribution |
| Duplicate content is NOT a "penalty" — Google filters, it doesn't penalise | Clarification | Google (confirmed repeatedly by John Mueller) | Current | High | N/A — Google deduplicates at the indexing stage. There is no "duplicate content penalty" as a manual or algorithmic action. | Yes | The practical effect (consolidation/filtering) can still hurt visibility, even without a formal penalty |

### Canonical Tags

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use self-referencing canonical tags on all indexable pages | GRec | Google Search Central — Consolidate duplicate URLs | Current | High | Medium — helps prevent URL parameter and tracking issues from creating duplicate indexing | Yes | Google treats canonicals as hints, not directives. If the content contradicts the canonical (e.g. the canonical points to a completely different page), Google may ignore it. |
| Use cross-domain canonical tags when content is legitimately syndicated | GRec | Google Search Central — Consolidate duplicate URLs | Current | High | Medium | Yes | Only for genuinely duplicated content, not as a redirect substitute |

### XML Sitemaps

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Submit an XML sitemap via Google Search Console | GRec | Google Search Central — Sitemaps overview | Current | High | Medium — sitemaps help Google discover pages, especially on larger or newer sites. Not required for small, well-linked sites. | Yes | Sites with fewer than ~500 well-interlinked pages may not need a sitemap, but it's still good practice |
| Only include indexable, canonical URLs in the sitemap | GRec | Google Search Central — Sitemaps best practices | Current | High | Low — including non-indexable pages in sitemaps wastes crawl budget signals and creates noise | Yes | None |
| Keep the sitemap updated when pages are added/removed | GRec | Google Search Central — Sitemaps best practices | Current | Medium | Low | Yes | Static sites with infrequent changes get less benefit |

### Robots.txt

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Use robots.txt to manage crawler access to non-essential resources | GRec | Google Search Central — Robots.txt introduction | Current | High | Medium — improper robots.txt can block critical pages. Primarily a crawl management tool, not a ranking tool. | Yes | robots.txt does NOT remove pages from Google's index — it prevents crawling. Use noindex for deindexing. |
| Do not use robots.txt to hide pages from search results | Clarification | Google Search Central | Current | High | Critical — blocked pages can still appear in search results (with no snippet). This is a common misunderstanding. | Yes | None |

### Core Web Vitals

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Meet "Good" thresholds: LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1 | GR (ranking signal) | Google Search Central — Page Experience | Current (INP replaced FID, March 2024) | High | Medium — CWV is a confirmed ranking signal, but a relatively minor one compared to relevance and content quality. A page with great content and poor CWV will still outrank a page with perfect CWV and thin content. | Yes | CWV is measured on field data (CrUX), not lab data. If a page has insufficient field data, CWV doesn't apply as a signal for that page. |

### Page Speed

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Page speed matters for user experience and is factored into CWV | GRec | Google Search Central — Page Experience | Current | High | Medium — speed contributes to LCP (the loading metric in CWV). Beyond CWV, speed affects bounce rate and conversion. | Yes | Speed improvements beyond "Good" CWV thresholds have diminishing returns for rankings. The biggest impact is going from "Poor" to "Good", not from "Good" to "Perfect". |

### Mobile Usability

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Site must be mobile-friendly (responsive design) | GR | Google — Mobile-first indexing | Current (mobile-first indexing is default for all sites) | High | Critical — Google predominantly uses the mobile version of content for indexing and ranking. A site that is not mobile-usable is effectively invisible. | Yes | None |

### Backlinks

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Backlinks from relevant, authoritative sites are a ranking signal | GR | Google (confirmed as one of the top ranking signals since PageRank; reiterated in various forms, though Google has stated its importance has been reduced over time) | Current | High | High — still a significant ranking factor, though Google has stated it is less important than it once was | Yes | The quality and relevance of backlinks matter far more than quantity. A few relevant links from authoritative sites outperform hundreds of low-quality links. |
| Do not buy links, participate in link schemes, or use manipulative link building | GR | Google Search Essentials — Link spam policies | Current | High | Critical — link spam violations can result in manual actions or algorithmic devaluation | Yes | Sponsored/paid links should use `rel="sponsored"`. Guest post links should use `rel="nofollow"` if the primary purpose is link acquisition. |
| "Domain Authority" is a third-party metric, not a Google ranking factor | Clarification | Moz (creator of DA), Google (has stated they don't use DA) | Current | High | N/A — useful as a comparative benchmark, but should never be described as a Google metric or ranking factor | Yes | DataForSEO's "Domain Rank" is similarly a third-party metric |

### E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness)

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| E-E-A-T is a quality concept, not a direct ranking factor | Clarification | Google Search Quality Rater Guidelines, Google Search Central | Current | High | High conceptually — E-E-A-T describes the qualities Google's systems aim to reward, but it is not a single score or algorithm. It's a framework human quality raters use. | Yes | More critical for YMYL (Your Money or Your Life) topics. For trade services, it means: show real credentials, real experience, real local knowledge — not just claim expertise. |
| Demonstrate first-hand experience (the first "E") | GRec | Google (added "Experience" to E-A-T in December 2022) | Current | High | Medium — content that demonstrates genuine first-hand experience is preferred over content that merely summarises information | Yes | For trade businesses: project photos, case studies, named team members, and specific local knowledge all signal first-hand experience |

### Content Freshness

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Content freshness matters for time-sensitive queries | GR | Google (freshness systems/QDF — Query Deserves Freshness) | Current | High | Context-dependent — freshness is a ranking signal ONLY for queries where timeliness matters (news, events, regulations). For evergreen service pages, freshness is irrelevant to rankings. | Yes | Do not update a plumbing service page's date just to appear "fresh" — Google can detect superficial date changes. Meaningful content updates are different from cosmetic date bumps. |

### AI-Generated Content

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| AI-generated content is NOT automatically penalised | GR | Google Search Central Blog — "AI-generated content" guidance (February 2023, reiterated 2024) | Current | High | N/A — Google's position is that it rewards high-quality content regardless of how it's produced. The focus is on quality, not production method. | Yes | AI-generated content that is spammy, thin, or mass-produced to manipulate rankings IS subject to spam policies — but that's the spam, not the AI. |
| Content should demonstrate E-E-A-T regardless of production method | GRec | Google Search Central | Current | High | High — AI-generated content that lacks human review, expert input, or genuine value is at higher risk of being classified as unhelpful | Yes | AI-assisted content that is reviewed, edited, and enriched with genuine expertise is treated the same as human-written content |

### AI Search Visibility

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Structured data is NOT required for AI Overviews or AI Mode | Clarification | Google (official documentation, 2025–2026) | Current | High | N/A — this is a correction to a widespread misconception. Standard SEO fundamentals (clear content, good structure, E-E-A-T) apply to AI search features. No special schema or markup is required. | Yes | AIO sources from the regular index. Being well-indexed and having clear, citable content is what matters. |
| Good SEO fundamentals are the best strategy for AI search visibility | GRec / IC | Google, industry consensus | Current | High | Medium — clear writing, factual accuracy, structured headings, and authoritative content are what AI systems extract from. No separate "AI SEO" playbook is needed. | Yes | This is an emerging area. Monitoring how AI systems source and cite content is worthwhile, but "optimising for AI" currently means "doing good SEO." |

### Google Business Profile Optimisation

| Rule | Classification | Source | Source Date | Confidence | Likely Impact | Current | Exceptions |
|---|---|---|---|---|---|---|---|
| Claim and fully populate the Google Business Profile | GRec | Google Business Profile Help Center | Current | High | High for local search — GBP is the primary driver of local pack / map pack visibility | Yes | None for local businesses |
| Keep NAP (Name, Address, Phone) consistent across GBP, website, and citations | IC | Industry convention (supported by Google's local search documentation) | Ongoing | High | High for local search — inconsistent NAP data reduces confidence in the business entity | Yes | Businesses going through a rebrand or address change need a coordinated transition, not just an update |
| Respond to reviews | GRec | Google Business Profile Help Center | Current | Medium | Low to Medium for rankings — Google has hinted review response may factor in, but the primary benefit is user trust and conversion | Yes | None |
| Use Google Business Profile categories accurately | GRec | Google Business Profile Help Center | Current | High | High for local search — primary category selection directly affects which searches the business appears for | Yes | None |

---

## 3. Potentially Outdated Recommendations — Assessment

### Claim: H1 headings must use title case or uppercase

**Classification: Unsupported**

There is no evidence — from Google or from any reputable study — that heading capitalisation affects search rankings. Google processes the text content of headings for relevance signals, not their formatting or case. Title case vs sentence case is a brand style decision, an accessibility consideration, or an internal preference. It should never be described as an SEO improvement.

*Primary source:* Google SEO Starter Guide makes no mention of heading capitalisation. Google's John Mueller has confirmed heading format is not a ranking signal.

### Claim: Every page must contain exactly one H1 for ranking purposes

**Classification: Generally recommended (but not required for ranking)**

Google has explicitly stated that multiple H1 tags on a page are fine from a ranking perspective. John Mueller confirmed this in a 2019 Webmaster Hangout and has reiterated it since. The convention of using a single H1 is a good practice for content clarity, accessibility (screen readers benefit from a clear document outline), and maintainability — but violating it does not harm rankings.

*Primary source:* Google Search Central — "Our systems don't have a problem when it comes to multiple H1 headings on a page." (John Mueller, 2019, corroborated by Google documentation which does not require a single H1.)

### Claim: Keywords must appear at a fixed density

**Classification: Outdated / Incorrect**

Google does not use keyword density as a ranking signal. There is no target percentage. Google's spam policies explicitly warn against "keyword stuffing" — unnaturally high repetition of keywords. The concept of an optimal keyword density (e.g. 2–3%) was debunked over a decade ago and has never been confirmed by Google.

My current practice of "use the primary keyword 2–3 times naturally" is a readability guideline to ensure the keyword appears on the page, NOT a density target. I should state this distinction clearly in all future work.

*Primary source:* Google Search Essentials — Spam policies (keyword stuffing). Matt Cutts (when at Google, 2011): "There is no ideal keyword density."

### Claim: Meta descriptions directly improve rankings

**Classification: Incorrect**

Google has confirmed, repeatedly and explicitly, that meta descriptions are NOT a ranking signal. They do not affect where a page ranks. Their value is in click-through rate (CTR) — a well-written meta description can improve clicks from the SERP, and there is debate about whether CTR itself is a ranking signal, but the meta description text is not used for ranking.

*Primary source:* Google Search Central — "Even though meta descriptions are not a ranking factor…" (Google SEO Starter Guide).

### Claim: Every page needs a minimum word count

**Classification: Incorrect**

Google has stated there is no minimum word count for ranking. Content should be as long as it needs to be to serve the user's query. A 300-word page that perfectly answers a query will outrank a 3,000-word page that buries the answer in padding.

The TWG client blog writing skill specifies 1,000–1,500 words as a target range — this is an internal quality guideline based on the depth needed to cover trade topics properly, not a Google requirement.

*Primary source:* John Mueller (Google, 2021): "Word count is not a ranking factor." Google's helpful content system rewards content that provides a satisfying experience, regardless of length.

### Claim: Fax numbers should be included in LocalBusiness schema

**Classification: Outdated / Unnecessary**

The `faxNumber` property exists in the Schema.org LocalBusiness vocabulary, but there is no SEO benefit to including it. Most trade businesses do not have fax numbers. Populating schema properties with irrelevant or fabricated data (e.g. adding a fax number the business doesn't have) would violate Google's structured data policies. Only populate properties with accurate, current information that serves a purpose.

*Primary source:* Google Structured Data policies — "Structured data should be an accurate representation of the page content."

### Claim: All available schema properties should be populated

**Classification: Incorrect**

Google's structured data documentation specifies which properties are **required** and which are **recommended** for each schema type. Only required properties are mandatory for rich result eligibility. Recommended properties may improve the rich result appearance. Optional/undefined properties have no SEO benefit and should only be added if they're accurate and useful.

Populating every available property regardless of relevance is busywork at best and a policy violation at worst (if the data is inaccurate).

*Primary source:* Google Structured Data documentation — each type lists "Required" and "Recommended" properties explicitly.

### Claim: FAQ schema will normally produce FAQ rich results for local businesses

**Classification: Outdated (as of May 2026)**

Google changed FAQ rich result eligibility in 2023 (initially restricted) and further in 2026. As of May 2026, FAQ rich results are only shown for well-known, authoritative government and health websites. Local trade businesses — plumbers, electricians, solar installers — will NOT see FAQ rich results from FAQPage schema markup.

**Visible FAQ content on the page remains valuable** — for user experience, for featured snippet eligibility, and for AI search snippet extraction. But the FAQ *schema markup* itself is optional and low-priority. It should not be presented as a meaningful visibility feature for TWG clients.

*Primary source:* Google Search Central Blog — FAQ rich result eligibility changes. Confirmed in TWG learnings from Clean Earth Solar audit review (2026-07-20).

### Claim: Exact-match keywords must appear in every heading

**Classification: Unsupported**

Google's systems use natural language processing and semantic understanding. Exact-match keywords in every heading are unnecessary and often produce robotic, unreadable content. Keywords should appear in headings where they fit naturally — typically the H1 and one or two H2s. Forcing the exact keyword into every heading is a form of over-optimisation that can hurt readability without improving rankings.

*Primary source:* Google SEO Starter Guide recommends using headings to "organize your content" — not to insert keywords. Google's systems understand synonyms, related terms, and semantic equivalents.

### Claim: Changing a heading's capitalisation is an SEO priority

**Classification: Incorrect**

Heading capitalisation has zero effect on search rankings. Changing an H1 from sentence case to title case (or vice versa) is a brand consistency or editorial decision, never an SEO task. Recommending this as part of an SEO audit creates busywork with no search benefit.

*Primary source:* No Google documentation mentions heading capitalisation as a ranking or quality signal. This is a confirmed anti-pattern from TWG audit learnings (2026-07-20).

### Claim: Location pages rank mainly because the suburb name appears repeatedly

**Classification: Incorrect**

Repeating a suburb name does not create local relevance. Location pages rank because of content quality, genuine local detail (local conditions, property types, council requirements, climate factors), GBP signals, NAP consistency, local backlinks, and the site's overall authority. A page that mentions "Frankston" twelve times but provides no genuinely useful local content will be outperformed by a page that mentions it naturally and provides real local value.

*Primary source:* Google's helpful content system and spam policies (keyword stuffing). Google's local search documentation focuses on relevance, distance, and prominence — not keyword repetition.

### Claim: AI-generated content is automatically penalised

**Classification: Incorrect**

Google has explicitly stated that AI-generated content is not automatically penalised. Google's focus is on content quality, not production method. Content that is helpful, reliable, and people-first is treated the same regardless of whether it was written by a human, an AI, or a combination. Content that is mass-produced, low-quality, or designed to manipulate rankings IS subject to spam policies — but that applies equally to human-written spam.

*Primary source:* Google Search Central Blog — "AI-generated content guidance" (February 2023): "Our focus on the quality of content, rather than how content is produced, is a useful guide."

### Claim: A high SEO-tool score means a page is well optimised

**Classification: Incorrect**

SEO tool scores (e.g. Ahrefs Health Score, SEMrush Site Audit score, Screaming Frog's scoring, DataForSEO's page quality scores) are proprietary metrics based on each tool's own criteria. They do not represent Google's assessment of a page. A page can score 95/100 on an SEO tool and rank poorly. A page can have a "failing" tool score and rank #1.

Tool scores are useful as a structured checklist for identifying potential issues, but they should never be presented to clients as a measure of SEO quality or used as the basis for prioritising fixes.

*Primary source:* Every major SEO tool's own documentation acknowledges its scores are proprietary. Google does not publish or endorse any third-party scoring system.

---

## 4. SEO vs Other Recommendations — Category Labels

Every recommendation I make should be clearly labelled with its primary domain. The following labels apply:

| Recommendation | Primary Domain | Notes |
|---|---|---|
| Primary keyword in title tag | **Ranking** | Confirmed ranking signal |
| Primary keyword in H1 | **Ranking** | Confirmed (minor) ranking signal |
| Meta description content | **Search-result appearance** | NOT a ranking signal — affects CTR in SERPs |
| Meta description length (150–160 chars) | **Search-result appearance** | Display guideline, not a ranking factor |
| Heading hierarchy (H1→H2→H3) | **Accessibility** | WCAG requirement; minor relevance signal for Google |
| Heading capitalisation (title case vs sentence case) | **Brand consistency** | No SEO impact whatsoever |
| Keyword density target | **SEO tool scoring** | Not a real Google signal — should not be applied |
| URL structure / slug | **User experience** | Very minor ranking signal at best |
| Image alt text | **Accessibility / Ranking** | WCAG requirement AND used by Google Images |
| Internal linking | **Ranking / Crawling** | Confirmed mechanism for PageRank flow and discovery |
| Schema markup (general) | **Search-result appearance / Indexing** | Enables rich results; aids entity understanding. NOT required for rankings or AI search. |
| LocalBusiness schema | **Search-result appearance** | Supports knowledge panel and local features |
| FAQ schema markup | **Search-result appearance** | Low priority since May 2026 — no rich results for local businesses |
| Visible FAQ content | **User experience / Search-result appearance** | Valuable for users and featured snippets — separate from schema markup |
| Core Web Vitals | **Ranking** (confirmed, minor) | Confirmed page experience signal — but minor compared to content relevance |
| Page speed beyond CWV thresholds | **User experience / Conversion rate** | Diminishing returns for ranking once CWV is "Good" |
| Mobile responsiveness | **Ranking** (confirmed, critical) | Required for mobile-first indexing |
| Content word count | **Content quality** (not ranking) | No minimum word count for ranking — length should match query intent |
| Backlinks | **Ranking** | Confirmed ranking signal — quality over quantity |
| E-E-A-T signals | **Content quality** | Quality framework, not a direct algorithm — but indirectly affects all ranking |
| Content freshness (date updates) | **Ranking** (only for time-sensitive queries) | Irrelevant for evergreen service pages |
| Review schema on own site | **Code validity** | Not eligible for rich results on the business's own domain |
| Title case headings | **Brand consistency** | Never present as an SEO recommendation |
| Minimum word count | **Content quality** (internal guideline) | Not a Google requirement |
| XML sitemap submission | **Crawling / Indexing** | Helps discovery, not ranking |
| Robots.txt configuration | **Crawling** | Controls crawler access, does NOT control indexing |
| Canonical tags | **Indexing** | Consolidates duplicate URLs — Google treats as a hint |
| GBP optimisation | **Local search visibility** | Primary driver of local pack visibility — separate from organic rankings |

---

## 5. Evidence Hierarchy — Adopted

I will use the following hierarchy for all future SEO recommendations:

| Level | Definition | Example |
|---|---|---|
| **Level 1** | Explicitly documented by Google or another relevant search engine | "Google confirms CWV as a ranking signal" — linked to Google Search Central documentation |
| **Level 2** | Supported by repeatable industry research or testing | "Ahrefs study of 1M pages found title tag correlation with rankings" — study linked, methodology described |
| **Level 3** | Widely accepted implementation convention | "Use descriptive anchor text for internal links" — universally recommended, common sense, but not a formally documented Google rule with specific requirements |
| **Level 4** | Reasonable hypothesis requiring testing | "Responding to GBP reviews may improve local rankings" — plausible, some indirect evidence, but not confirmed and not testable without controlled experiment |
| **Level 5** | Personal, stylistic, or tool-specific preference | "Use title case headings" — a style choice. "Fix all issues flagged by Screaming Frog" — a tool's scoring system. |

**Commitment:** Every recommendation in future audits will include its evidence level. A Level 3, 4, or 5 recommendation will NEVER be described as a Google requirement.

---

## 6. Impact Framework — Adopted

I will use the following impact classifications for all future audit findings:

| Classification | Definition | Examples |
|---|---|---|
| **Critical** | Likely to prevent crawling, indexing, or normal site operation | Robots.txt blocking critical pages; site-wide noindex tag; broken SSL certificate; server returning 5xx errors on key pages |
| **High** | Strong potential to materially affect organic visibility or lead generation | Missing or duplicate title tags on key service pages; no mobile responsiveness; no GBP listing; site-wide broken internal linking; no indexable content on critical pages |
| **Medium** | Worthwhile improvement with a plausible but limited effect | Missing meta descriptions; heading hierarchy issues; image alt text gaps; page speed improvements within CWV "Needs Improvement" range; incomplete LocalBusiness schema |
| **Low** | Minor optimisation, quality improvement, or preventative maintenance | URL structure cleanup; minor redirect chains; adding recommended (not required) schema properties; improving anchor text specificity |
| **Informational** | Preference, observation, or optional enhancement | Heading capitalisation style; FAQ schema markup (post-May 2026); populating optional schema fields; SEO tool score improvements; cosmetic formatting changes |

**Commitment:** An issue will NOT be classified as high priority merely because an auditing tool flags it. Tool flags will be cross-referenced against the evidence hierarchy (Section 5) and this impact framework before being included in any audit.

---

## 7. Uncertainty Acknowledgements

### Areas where evidence is unclear or conflicting

| Topic | What's uncertain | What I recommend instead of guessing |
|---|---|---|
| **CTR as a ranking signal** | Google has never confirmed that click-through rate from SERPs is used as a ranking signal. Some industry studies suggest correlation, but correlation ≠ causation. Google's Navboost system (revealed in leaked documents) suggests user engagement signals are used, but specifics are unconfirmed. | State that meta descriptions and title tags may improve CTR, which has *possible* ranking benefits. Do not claim CTR is a confirmed ranking factor. Recommend optimising titles/descriptions for clicks based on conversion logic, not ranking assumptions. |
| **Backlink importance trajectory** | Google has stated backlinks are less important than they once were, but has not quantified how much less. Some SEO practitioners believe links are still the #1 factor; others believe they've been largely superseded by content quality and entity signals. | Acknowledge backlinks are a confirmed signal with unclear weighting. Focus on earning relevant links through valuable content and real business relationships. Do not recommend link building as the primary SEO strategy without evidence of a specific link deficit. |
| **AI search citation behaviour** | How Google's AI Overviews, ChatGPT, Perplexity, and other AI systems select and cite sources is not fully understood. Structured data, schema, and specific optimisations are frequently recommended but are NOT confirmed as requirements. | Recommend good SEO fundamentals (clear content, structured headings, factual accuracy, E-E-A-T) as the best strategy for AI visibility. Do not recommend specific "AI SEO" tactics without evidence. Monitor and test. |
| **GBP ranking factors** | Google's local ranking algorithm (local pack) considers relevance, distance, and prominence, but the specific weighting and sub-factors are not documented. Category selection, review count, review content, and GBP post activity are all hypothesised to matter, with varying levels of evidence. | Recommend GBP best practices (complete profile, accurate categories, regular review engagement) based on Level 2–3 evidence. Do not claim specific GBP actions will produce specific ranking improvements without testing. |
| **Content freshness for evergreen pages** | Whether updating an evergreen service page's content (not just the date) produces a ranking boost is debated. Google's freshness systems primarily apply to time-sensitive queries. Some practitioners report improvements after content refreshes, but this may be correlation with content *improvement*, not freshness itself. | Recommend content updates when the content is genuinely outdated, incomplete, or can be improved — not as a routine "freshness" tactic. If recommending a content refresh, specify what should change and why, not just "update the date." |
| **Exact impact of heading keywords** | Heading content is a ranking signal, but its weight relative to title tags, body content, and other signals is not quantified. | Recommend including keywords in headings where natural. Do not overstate the impact or recommend keyword-stuffing headings. |

### How I will handle uncertainty in future audits

1. **State uncertainty clearly** — if the evidence is mixed or absent, say so
2. **Do not invent a definitive rule** — distinguish between "Google requires this" and "this is generally considered helpful"
3. **Explain what additional information would help** — e.g. "Check Search Console performance data for this page to see if this is actually causing a problem"
4. **Recommend validation through data** — Search Console, GA4, crawl data, or controlled testing rather than assumptions
5. **Distinguish correlation from causation** — when citing industry studies, note whether they show correlation or confirmed causation

---

## 8. Knowledge-Gap Report

### Areas where my knowledge may be outdated

| Area | Risk | Mitigation |
|---|---|---|
| **Google algorithm updates post-training** | My training data has a cutoff. Algorithm updates, new SERP features, or policy changes after that date may not be reflected in my base knowledge. | Always verify against live Google Search Central documentation before making recommendations. Use web search for recent changes. |
| **AI search feature evolution** | AI Overviews, AI Mode, and competing AI search tools are evolving rapidly. Best practices for appearing in AI-generated answers are not established. | Monitor Google's official guidance. Do not recommend speculative "AI SEO" tactics. Test and observe. |
| **Google Business Profile feature changes** | GBP regularly adds and removes features (e.g. Posts, Q&A, messaging, product listings). Current feature availability may differ from my training data. | Verify current GBP features before recommending specific actions. |
| **Schema markup eligibility changes** | Google regularly changes which schema types produce rich results. FAQ schema eligibility was reduced in 2023 and again in 2026. Other types may change similarly. | Check Google's [supported structured data types](https://developers.google.com/search/docs/appearance/structured-data/search-gallery) before recommending any schema as "producing rich results." |
| **Local SEO ranking factors** | Google's local search algorithm is opaque and evolves. The relative importance of categories, reviews, proximity, links, and on-page signals shifts over time. | Use Level 2–3 evidence with appropriate uncertainty disclosure. Don't claim specific local ranking formulas. |

### Recommendations I have previously made that should be reconsidered

| Past recommendation | What should change | Why |
|---|---|---|
| **FAQ schema as a standard recommendation** | Downgrade to Informational/optional | FAQ rich results no longer show for local businesses (May 2026). Visible FAQ content is still valuable; the markup is not. |
| **"Fix all technical issues flagged by DataForSEO"** | Triage each issue against evidence hierarchy and impact framework | Not all tool-flagged issues affect SEO. Cosmetic issues (like heading capitalisation) should not be presented as SEO findings. |
| **Competitor identification from DataForSEO overlap data** | Filter out aggregators/marketplaces | DataForSEO "competitor overlap" shows keyword overlap, not business competition. Lead aggregators (SolarQuotes, HiPages, etc.) must be filtered. Use client-named competitors first. |
| **Recommending schema "for AI search visibility"** | Remove this recommendation | Google has confirmed structured data is not required for AI Overviews or AI Mode. |
| **Treating tool scores as audit findings** | Stop reporting tool scores as SEO metrics | Tool scores are proprietary. Report the underlying issues, not the score. |

### Areas requiring live research before any recommendation

| Area | What needs verification | How to verify |
|---|---|---|
| SERP features for specific Australian queries | Which rich results actually appear for the client's target keywords in the Australian market | Run test searches, check SERP features in DataForSEO or Ahrefs |
| Current GBP feature set | What features are currently available and which have been deprecated | Check Google Business Profile Help Center |
| Specific CMS or theme limitations | Whether the client's WordPress theme or page builder supports schema, proper heading structure, etc. | Crawl the site and inspect the HTML |
| Competitor landscape | Who the real business competitors are (vs keyword-overlap competitors from tools) | Ask the client, verify from onboarding data |
| Client-specific conversion data | Whether a specific recommendation will improve leads for this client | Requires GA4, Search Console, and CRM data analysis |

### Subjects where Google provides no definitive rule

| Subject | Google's position | Practical approach |
|---|---|---|
| Optimal content length | No minimum or maximum. "Make it as long as it needs to be." | Use content depth and query intent to determine length. Internal guidelines (1,000–1,500 for blogs) are quality benchmarks, not SEO rules. |
| Ideal number of internal links | No stated limit or recommendation beyond "use them to help users navigate." | Scale with content length and link where it genuinely helps the reader. |
| How many keywords to target per page | No stated limit. | Focus on one primary topic with natural variations. The concept of "one keyword per page" is an industry simplification, not a Google rule. |
| Exact heading hierarchy requirements | Google says multiple H1s are fine. Heading hierarchy is a recommendation, not a requirement. | Follow heading hierarchy for accessibility and clarity, but don't treat hierarchy violations as ranking issues. |
| When to use noindex vs canonical vs robots.txt | Google provides guidance on each tool individually but the decision of which to use in specific situations requires judgment. | Match the tool to the intent: noindex to prevent indexing, canonical to consolidate, robots.txt to prevent crawling. Test in staging first. |
| Whether GBP reviews directly affect rankings | Google says local ranking depends on relevance, distance, and prominence. Reviews are part of "prominence" but the specific mechanism is not documented. | Encourage review engagement for business reasons. Don't claim a specific number of reviews will produce a specific ranking improvement. |

### Proposed safeguards to prevent outdated advice in future audits

1. **Pre-audit verification step:** Before any audit, verify current Google documentation for any schema types, SERP features, or ranking signals being recommended. Web search for recent changes in the past 6 months.

2. **Evidence level on every recommendation:** Every finding in every audit must include its evidence level (1–5). This forces me to source and verify each claim.

3. **Impact classification on every finding:** Every finding must include its impact level (Critical / High / Medium / Low / Informational). This prevents tool-generated noise from being presented as high-priority work.

4. **Tool-flag triage:** SEO tool warnings are a starting point for investigation, not a finished finding. Every tool flag must be assessed against primary sources before inclusion in the audit.

5. **Competitor verification:** Never use DataForSEO competitor overlap data without filtering for aggregators, marketplaces, and non-business-competitor domains. Always check client onboarding data for named competitors first.

6. **Schema eligibility check:** Before recommending any schema type for "rich result visibility," verify the type is currently eligible on Google's [Search Gallery](https://developers.google.com/search/docs/appearance/structured-data/search-gallery).

7. **Periodic skill review:** The dataforseo_audit and copywriting skills should be reviewed quarterly against current Google documentation to catch any guidance that has drifted out of date.

8. **"Not an SEO issue" label:** Create a specific label for findings that relate to accessibility, brand consistency, code validity, or conversion — not ranking. Use it actively to prevent category confusion.

9. **Learnings capture:** After every audit review (like the Clean Earth Solar review on 2026-07-20), capture corrections as anti-patterns in the relevant skill files immediately.

---

## Summary

This audit exposes several areas where my recommendations need tightening:

1. **FAQ schema** was previously treated as a standard recommendation. It should now be Informational/optional for local businesses.
2. **Tool scores** were sometimes used as proxy measures of SEO quality. They are proprietary metrics with no Google backing.
3. **Heading capitalisation** was included in some audits as an SEO finding. It has zero ranking impact.
4. **Competitor identification** relied too heavily on DataForSEO overlap data without filtering.
5. **AI search schema** was sometimes recommended for AI visibility. Google has confirmed this is unnecessary.
6. **Keyword density** language in current skills is close to correct ("2–3 times naturally") but risks being misread as a density target. The distinction needs to be explicit.

The evidence hierarchy (Section 5) and impact framework (Section 6) are ready for adoption. Every future audit should enforce both.

This document is the foundation — the SEO Playbook should be built on top of it after your review.
