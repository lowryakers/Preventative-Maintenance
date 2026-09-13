# ReadyDoc — release history and function inventory

Context document. Every date below is either a git commit date from this repository or a
date recorded in the project's own working notes. Nothing here is estimated.

**Dating provenance.** This repository's git history begins **2026-08-17** and runs to
**2026-09-11** (251 commits). Part 2 dates are exact commit dates. Part 1 covers modules that
were already in production before that history begins; those carry a date only where the
working notes record one, and are otherwise marked `pre-2026-08-17`. Part 3 is the inventory
as it stands today, counted from the code.

Production go-live: **2026-07-01** (`GO_LIVE_DATE` in the schema). Deployment: single production
instance, Railway, deploying from `main`. One to thirty-four releases per working day over the dated
period. Modules in Part 1 were therefore built before go-live or in the first six weeks after it.

---

## Part 1 — Shipped before 2026-08-17

| Function | Date | Note |
|---|---|---|
| Core QMS record spine (deviations, non-conformance, on-hold, disposals) | pre-2026-08-17 | One config file drives form, log, record view, auditor view and CSV import |
| Controlled document registry (SOPs, work instructions, job descriptions) | pre-2026-08-17 | Revisions, approvals, review dates, withdrawal |
| Document Change Requests (DCR) | pre-2026-08-17 | |
| Task Center + recurring PM schedules + work orders | pre-2026-08-17 | |
| Operator View (phone-first task screen, EN/ES) | pre-2026-08-17 | |
| Equipment register + maintenance task lists | pre-2026-08-17 | |
| Calibration management + instruments | pre-2026-08-17 | |
| Lockout/Tagout procedures and executions | pre-2026-08-17 | |
| Sanitation / cleaning records | pre-2026-08-17 | |
| QA Inspections (light, brittle plastic & glass, temp/humidity) | pre-2026-08-17 | |
| Chemical register + SDS | pre-2026-08-17 | |
| COA / lab testing: requests, specifications, auto pass/fail, facility COA PDF | pre-2026-08-17 | |
| Production Log, per-team EOD templates, multi-MO entries, "My Day" running log | pre-2026-08-17 | |
| Production Schedule (grid, publish-to-channel, bulk move) | pre-2026-08-17 | |
| Production KPIs | pre-2026-08-17 | |
| Receiving Log + FORM 204-01 receiving inspection checklist | pre-2026-08-17 | |
| Sign In/Out — knives (440-02), equipment/tools/chemicals (703-01), component pulls | pre-2026-08-17 | |
| Scale Verification (FORM 417-01…05) + public kiosk | pre-2026-08-17 | |
| Kiosks: component, knife, maintenance, scale | pre-2026-08-17 | Public, QR-addressed |
| Training records + courses + quizzes; Training Log matrix importer; scanned-test importer | pre-2026-08-17 | |
| Certifications | pre-2026-08-17 | |
| CAPA / complaints register | pre-2026-08-17 | |
| Mock Recall (FORM 415-1, SOP 415 V3) | pre-2026-08-17 | |
| Internal Audits (FORM 403-01, 104 questions) | pre-2026-08-17 | |
| Meetings / management review minutes | pre-2026-08-17 | |
| Safety: crisis contacts, evacuation drills, first aid, injuries | pre-2026-08-17 | |
| Hygienic design verification | pre-2026-08-17 | |
| Auditor View (self-service binder) + process maps | pre-2026-08-17 | |
| Audit log (immutable, actor/role/department, diff view) | pre-2026-08-17 | |
| QA Review Center (one queue, seven signature sources) | pre-2026-08-17 | |
| Document Control Review Center | pre-2026-08-17 | |
| Controlled Changes (`controlled.js`) — a deployed form definition is parked until Document Control approves it | pre-2026-08-17 | The mechanism behind the whole platform's change control |
| Log Builder / managed lists / custom fields (self-serve structure engine) | pre-2026-08-17 | |
| Universal file importer (CSV/TSV/XLSX; Monday, Airtable, Drive, QuickBooks exports) | pre-2026-08-17 | analyze → preview → commit → provenance |
| Comms Phase 1 — channels, DMs, threads, reactions, membership access layer | pre-2026-08-17 | |
| Comms Phase 2 — realtime via socket.io | pre-2026-08-17 | |
| Comms Phase 3 — R2 file uploads + FTS5 keyword search | pre-2026-08-17 | |
| Comms Phase 4 — Voyage embeddings, semantic search, membership-scoped RAG "Ask" | pre-2026-08-17 | |
| Comms Phase 5 — EN/ES translate, @mentions, installable PWA, web push | pre-2026-08-17 | |
| Web push diagnostics + VAPID key-rotation repair | 2026-07 | |
| Slack history importer | pre-2026-08-17 | |
| Team Activity / efficiency dashboard (admin-only) with full drill-down | 2026-07-22 | User-approved ship date |
| Comms → compliance-record crossover ("create compliance record from a message") | 2026-07-23 | |
| Chat message → Task Center task (intent detection, EN/ES) | pre-2026-08-17 | |
| Offline mode — read cache + write outbox, approvals never queued | pre-2026-08-17 | |
| Password auth replacing PIN; usernames; password expiry policy | pre-2026-08-17 | |
| Module access map (per-user, per-module view/edit grants) | pre-2026-08-17 | |
| Step-ticking required to complete food-contact work | 2026-08-12 | Plant decision |
| NULL module map = empty account (Messages only) | 2026-08-13 | Plant decision |
| Office: supply orders, requests, time tracking, newsletter, pay tracking, org chart | pre-2026-08-17 | |
| Accounting: AP ledger, AR ledger, Partner Reconciliation, Banking, QuickBooks read-only sync | pre-2026-08-17 | Ledger/Banking/QBO tabs later hidden — see 2026-09-11 |
| Flavor approvals by SMS (Twilio magic link) | pre-2026-08-17 | |
| Danny's List (request log for the owner, who works by text) | 2026-08-21 | See Part 2 |
| Procurement & demand / purchase orders | pre-2026-08-17 | |
| Pre-launch cleanup (bulk close-out, waive-never-sign) | pre-2026-08-17 | |
| ReadyDoc feedback "Request" button | removed 2026-08 | Removed at user request |

