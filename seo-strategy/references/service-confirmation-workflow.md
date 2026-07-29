# Service Confirmation Workflow

Triggered automatically after the client KB is created. Produces a ClickUp task listing extracted services and an expanded location breakdown for PM review.

## Trigger

After `twg-client-kb-creator` finishes creating the KB, Viktor creates a ClickUp subtask called **"Confirm Services & Locations"** in the client's onboarding list.

## Two-Tier Output

### Services — Straight Extraction (no elaboration)

Extract services exactly as stated in the questionnaire or onboarding form. List them as-is. Do NOT propose additional services — scope creep risk is too high. The PM will manually refine.

### Locations — Two-Tier with Suburb Expansion

**Tier 1 — Client-stated (verbatim)**
What the client said in their questionnaire. Could be a city ("Brisbane"), a region ("North Shore Sydney"), or a general area ("Canberra region").

**Tier 2 — Proposed suburb expansion (Viktor-generated)**
For each stated region, break it into suburbs ranked by search demand. This helps the PM decide which suburbs warrant dedicated location pages without having to research manually.

## How Suburb Expansion Works

### Step 1 — Generate suburb candidates

For each stated region, generate a list of known suburbs/areas. Use two sources:

1. **DataForSEO keyword suggestions** — call `pd_dataforseo_get_keyword_suggestions` with `keyword="{primary_service} {region}"` (e.g. "plumber brisbane"), `locationCode=2036`, `languageCode="en"`, `limit=50`. This returns location-specific keyword variants like "plumber logan", "plumber north brisbane". Extract the suburb/area names from these suggestions.

2. **General Australian geographic knowledge** — supplement with known suburbs for the region. For major metros, include key suburbs that may not appear in keyword suggestions but are commercially relevant (e.g. major residential areas, commercial centres).

Combine both sources into a deduplicated suburb list.

### Step 2 — Get search demand data

Batch all suburb-level keywords into a single DataForSEO call:

```python
keywords = [f"{primary_service} {suburb}" for suburb in suburb_list]
# Max 1000 per call — batch if needed
result = await pd_dataforseo_get_google_ads_search_volume(
    keywords=keywords,
    locationCode=2036,
    languageCode="en"
)
```

Extract search volume for each suburb keyword. Cost: ~$0.075 per batch of up to 1000 keywords.

### Step 3 — Rank and classify

| Priority | Criteria |
|----------|---------|
| **High** | Top 30% by search volume, or volume ≥ 100/month |
| **Medium** | Middle 40%, or volume 30–99/month |
| **Low** | Bottom 30%, or volume < 30/month |

Sort descending by search volume within each priority tier.

### Step 4 — Use the primary service only

Use the client's single most prominent service for the keyword queries — not every service. This keeps costs low (one batch call per region) and the primary service is a reliable proxy for overall local demand. The keyword research skill later covers all service × location combinations.

## ClickUp Task Format

Create in the client's onboarding list (or SEO list if onboarding is complete).

**Task name:** `Confirm Services & Locations — {CLIENT NAME}`
**Assignee:** PM (from ClickUp onboarding task or default)
**Status:** `in review`

**Task description (markdownDescription):**

```markdown
## Services (from questionnaire)

@Viktor extracted these services from the onboarding questionnaire. Confirm, edit, or add as needed.

- {Service 1}
- {Service 2}
- {Service 3}
- ...

---

## Locations

### Client-stated regions
- {Region 1} (verbatim from questionnaire)
- {Region 2}

### Proposed suburb breakdown — {Region 1}

Based on search demand for "{primary service}" in this region:

| Suburb | Est. monthly searches | Priority |
|--------|----------------------|----------|
| {Suburb A} | {volume} | High |
| {Suburb B} | {volume} | High |
| {Suburb C} | {volume} | Medium |
| {Suburb D} | {volume} | Medium |
| {Suburb E} | {volume} | Low |
| ... | ... | ... |

### Proposed suburb breakdown — {Region 2}
| Suburb | Est. monthly searches | Priority |
|--------|----------------------|----------|
| ... | ... | ... |

---

## What to do

1. **Services:** Delete any services the client doesn't want to promote. Add any missing ones.
2. **Locations:** Delete suburbs that are out of scope. Adjust priority if needed. Add any missing suburbs.
3. When done, mark this task complete. @Viktor will update the Client KB with your confirmed selections.

---
_Search volume data from DataForSEO (Google Ads keyword data, Australia). Volume = estimated monthly searches._
_Note: Services listed as-is from questionnaire. Location suburbs proposed based on search demand — PM to confirm._
```

## After PM Confirms

When the ClickUp automation fires (task completed → Slack message to Viktor):

1. Re-read the task description from ClickUp API (do not use cached version)
2. Parse the confirmed services and locations
3. Update the Client KB (`skills/clients/{shortcode}/SKILL.md`):
   - **Section 2 (Services)** — update to match confirmed list
   - **Section 3 (Service Areas)** — update Primary (high-priority suburbs), Extended (medium), full coverage label. Populate "Not Serviced" if PM deleted any proposed suburbs or noted exclusions.
4. Post Slack confirmation: "KB updated with confirmed services and locations for {CLIENT}"

## Edge Cases

- **Client gives a single suburb** (e.g. "Paddington") — no expansion needed. List as-is with a note: "Single suburb stated — consider expanding to neighbouring areas?"
- **Client gives a state** (e.g. "Queensland") — too broad for suburb expansion. Flag for PM: "Region is very broad. Please specify target cities/areas for suburb expansion."
- **New Zealand clients** — use `locationCode=2554` instead of 2036. Suburb dynamics are similar.
- **No search volume data** — if DataForSEO returns zero volume for all suburb keywords (very unlikely), fall back to listing suburbs by population and flag: "No search volume data found — suburbs listed by estimated population."
- **Multiple primary services** — still only query with the single most prominent service. Avoids cost multiplication and the keyword research skill handles the full matrix later.
