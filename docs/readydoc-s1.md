# ReadyDoc — Form S-1 (framework only; not an offering)

This follows the structure of a registration statement because that structure forces the honest
questions: what is the business, what does it own, what has it proved, and what would break it.
It is written for a licensing or acquisition conversation, not for a regulator.

Prepared 2026-09-13. All operating figures are counted from the codebase and the production
deployment, not estimated.

---

## 1. Summary

**ReadyDoc is the execution layer for food-safety and quality compliance in a manufacturing plant.**

A document system tells you what the plant is *supposed* to do. ReadyDoc is the system that makes it
happen and produces the record afterwards: it raises the task on the right day, puts it on the right
person's phone in their language, refuses the completion if the evidence is missing, files the numbered
controlled-form record the auditor will ask for, and escalates to a named person when a limit is
breached.

The company it runs is Powder Ops, a dietary-supplement contract manufacturer. It went live on
**1 July 2026**. Eight weeks later an NSF audit covering both GMP for Sport and NSF/ANSI 455-2 returned
**twelve minor nonconformances, zero major, zero critical, zero Not Acceptable.** Twelve corrective-action responses
were drafted from the platform's own records.

**The one-sentence thesis:** the recurring, expensive defect in plant compliance is *a fact that exists
in more than one place*. ReadyDoc's whole architecture is the opposite discipline — one fact, one owner,
everything else derived on read.

---

## 2. The business

### 2.1 What it replaces

Before ReadyDoc, the plant ran on: paper forms in binders, Monday.com boards, Google Sheets, a Slack
workspace, LobbyTrack for visitors, MRPEasy for production, QuickBooks for money, and one person's
memory for everything in between. Each of those held a copy of a fact, and the copies disagreed.

Concrete, measured examples the platform found and closed:

- QA inspections (light, brittle plastic & glass, temperature & humidity) had been **performed and
  never recorded** — the completion wrote readings onto a work order and filed nothing. Two to three
  months of records were missing across three controlled forms. Recovered from the completion history.
- The 72-hour re-clean rule was **reading the wrong table**.
- A Monday receiving export of 2,107 rows contained **1,328 lines sharing 511 inspection numbers** —
  a numbering scheme no spreadsheet could enforce.
- Two of three real packaging purchase orders **overstated by $24,850** because a removed line stayed
  in the total.
- Ten supplier certificates on file **had already expired** and nothing knew.
- Ten flavours carried two different codes, and **four codes meant two flavours each**.

### 2.2 Current scope

Ten module groups, 79 navigable modules: Floor · Production · Warehouse · Maintenance · Product ·
Quality · Sanitation · Document Control · Office · System. The regulatory surface covered is 21 CFR 111,
21 CFR 117, SQF (Dietary Supplement edition), NSF/ANSI 455-2, NSF GMP for Sport, 29 CFR 1910.147 and
.178, 8 CFR 274a, and GS1 GTIN allocation.

The full function list and release timeline is `docs/readydoc-release-history.md`.

---

## 3. The product's differentiating mechanisms

These are the things a document repository cannot do, and they are what would be bought.

**A controlled change is parked, not deployed.** A change to a form definition or an acceptance
criterion ships in the code but does **not take effect** — the application keeps serving the last
snapshot Document Control approved, raises a Document Change Request, and messages Document Control.
Approving promotes it immediately, no restart. This is Part 11 change control implemented as a runtime
mechanism rather than a policy document.

**Acceptance criteria are transcribed, never typed.** The ATP critical limit of 35 RLU, the five scale
forms' tolerances, the 104 internal-audit questions, the 41 supplier-questionnaire questions, the mock
recall's 99.5–100.5% mass balance — all are verbatim from the plant's approved documents, in source,
gated. A critical limit editable in a text box is the audit finding the architecture refuses to create.

**An acceptance criterion travels with the record it graded.** A cleaning record graded under 35 RLU
goes on saying 35 after the number moves. A barcode image remembers which GTIN it encodes. A sensory
result carries the specification it was judged against, and says whether that specification was approved
at the time.

**A check declares what its completion must carry, and one interface files it.** Completing a scheduled
task files the numbered controlled-form record inside the same transaction. A completion missing its
evidence is refused by the server, not just discouraged by the screen.

**Derived on read, never stored.** Readiness, coverage, gaps, ageing, overdue, on-hand stock, the
supplier register's counts, the reconciliation total — every figure is recomputed from the records it
summarises, so a badge can never disagree with the queue it opens.

