# PDF Template

The client-facing PDF is generated from HTML using `sdk.utils.render.html_to_pdf` or equivalent, styled to match the TWG brand.

## Brand Tokens (from `/work/brand/DESIGN.md`)

```css
:root {
  --navy: #1A1F2E;
  --lime: #8DC63F;
  --forest: #1F9C51;
  --white: #FFFFFF;
  --offwhite: #F5F4F2;
  --ink: #1A1F2E;
  --muted: #6B6560;
  --border: #E0DDD9;
  --font-heading: 'Outfit', 'Poppins', sans-serif;
  --font-body: 'Inter', sans-serif;
}
```

## Layout

### Cover Page
- Full Dark Navy background
- White TWG logo (centred, upper third)
- Report title: "Monthly SEO Report" in Outfit, white, large
- Client name below title in Lime Green
- Reporting period in white, smaller
- Generated date at bottom

### Section Pages
- Off-White `#F5F4F2` background
- Dark Navy page header bar with section title in white
- Lime Green accent for metric highlights, section markers, and positive change indicators
- Tables: white background, `#E0DDD9` borders, `#1A1F2E` text
- Positive changes: Lime Green text or background highlight
- No red, no decline indicators, no negative callouts

### Footer (every page except cover)
- Dark Navy bar
- White TWG logo (small, left)
- Page number (right)
- "Confidential — Prepared for {Client Name}" (centre, muted)

### Final Page
- CTA section with Lime Green accent border
- "Questions about this report? Reply to this email, or contact us at Support@TradieWebGuys.com.au"

## Typography

| Element | Font | Size | Weight | Colour |
|---------|------|------|--------|--------|
| H1 (section titles) | Outfit | 24px | 700 | `#1A1F2E` or `#FFFFFF` on dark |
| H2 (subsections) | Outfit | 18px | 600 | `#1A1F2E` |
| Body text | Inter | 12px | 400 | `#1A1F2E` |
| Table headers | Inter | 11px | 600 | `#FFFFFF` on `#1A1F2E` |
| Table cells | Inter | 11px | 400 | `#1A1F2E` |
| Metric values | Inter | 14px | 700 | `#1A1F2E` or `#8DC63F` for highlights |
| Muted/secondary | Inter | 10px | 400 | `#6B6560` |

## Logo URLs

- **White logo** (on dark backgrounds): `https://assets.cdn.filesafe.space/cuS7M6EnfbXM2s2VJ4I8/media/66e795f449587111bed8c101.png`
- **Dark logo** (on light backgrounds): `https://assets.cdn.filesafe.space/cuS7M6EnfbXM2s2VJ4I8/media/6a6848fbb7fe5a8e31ea40ca.jpg`

## Colour Rule

Dark Navy + Lime Green as the only prominent colours. Never introduce additional accent colours. Forest Green `#1F9C51` used sparingly if needed for secondary indicators.

## Charts and Graphs

Where possible, include visual charts (traffic trends, channel breakdowns, GBP performance). Generate as inline SVG or PNG within the HTML. Use the brand palette only.

## Important

The PDF content comes from the **re-read** ClickUp task description (Section 11), not from memory. See `clickup-output.md` for the re-read rule.