---

## Part 2 — Dated releases, 2026-08-17 → 2026-09-11

### August 2026

**08-17** Film inspection pick-one display fix · Procurement PO columns, quarter/urgent editable, mass update

**08-18** COA Specifications: 22 FORM 607-01 raw-material sheets seeded as drafts · Partner ledger line
summaries + amount cross-check · Partner reconciliation reminders + sanitation correction path · Comms
back-button history · Last-stop JSON error handler · Partner portal migration repair · Searchable
dropdowns on every sign-out form · Org chart: several job descriptions per position

**08-19** Org chart tree compaction · COA scan reads every test, stops inventing values · COA log true
count · Chemicals unreachable in sign-out picker (+4 silent-loss fixes) · Room numeration per FORM
431-01 V5 · Attachment upload repair + duplicate-task engine · **A task names the controlled form it
satisfies** (`shared/form-registry.js`) · **Completing a QA inspection files its record** ·
**QA-record backfill** from historical completions · PDF viewer double-pane fix · Cleaning logs had the
same gap; backfill pile announces itself

**08-20** Six scales de-duplicated; form numbers on sign-out logs · **Form register maintained in the
app** (`controlled_forms`) · Work-order filter fix · **The app explains its own rules** (`platformRules`)
+ Master Index transcribed · Twilio: pick the recipient at send time; texting-in as a per-user grant ·
SMS consent recorded; A2P disclosures; opt-out on every message · Settings names the texted-link domain ·
Weekly task no longer hands over the annual checklist

**08-21** **D-001 recorded — do not rebuild** · Write a controlled document without typing Markdown ·
Threads-inbox replies carry attachments · **Danny's List** (steps 1–4, opt-in module gating, real delete)
· Flavour decided by text = same record as decided in app · ReadyBot attribution on flavour announcements
· Split-screen lands on the channel list

**08-24** **Auditor pass** (read-only session instead of a shared password) · Four evacuation drills
filed · Controlled documents/DCRs hidden by default in the binder · Job Descriptions in the binder ·
**V2 architecture + decision record move into the repository** · 33 fire-drill signatures as training
records · Bulk task completion now files records · **Visitor sign-in** — schema, NDA as a frozen
revision, API, lobby tablet, signature pad (replaces LobbyTrack) · Backfill strip reaches the right
people · Sanitation per-area history + search · Recurring Schedules screen · 72-hour re-clean rule was
reading the wrong table · First password requires an invitation · Authentication & Access Control
Verification report filed · **D-002…D-022 recorded — the preventive-control walk**

**08-25** Daily PM carries daily tasks only · **Message deletion is admin-only** (`shared/comms-permissions.js`)
· **People / candidate tracker** + seven real rows seeded · **Four preventive controls transcribed**
(`server/preventive-controls.js`) · ATP limit proven end to end · D-010…D-012, D-023 recorded

