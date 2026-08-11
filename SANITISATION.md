# SANITISATION — gate before any public JobOps publish

Checklist from SPEC.md §6. Run before every publish of the `jobops`
public repo or its seed Airtable base — not just the first time.

No screenshots are part of the public artefact set (D-26): the repo's
README documents the system in prose plus a text/mermaid architecture
diagram, not UI screenshots of either Airtable base. This removes the
"retaken against the seed base" screenshot risk entirely rather than
managing it.

- [ ] `grep` every export (workflow JSON, seed CSVs, README) for: real
      company names from the Agenda, all personal emails
      (elesyng@proton.me, plus the retired yahoo/gmail addresses),
      phone number, salary figures, contact-person names. Phone number
      is N/A for `jobops` specifically — no phone number is collected,
      stored, or referenced anywhere in this system's schema, workflows,
      or seed data (confirmed 2026-08-11). Still check the rest.
- [ ] No Airtable base ID, table ID, or record ID appears in exported
      n8n workflow JSON — all live in the `jobops_template_config` Data
      Table instead (D-24).
- [ ] No credentials blocks in exports (n8n strips them on export —
      verify anyway, don't trust it blindly).
- [ ] Notes fields are empty or fictional in every published artefact
      (seed CSVs, and any example values quoted in the README).

## Two-pass procedure (D-26)

**Pass #1 — immediately after drafting the full artefact set.**
Run all four checklist items above against every file that will ship:
each `workflows/*.json`, every `seed/*.csv`, and the full README text.
Use `grep -ri` for the fixed strings (names, emails, phone, salary
figures) plus a manual skim of README prose and any workflow sticky
notes, since free text won't be caught by a fixed-string grep. Fix
anything found before moving to pass #2. Log below: date, what was
checked (file list), what (if anything) was found and fixed.

**Pass #2 — 24h+ after pass #1, fresh eyes, full re-read.**
Not a re-run of the same grep commands — re-read every artefact
top-to-bottom as if seeing it for the first time. This is what catches
what pass #1's keyword search structurally can't: prose that implies
something sensitive without naming it, a sticky note added to a
workflow after pass #1, a CSV cell edited during README-writing. Confirm
explicitly that nothing was added to the artefact set between pass #1
and pass #2 without being checked. Log below: date, elapsed time since
pass #1, confirmation of the no-unchecked-additions check, and outcome.
Only after pass #2 logs clean does the repo go public for the first
time.

## Pass log
- 2026-08-12: Pass #2 (D-26 procedure), full re-read, 24h+ after pass #1
  (2026-08-11). Confirmed first that nothing in the artefact set changed
  unchecked in the interim: every file under
  `~/Documents/public-repos/jobops/` still carried its 2026-08-11
  timestamp, with one exception — the repo's own `SANITISATION.md` copy
  was found stale (missing the pass #1 log entry and the phone-number
  N/A resolution, both of which had only been written to this project's
  `docs/SANITISATION.md`) and was re-synced from the up-to-date copy
  before the re-read began, so that file was current going into the
  pass. Method: re-read every artefact top-to-bottom rather than
  re-running pass #1's grep — all 9 `workflows/*.json` in full, all 6
  `seed/*.csv` in full, `seed/BASE_GUIDE.md`, `README.md` (already fully
  in context from its unchanged 2026-08-11 state, re-scanned for
  anything a keyword search could miss), `LICENSE`, and this file.
  Result: clean, no new findings. Nothing in README prose, workflow
  sticky notes, or CSV free text implies real data without naming it.
  The Berlin/Hamburg/Osaka location values throughout are the fictional
  seed data's own dropdown options, not tied to any real address. No
  fixes needed. Two passes now complete and both logged clean — per
  SPEC.md §6 item 5 and the procedure above, the repo is cleared to go
  public for the first time (Task #7: create and push
  `elenamedea/jobops`, still gated on Elena's separate confirmation).
- 2026-08-11: Pass #1 (D-26 procedure) run against the full `jobops`
  artefact set in `~/Documents/public-repos/jobops/`: all 9
  `workflows/*.json`, all 6 `seed/*.csv`, `seed/BASE_GUIDE.md`,
  `README.md`, `LICENSE`, `SANITISATION.md`. Method: built a grep list
  of real company names, real contact-person names, and real salary
  figures pulled live from the private base's CompanyList - Agenda and
  ApplicationTracker tables (`appBXFboSMpn5OgOm`, not from memory), plus
  the personal email prefix `elesyng` and known domains
  (`proton.me`, `yahoo.gr`), then ran a case-insensitive fixed-string
  grep across the whole artefact tree. Separately grepped for Airtable
  ID patterns (`app`/`tbl`/`rec` + 14 chars) in the workflow JSON and
  for `"credentials"` blocks. Manually skimmed README.md end to end and
  the workflow sticky notes for anything the grep could not catch.
  Result: clean. The only hit was the expected, self-referential
  mention of `elesyng@proton.me` inside SANITISATION.md's own checklist
  text (this is the rule describing what to check for, not a leak — the
  same line existed in the pre-D-26 checklist). README.md's use of
  "Elena" (first name only, no surname) in the two-track section is
  expected self-attribution for a repo published under her own GitHub
  account, not a contact-person disclosure the checklist is scoped to
  catch, so it was left as-is. No fixes were needed.
  **Phone number sub-item: N/A for `jobops`**, confirmed by Elena
  2026-08-11. No phone number is collected, stored, or referenced
  anywhere in this system's schema, workflows, or seed data — the item
  applies to other artefacts in this project (CVs, cover letters), not
  to the JobOps tracker itself. Resolved, not a gap carried into pass #2.
- 2026-08-02: First pass run against `seed/*.csv` after rebuilding them
  for the public JobOps base (`appisb98Q3fuwE89f`, JobOps workspace).
  Grepped for real Agenda/Applications company names, personal emails,
  real contact names, Airtable IDs — clean. Second pass still due 24h+
  later, before the base or repo is ever shared — do not skip. (Predates
  D-26's two-pass procedure and no-screenshot scope; superseded by the
  Phase 4 passes run against the full artefact set once workflows/README
  exist.)

## Seed data source
`seed/*.csv` in this repo — matches SPEC.md §2's schema and §3's
fictional rows (GreenGrid Analytics GmbH, Datentopf UG, Kumo Robotics
K.K. — all `.example` domains, reserved by RFC 2606, never resolve to
a real site).
