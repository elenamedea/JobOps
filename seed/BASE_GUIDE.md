# JobOps - Public Template

Reference implementation of a job-search tracking system, demonstrating linked-record data modelling in place of free text.
Seeded with fictional data only: GreenGrid Analytics GmbH, Datentopf UG, Kumo Robotics K.K.; none of these are real companies.

Make it yours: every select field's colors and emoji are just a starting point, so restyle, rename, or extend the options however fits the way you run your own search. The base only cares which field a value lives in — not what it's called or what color it wears.

## Tables

- **Companies**: the curated warm-outreach target list: an agenda of companies worth approaching, not companies already applied to.
- **Applications**: every job application actually submitted, whether or not the company is also a Companies target. 
- **Interviews**: interview rounds tied to a specific Application.
  Outcome is tracked separately from the Application's own Status, since an interview can advance while the application is still "Interviewing".
- **CV Versions**: every CV/resume variant in circulation: template, language, target role category.
- **Outreach**: cold mail / follow-up drafts. Every outbound message stops at Status = Proposed until a human reviews and sends it.
- **Reviews**: bi-weekly funnel stats (response rate, interview rate) summarising Applications/Interviews for a given period.

## How they connect

**Applications** is the hub: it links out to **Companies** (only when the applied-to company is also a curated target) and to **CV Versions** (which resume variant was used).
**Interviews** links back to the **Applications** record it belongs to.
**Outreach** links to **Companies**. **Reviews** aggregates data from Applications/Interviews but isn't itself linked - it's a periodic snapshot, not a live roll-up.

Applications also keeps Company name and CV version used as free text alongside the linked fields, deliberately; that's what the table looked like before the linked-record migration, left in place as a worked example of the "free text → linked records" pattern this base demonstrates end to end.