**08-26** Lobby-tablet reachability validated; name removed from a public path · **Kiosk isolation
report** · **QR posters carry their own key** (`server/kiosk-tokens.js`, off→warn→on rollout) ·
**Uploaded files require a session** (`FILE_COOKIE`) · Auditor pass announces itself · **One work
instruction, many machines** (`sop_documents.equipment_ids`) · **COA lab submission composed, not
scanned** (`server/coa-submission.js`) + signed submission PDF · **Drillable banner numbers**
(`server/attention-sources.js`) · **Comms search scoped to the caller's channels before the cap** ·
**Flash Report** (exceptions / scorecard / output) · Each kiosk installs as itself · Red-line both
plans; hub-and-spoke document graph designed (D-024…D-027)

**08-27** Settlement folds the credit into the side it reduces · **`npm run verify` + `.githooks/pre-push`
— a red build becomes impossible** · **August 2026 NSF audit findings recorded** · Threads refresh no
longer resets the screen; @mention caret · **ATP swabs graded against PC #1's 35 RLU; two failures raise
the re-clean** (`server/atp-limits.js`) · Sign In/Out dropdown scrolling · **Supplier Qualification
register** (NC 4.3.1) — SOP 404 transcribed, 836-file archive parsed, tracker/archive reconciliation ·
**Obligations register + `npm run check:obligations`** · SQF pass: 22 findings by clause (D-028…D-043)

**08-28** **Annual vendor review raises its own work order** (`server/supplier-review.js`)

**08-31** **End-of-week clean level** (`shared/clean-levels.js`) · **Lab tests on receipt**
(`server/lab-test-items.js`) · **`gsmSafe` — an em-dash cost three SMS segments** · Completing a 72-hour
re-clean files its cleaning record · **QA scores the tasting, the approver decides** · **Flavour code
register** (`flavor_codes`, append-only) · **Preferred-SKU preview column + bottle-line drafts** · Line
codes for all ten product lines; three collisions broken · Every flavour has a code; all 118 SKUs resolve
· Supplier documents stored as bytes · **NFP panel file attach on filing** · **GS1 barcode image +
`barcode_gtin` staleness** · Draft realign to the register · **Supply Orders: partial receipt by
quantity + totals read off the invoice** (`server/invoice-figures.js`) · Re-clean tasks name their reason
(`shared/reclean-reasons.js`)

### September 2026

**09-01** Work the 43 NCs as a queue with evidence in one window · **`check:ncstatus`** — the status page
cannot claim work the code lacks · Draft realign offered where the disagreement is visible ·
**Product readiness: three states (todo/done/stale), dependency graph, first-sight rule**
(`shared/product-readiness.js`) · Comms caret drift, who-reacted, `[label](url)` links ·
**Equipment readiness staleness** · **GTIN barcode board + product document registry**

**09-02** **A QA signature proves it is you, at the moment you sign** (`server/signature.js`, 21 CFR
11.200) · Reaction tooltip flicker · **Swab stock tracker** (`server/swab-stock.js`) ·
**Track B folded into `main` — one track (D-045)** · Twelve findings checked against code, not the
register · Document Control worklist · NULL module map corrected · A repeated reading is questioned, not
refused (D-046) · **A completion advances the schedule from the day the work was done (D-047)** ·
**New-hire onboarding folded onto `main` (D-048)** · Artwork proofer dependency written down

**09-03** **Pre-spine review — 40+ defect classes found and closed in one pass** (reviews 01–12, B2–B7,
C2–C9, D2–D9, E4, G3–G13): the task door grades ATP, one signer, one completion door, an empty scale form
is not a pass, mirrors written around their owner, ten test assertions that passed with the feature
broken · **Photo viewer** (pinch/zoom/copy-as-image) · **FORM 602-01 V2 — organoleptic test as pass/fail
against a per-product specification** (`shared/sensory.js`, D-049/D-050) · **Artwork-Proofing sync**:
fill weight, ingest snapshot, snapshot endpoint · **`verify:all`** · **`verify:prodcopy` — boot the
current code against a copy of the production database** · **People: tags + résumé files** ·
**Shipping Truck Inspection, stamped DRAFT-1 until Document Control issues it (D-052)** ·
**Integrations screen** · **Onboarding: W-4 and I-9 completed and signed on the link (D-053)**