**An electronic signature asks for a second factor at the moment of signing.** 21 CFR 11.200: the
signer's own password, checked before anything is written, rate-limited, never stored or logged, with
`signature_verified` in the audit entry. Four signing doors, one definition.

**Nothing is deleted.** Retired, withdrawn, superseded, waived — each with a name, a time and a reason.
A back-dated entry carries both dates and why they differ.

**It reaches the person.** A rule nobody can see is a rule nobody follows. Escalations DM and push to a
named person; a re-clean raises its own work order rather than waiting for a supervisor to notice a
badge; nudges chase what nobody has fixed and go quiet by themselves.

---

## 4. Market and positioning

### 4.1 The gap

Food-safety software divides into three: **document repositories** (MasterControl, Qualio, Greenlight
Guru, and Keychain OS's food-safety module), **ERP/MES** (Keychain, MRPEasy, Datacor), and
**point tools** (environmental monitoring, supplier portals, label proofing).

Nobody owns the middle. The repository knows the SOP exists; the ERP knows the batch ran; **neither
produces the numbered record proving the SOP was followed on that batch.** That record is what an
auditor asks for, and in most plants it is still paper in a binder.

### 4.2 The Keychain thesis

Keychain has two assets: a partner network connecting brands, manufacturers and suppliers, and
Keychain OS. Its food-safety module is, functionally, a controlled-document repository.

The complementarity is structural, not incidental:

| Keychain has | ReadyDoc has |
|---|---|
| The approved document | The record that proves it was followed |
| The master manufacturing record and batch record | Every check around the batch: sanitation, ATP grading, scale verification, inspection, retention, stability, release gate |
| Supplier relationships across a network | Supplier *qualification* — SOP-driven disposition, questionnaire on a signed link, certificate expiry, annual review that raises its own work order |
| The plan | The floor: phone-first, bilingual, offline-tolerant, kiosk-addressable |

This plant is already migrating to Keychain and has explicitly decided the master manufacturing record
belongs there, not in ReadyDoc (decision D-059). The boundary has therefore already been drawn in
production, by a customer, rather than proposed in a deck.

**The strategic argument:** a document module makes Keychain OS defensible against a spreadsheet.
An execution layer makes it defensible against an auditor — and an audit finding is the event that
actually causes a plant to buy software.

### 4.3 Buyer

The plants that need this are 20–200 people, audited annually against SQF/BRC/NSF, running paper and
spreadsheets, with one or two people holding the whole quality system in their heads. Powder Ops is
exactly that profile.

---

## 5. Technology

Node.js / Express / better-sqlite3 on the server; React and Tailwind on the client; deployed on
Railway from `main`; Cloudflare R2 for files.

| | |
|---|---|
| Database tables | 188 |
| HTTP route handlers | 939 (74 routers) |
| React components | 170 |
| Application code | ~143,000 lines |
| Automated suites | 76 — 31 pure-logic, 45 executed against a live server on a fresh database, several driving a real browser |
| Decision records | 82, append-only, each with the reasoning |

**Verification is a mechanism, not a promise.** `npm run verify` is the whole of CI in one command and
a pre-push git hook refuses a push that fails it. `verify:prodcopy` boots the current code against a
copy of the production database twice — the second is the redeploy case — and asserts no table lost a
row, no compliance log gained one, and the release's own migrations landed. Several suites carry a
**control run**: the fix is deliberately reverted and the test is required to fail, so a guard nobody has
seen fire is not trusted.

**Every integration degrades gracefully.** Missing credentials hide a feature; they never break the app.
That property is what makes a per-customer deployment configurable rather than a fork.

**Documentation is unusual and is part of the asset.** ~10,000 lines: a 2,700-line engineering memory
recording every trap and why each rule exists, an append-only decision register, and per-module runbooks.
An acquirer is buying a codebase that explains itself.

---

## 6. Operating history

| | |
|---|---|
| Production go-live | 2026-07-01 (`GO_LIVE_DATE` in the schema) |
| Production deployments | 1 (Powder Ops) |
| People on the system | ~35 on payroll; the whole plant, including the floor |
| Development window in this repository | 2026-08-17 → 2026-09-11, 251 releases |
| Releases per working day, that window | 1–34 |
| Regulatory audits passed on the system | 2 (NSF GMP for Sport, NSF/ANSI 455-2), August 2026 |
| Major or critical findings | 0 |
| Findings naming the software | 1 (4.4.39 — the *validation package*, not the controls, which the auditor credited) |

Revenue: none. ReadyDoc has never been sold, licensed, or offered to a second party.

---

## 7. Paths to monetisation

1. **Licence to a platform (the Keychain case).** Sell the execution layer as a module, or licence the
   source. Highest value, fewest customers to serve, and the acquirer already owns distribution.
2. **Per-plant licence, single-tenant.** One instance per plant, priced against the QA headcount it
   replaces or the audit finding it prevents. Deployable today; the configuration work is real (§8.1).
3. **Multi-tenant SaaS.** Highest ceiling, and the furthest away — it is a re-platforming project, not
   a packaging exercise.
4. **Sell the company/asset outright.** Cleanest exit; requires §8.4 resolved first.

---

## 8. Risk factors

Stated plainly, because a buyer will find them anyway and finding them first is worth more than
presenting well.

### 8.1 It is single-tenant by construction, and seeded with one plant's reality

There is no tenant concept anywhere in the codebase — one SQLite file is one plant. Twenty-four seed
files carry Powder Ops' actual rooms, forms, org chart, 118 SKUs, scale tolerances, preventive controls
and supplier list. **A second customer is a configuration project, not a signup.** Concretely: the
form register, room vocabulary, preventive controls, scale forms, org chart and checklists are all
plant-specific and must be re-transcribed from the second plant's own approved documents — which is
also, correctly, the only way they *should* be populated.

Estimate this honestly in any conversation: first additional plant is weeks of transcription plus a
tenanting decision, not days.

### 8.2 No validation package exists

NSF finding 4.4.39 names this. The *controls* were credited by the auditor — she had read the executed
Authentication and Access Control Verification before writing the finding. What does not exist is the
package: scope, a 21 CFR Part 11 gap assessment, protocols approved by Quality *as validation*, and
documented software change control. For a buyer selling into regulated plants, producing that package is
a required, funded work item — and answering it with more test scripts is the wrong answer.

### 8.3 Key-person concentration

The platform was specified, built and is maintained by one person working with an AI assistant. The
engineering memory and the decision register materially reduce this risk — the reasoning is written
down, not held — but they do not eliminate it. A buyer inherits a system no second engineer has yet
onboarded onto.

### 8.4 Ownership and IP are not formally established

There is no separate entity, no IP assignment, no trademark, and the work was produced inside an
operating company. Before any sale or licence, ownership has to be established on paper. This is
lawyer work, and it is the first item, not the last.

### 8.5 Concentration and unproven generality

One customer, one plant, one product category (dietary supplements). Every rule in the system is correct
for this plant; some of them are *specific* to this plant and neither the code nor these notes always
distinguish the two. A second deployment is the only way to find out which.

### 8.6 Architectural limits

better-sqlite3 with a single-instance in-memory socket adapter caps horizontal scaling. It is the right
choice for one plant and the wrong one for a hundred tenants on shared infrastructure. Migration is
tractable — the data layer is centralised — but it is a project.

### 8.7 Dependency on a single AI provider

AI features (Ask, semantic search, translation, policy drafting) depend on Anthropic and Voyage. All
degrade gracefully, so the core compliance system is unaffected — but the differentiated features are
priced and provisioned by third parties.

### 8.8 Regulatory change

The controls encode a specific reading of specific standards at a specific revision. Standards move. The
`controlled.js` mechanism is the mitigation — it parks a change until a person approves it — but keeping
the transcriptions current is ongoing work, not a one-time build.

---

## 9. What a buyer would need to fund

1. Ownership and IP established on paper (§8.4). **First.**
2. The validation package (§8.2) — the item that converts a working system into a sellable regulated one.
3. A tenanting decision and a second deployment (§8.1, §8.5) — the only real proof of generality.
4. A second engineer onboarded against the existing documentation (§8.3).

---

## 10. Closing statement

ReadyDoc is not a prototype and it is not a product. It is a **working, audited, production compliance
system with one customer** — live since 1 July 2026, two regulatory audits passed eight weeks later with
no major findings, 188 tables, 76 automated test suites, and a written record of why every rule in it
exists.

What it lacks is everything that follows from having been built for one plant: a second customer, a
validation package, a legal wrapper, and a tenant model.

For an acquirer who already has distribution into food manufacturing — Keychain being the clearest
example — those four gaps are exactly the ones their existing business is set up to close, and the
thing they would be buying is the one part that is genuinely hard: the accumulated learning of what
actually breaks on a plant floor, written down as it was found.
