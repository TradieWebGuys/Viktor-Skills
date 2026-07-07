# Report Specification

## Individual Call Report Sections

### 1. Call Details
- Staff member name
- Contact name and number
- Duration (formatted as minutes:seconds)
- Direction (inbound/outbound)
- Date and time (AEST)
- Call type (sales enquiry, service call, follow-up, general)

### 2. Overall Assessment
- **Score**: out of 10, based on criteria below
- **Sentiment**: positive / neutral / negative
- **Outcome**: booked / lost / voicemail / follow-up required / general enquiry

### 3. Executive Summary
2–3 sentences covering what the call was about, how it went, and the outcome.

### 4. Sentiment Analysis
Track emotional trajectory for both staff and caller through the call:
- Opening sentiment
- Mid-call shifts
- Closing sentiment
- Key moments that shifted sentiment (with timestamps)

### 5. Outcome Classification and Action Items
- Primary outcome with confidence level
- Any commitments made (appointments, quotes, callbacks)
- Follow-up actions required, with responsible party

### 5b. Contact Detail Capture

A checklist of the essential lead details and whether each was captured and confirmed on the call. This applies to every sales/enquiry call — a great conversation that ends with no way to reach the lead is a failed call.

For each detail, record a **status** and a **source / note**. Status is one of:
- **On file** — already held before the call (e.g. the mobile dialled on an outbound callback, or an existing CRM record). Not a capture, and *not* a miss — don't coach the agent for failing to ask for something they already had.
- **Captured** — obtained or confirmed on the call.
- **Partial** — incomplete (e.g. first name but no surname).
- **Not captured** — needed but never obtained.

| Detail | Status | Source / note |
|--------|--------|---------------|
| Contact name (first + surname) | | |
| Phone number | | |
| Email address | | |
| Business name | | |
| Website / web address | | |
| Business location (suburb + state) | | |
| Service type | | |

**Match the check to the call direction — this matters:**
- **Outbound callback / dialled from a lead record:** the phone number is already on file. Mark it "On file", not a miss. The win condition is leaving with the details you *didn't* already have — typically email, business name, and web address.
- **Inbound call:** the number may sit in caller ID, but it should be verbally confirmed, along with the correct email. "It's probably in the system" is not capture.

Then flag:
- **Follow-up commitments vs what's actionable.** For each thing the agent promised (email, callback, quote), state whether it can actually be delivered with the details in hand. If the agent promised to email something but never got an email, that commitment is blocked — call it out as a broken-promise risk. If the callback is fine because the number is on file, say so rather than treating it as a failure.

Missing contact-detail capture is a **compliance and process** failure and should pull the overall score down accordingly (see Scoring Criteria).

### 6. What Went Well
3–5 specific strengths, each with a direct transcript quote as evidence. Focus on:
- Rapport building
- Objection handling
- Product knowledge
- Closing technique
- Active listening

### 7. Areas for Improvement
2–4 specific areas, each with:
- What happened in the call
- Why it matters
- A concrete coaching note on what to do differently

### 8. Coaching Opportunities
1–3 targeted coaching scripts — word-for-word alternatives the staff member can practise. Tied to the areas for improvement above.

### 9. Lead Quality Assessment (sales calls only)
- Lead score out of 10
- Budget signals
- Timeline signals
- Decision-maker status
- Service match quality

### 10. Call Tags
Auto-generated tags for filtering: e.g. `sales-enquiry`, `booked`, `high-value`, `coaching-priority`, `follow-up-needed`.

## Scoring Criteria

| Score | Meaning |
|-------|---------|
| 9–10 | Exceptional — textbook call, strong close, great rapport |
| 7–8 | Good — solid performance, minor areas to polish |
| 5–6 | Adequate — got the job done but missed opportunities |
| 3–4 | Below standard — significant issues affected the outcome |
| 1–2 | Poor — multiple failures, likely lost a winnable lead |

Scoring factors (weighted):
- **Greeting and introduction** (10%) — professional, warm, identified the business
- **Discovery and qualification** (20%) — asked the right questions, understood the need
- **Product/service knowledge** (15%) — accurate, confident information
- **Objection handling** (15%) — addressed concerns without being pushy
- **Closing and next steps** (20%) — clear CTA, booking attempt, follow-up plan
- **Communication skills** (10%) — clarity, pace, tone, active listening
- **Compliance and process** (10%) — followed company procedures, and captured/confirmed the essential contact details (name, phone, email, business name, web address). Committing to a follow-up (email, callback, quote) without capturing the detail needed to deliver it is a significant deduction here.

## Weekly Batch Report Format

For high-volume accounts (15+ calls/week), produce a single document covering the full period:

### Summary Dashboard
- Total calls processed
- Booking rate (booked / total non-voicemail calls)
- Average score
- Calls by outcome (booked, lost, voicemail, follow-up, general)
- **Contact-capture gaps** — count of sales/enquiry calls that ended without a confirmed phone or email, and any where a follow-up was promised but the detail to deliver it was missing
- Comparison with previous period (if available)

### Per-Staff Breakdown
For each staff member:
- Calls handled, average score, booking rate
- Top strength and priority coaching area
- Best call (highest score) and call needing most attention (lowest score)

### Call-by-Call Log
Table with: date, staff, contact, duration, score, outcome, one-line summary.

### Top Coaching Priorities
The 3 most impactful coaching areas across all staff, with evidence from specific calls.

### Notable Calls
Flag any calls that need immediate attention:
- Lost leads that were winnable
- Complaints or escalations
- Exceptional performances worth recognising