**09-04** Six laptop-facing logs render as cards on a phone · **`PhotoPicker` — take one or choose one**
· Reimbursement claim with a photo was refused

**09-05** **Four preventive controls seeded and guarded at boot (OBL-02, D-054)** · **A paused schedule
reports the work it left behind (D-055)**

**09-08** **Official NSF reports recorded; CAR deadlines 18 Sep and 4 Oct (D-056)** · **All twelve CAR
responses drafted** in NSF's six-part format from one data file

**09-09** CAR names and titles from the org chart, plain English · **Pay-review actions stay listed until
acted on (D-057)** · **FORM 404-1 supplier questionnaire completed and signed on a link (D-058)** ·
**A scheduled check declares what it files, and one interface files it (D-060)** — EMP sampling, GMP
walk-through, banned-list review · **Stability studies and pulls (D-061)** · **Change register — every
kind of change 21 CFR 111.130(e) names, Quality signs twice (D-062)** · **COA specification release gate
in warn mode (D-063)** · **IQ/OQ/PQ on the equipment checklist; FORM 204-01 V2 deploys parked (D-064)**

**09-10** **ADP: API Central + Applicant Onboard V2** (D-065…D-071) — payload rebuilt from RUN's guide,
integration route established as Workforce Now, priced, and **parked** · Onboarding EN/ES + install
hand-off · **Pay Tracking: onboarding seeds the roster, 30/90-day reviews, contractors** · Time Tracking
attendance follows the account · **1099 contractor path through onboarding** · **Revoking access reaches
the sessions it already opened (D-072)** · **AP Drop — one intake for every finance PDF (D-073)** ·
**Four name-keyed tables get an account id (D-074)**

**09-11** AP Drop photo intake + Accounting review pack · Settings roster access summary ·
**Accounting: ledger/Banking/QuickBooks tabs hidden; AP Drop routes partner documents itself (D-075)** ·
**Onboarding reveal — the masked SSN and bank numbers, once, for ADP entry (D-076)** · W-2 / 1099 chosen
on the Start form · Legal-name directions; office told when a packet finishes ·
**Employee documents — send a W-4 or a policy to somebody who already works here, signed in the app
(D-077)** · **Five reports from the floor (D-079)** · **Private client channel for M4 Dynamic (D-080)** ·
**The SKU rename carried one of its four child tables (D-081)** · **Amazon as the fourth external
system; `applies` on the readiness model (D-082)**

---

## Part 3 — Inventory as of 2026-09-11

Counted from the repository, not recalled.

| | |
|---|---|
| Database tables | 188 |
| HTTP route handlers | 939 |
| API routers | 74 |
| React components | 170 |
| Application code | ~143,000 lines (66,800 server · 74,200 client · 2,300 shared) |
| Automated test scripts | ~13,000 lines |
| Documentation in repo | ~10,000 lines |
| Automated suites | 76 (31 `check:` pure-logic · 45 `verify:` against a live server on a fresh database, several driving a real browser) |
| Navigable modules / tabs | 79 |
| Decision records | 82 (`docs/v2/decisions.md`, append-only) |

**Module groups:** Floor · Production · Warehouse · Maintenance · Product · Quality · Sanitation ·
Document Control · Office · System.

**Integrations:** Cloudflare R2 (files) · Anthropic (AI assistance) · Voyage AI (embeddings) ·
Twilio (SMS) · Web Push / VAPID · Plaid (built, dormant) · QuickBooks Online (built, hidden) ·
ADP API Central / Workforce Now (built, parked) · Artwork-Proofing service (live, two-way) ·
Slack (import only).

**Every one degrades gracefully:** the absence of a credential hides a feature; it never breaks the app.

---

## Part 4 — Regulatory scope covered

21 CFR 111 (dietary supplement cGMP) · 21 CFR 117 (preventive controls) · 21 CFR Part 11
(electronic records and signatures — signature component implemented, validation package not yet
produced) · SQF Food Safety Code, Dietary Supplement edition · NSF/ANSI 455-2 · NSF GMP for Sport ·
29 CFR 1910.147 (LOTO) · 29 CFR 1910.178 (powered industrial trucks) · 8 CFR 274a (I-9) ·
GS1 GTIN allocation and check digits.

**Audit result, 24–26 August 2026** (NSF, auditor Sonya Hess, one visit, two audits):
GMP for Sport 3 minor · NSF/ANSI 455-2 9 minor · **0 major, 0 critical, 0 Not Acceptable.**
Twelve CARs; all twelve responses drafted; deadlines 18 September and 4 October 2026.
