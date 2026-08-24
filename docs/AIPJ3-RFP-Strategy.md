# AIPJ3 Website RFP — Bid Strategy

**RFP:** RFP/Website Development/018-08-2026 — AIPJ3 Website Development and Maintenance
**Issuer:** DT Global, on behalf of Australia Indonesia Partnership for Justice Phase 3 (DFAT-funded)
**Source of truth:** the RFP PDF itself (15pp, issued 12 Aug 2026). All facts below are cited to it.
**Analysis date:** 24 August 2026, 17:42 WIB

---

## 0. Correction to prior analysis

The earlier `AIPJ3_Full_Analysis_Checklist.md` marked the submission deadline as "🔴 likely passed."
That is incorrect.

| Milestone | Date | Status as of 24 Aug 2026 |
|---|---|---|
| RFP advertised | 12 Aug 2026 | done |
| Briefing session (online, **not mandatory**) | 20 Aug 2026, 10:00–11:00 WIB | **closed — missed** |
| Written questions deadline | 20 Aug 2026, 15:00 WIB | **closed — missed** |
| **Proposal submission** | **26 Aug 2026, 23:59 WIB** | **OPEN — ~54 hours remain** |
| Evaluation, due diligence, negotiation, signing | 27 Aug – 14 Sep 2026 | upcoming |
| Commencement | ~15 Sep 2026 | upcoming |

Consequence: missing the briefing costs nothing formal (attendance was optional). Missing the
questions window costs the ability to get a binding written clarification — which matters, because
the RFP contains at least three genuine ambiguities (§5). Those must now be handled as **stated
assumptions inside the proposal**, not as questions.

---

## 1. The actual gate is administrative, not the 8-year rule

Prior analysis treated "8+ years organisational experience" as the deal-breaker. It is not the
first one. Read the Proposal Requirements section (p.3):

> "If any of the above documentation is not complete, then the tender will be deemed noncompliant
> and AIPJ3 has the right to not accept the proposal."

That refers to Attachment 1, which requires:

1. Cover letter (org name, Corporate Taxpayer Number, address, contacts, responsible person)
2. **Deed of establishment + approval from Ministry of Law and Human Rights** (akta + SK Kemenkumham)
3. **Organisation Tax Identification Number (NPWP)**
4. **Organization's Domicile letter (Surat Izin Domisili)**
5. Due Diligence Preliminary Supplier Statement (DT Global template)
6. Signed Tenderer's Declaration (DT Global template)
7. VAT Exemption Commitment Letter — **only if registered as Pengusaha Kena Pajak (PKP)**

Items 2–4 are *documentary proof of corporate existence*. They cannot be drafted, argued, or
compensated for by a strong technical proposal. Without them the submission is discarded before
scoring begins.

**So the decision tree has one root node:**

> Does the bidding entity hold akta + SK Kemenkumham + NPWP + domicile evidence, in hand, by 26 Aug?

- **No** → that entity cannot bid. Not "scores poorly" — is not evaluated.
- **Yes** → proceed; the 8-year question becomes a scoring question, and scoring questions are winnable.

### How bad is the 8-year criterion, really?

It sits inside a 20%-weighted block ("Essential Organisational Experience (Capacity) and Capability"),
alongside legal registration, portfolio, and a dedicated PM. The RFP does **not** state it as a
pass/fail threshold — but the block is titled "Essential" and uses "must," and the Contract Award
clause says awards go to a tenderer that "meets the eligibility requirements." The honest reading
is: **ambiguous, panel-dependent, and likely to cost most or all of the 20%.**

Arithmetic if it is scored (not threshold): 50% + 30% = 80 points remain reachable. Score 90% of
those and you land at 72/100 with a zero on organisational experience. In a thin field (see §3)
that is not automatically a losing number. It is, however, a bet you should only take *after*
clearing the administrative gate — never instead of clearing it.

---

## 2. Where the bid is actually won: the 50% block

Approach and Methodologies carries **50% weight — more than organisational history and personnel
put together.** And the RFP explicitly opens the door on the stack (§3.2.2):

> "The following list is for reference only. Provider could identify other than the list with
> description of its advantages and disadvantages."

This is an invitation to demonstrate engineering judgement. Most bidders will paste the technology
table back verbatim as a compliance checklist. That scores "compliant," not "excellent."

The required stack maps almost exactly onto a modern Next.js practice:

| Layer | RFP requirement | Notes |
|---|---|---|
| Front-End | HTML5, CSS3, ES2024, TypeScript | direct match |
| Framework | React 19 / Next.js 15 **or** Vue 3 / Nuxt 3 **or as proposed** | Next.js 15 App Router |
| Styling | Tailwind CSS 4, CSS custom properties | design tokens as CSS vars |
| CMS | Headless (Contentful, Sanity) | see §5.2 — cost trap |
| Back-End | Node.js 22 LTS, REST or GraphQL | Next route handlers |
| Database | PostgreSQL / MySQL / serverless | Postgres |
| Hosting | AWS / Azure / Vercel / Cloudflare Pages | see §5.1 — conflicts with "local" |
| VCS | Git + CI/CD | GitHub Actions |
| Security | TLS 1.3, CSP, WAF, OWASP Top 10 | |
| Accessibility | WCAG 2.2 AA, ARIA landmarks | see §5.3 — the differentiator |
| Analytics | GA4 + Consent Mode v2, GTM | |
| Perf KPIs | LCP <2.5s, INP <200ms, CLS <0.1 | Lighthouse ≥90 all categories |

### Five differentiators available in this document

1. **Resolve the hosting contradiction out loud** (§5.1). Shows the document was read, not skimmed.
2. **Cost-engineer the CMS choice with an advantages/disadvantages table** (§5.2). The RFP asks for
   exactly this and it protects the budget.
3. **Budget real disabled-user testing sessions, named partner org** (§5.3). Ties directly to EOPO 3.
4. **Lead with the editor, not the framework.** The client's stated pain is weekly publishing by
   non-technical comms staff (Objective 4, Deliverable 4, maintenance clause). Open Part B with the
   editorial workflow and the 2-hour training, not with "we use Next.js."
5. **Reconcile the deliverable schedule** (§5.4) and present a workplan that is internally coherent.

### Bilingual approach

EN/ID as parallel structured content fields from day one, not a translation plugin. The RFP requires
the site "available in English, Bahasa Indonesia, and with accessibility features for people with
disabilities" (Background, p.11). Model locale as a first-class dimension of the content schema so
EOPO updates publish in both languages without drift.

---

## 3. The budget is a filter — and that is an advantage

**Ceiling: IDR 150,000,000** covering build + 12 months hosting + 12 months maintenance (~USD 9,200
at prevailing rates; exchange rate not independently verified here).

What that must cover: a 4-month build; five named senior personnel (PM 8yr, FE 5yr, BE 5yr, DevOps
5yr, QA 5yr); bilingual site; WCAG 2.2 AA with disabled-user testing; Lighthouse ≥90; 12 months
hosting; 12 months maintenance at 99.9% uptime SLA, 48-hour critical patch SLA, monthly backups,
weekly content uploads, monthly + six-monthly reporting, annual penetration-testing recommendation.

An established agency staffing five senior FTEs cannot deliver this at margin — a conventional
Jakarta agency quote for this scope lands roughly 2–3× the ceiling. **The field will therefore be
thin, and skewed toward bidders treating this as a relationship/portfolio play rather than a profit
centre.** That is structurally favourable to a small, senior, low-overhead team — *conditional on
clearing the administrative gate.*

### Indicative allocation within the ceiling

| Line | IDR | Share |
|---|---:|---:|
| Phase 1 — Design Concept (UX research, personas, IA, wireframes, brand direction) | 20,000,000 | 13% |
| Phase 2 — UI Design (Figma hi-fi, desktop/tablet/mobile, interactive prototype) | 16,000,000 | 11% |
| Phase 2 — Front-end build (Next.js 15, TS, Tailwind 4, bilingual, a11y) | 26,000,000 | 17% |
| Phase 2 — Back-end, CMS integration, RBAC, content models | 16,000,000 | 11% |
| Phase 2 — QA + accessibility audit incl. disabled-user sessions + perf | 12,000,000 | 8% |
| Phase 3 — Launch, DNS/SSL, GA4 + Search Console, training, handover docs | 6,000,000 | 4% |
| Hosting — 12 months (local, incl. CDN/WAF/backup) | 15,000,000 | 10% |
| Maintenance — 12 months @ 3,250,000/mo | 39,000,000 | 26% |
| **Total** | **150,000,000** | **100%** |

Two things this implies, and both should be stated openly in the proposal rather than hidden:

- The five key personnel are **fractional, not full-time.** State level of effort as a percentage
  per role. A panel reading a 150M budget alongside five claimed FTEs will assume either padding or
  naivety; an explicit LOE table reads as competence.
- **Quote net of VAT.** Under PMK 59/2024 the AIPJ3 program facilitates VAT exemption for
  grant-funded transactions. If the entity is PKP, sign the commitment letter and quote net. Quoting
  150,000,000 + 11% VAT breaches the ceiling and may be scored as non-compliant on price.

### Payment terms — propose them, don't wait

The RFP invites this ("The Prospective Bidder may propose its preferred payment terms"). Payment is
against seven accepted deliverables, the last running to Jan 2028 — meaning the bidder finances the
build and is paid on acceptance. For a young entity that is a genuine working-capital risk. Proposed
structure:

| Trigger | % |
|---|---:|
| D1 Design Concept signed off (15 Oct 2026) | 20% |
| D2 UI Mockups approved (30 Nov 2026) | 20% |
| D3 Developed Website, UAT passed (22 Jan 2027) | 25% |
| D4–D6 Training + audit + post-launch report accepted (Mar 2027) | 15% |
| Maintenance retainer, monthly in arrears (Feb 2027 – Jan 2028) | 20% |

---

## 4. Three strategic options

### Option A — Bid as ICW, standalone
**Viable only if** akta + SK Kemenkumham + NPWP + domicile are in hand before 26 Aug 23:59.
If registration is still "in process," this option does not exist. Even if documents exist, expect
to lose most of the 20% organisational block, and mitigate by presenting the KSP work honestly as
**key personnel experience** (Part C) rather than as organisational portfolio (Part A). That framing
is standard, accepted, and — critically — true.

### Option B — Bid through a registered partner as prime, ICW as named delivery team
Solves the administrative gate **and** the 8-year criterion in a single move. The partner's akta,
NPWP, domicile, and experience sheets carry Part A and the 20% block; ICW's people carry Part C and
do the delivery.

Structures, fastest first:
- **KSO (Kerja Sama Operasi)** — joint operation for this specific bid; project-scoped, no merger
- **ICW as subcontractor to the partner prime** — simplest to paper in 48 hours
- Equity/division arrangement — too slow for this deadline, right for the long term

Requirements to execute in 54 hours: an existing relationship (cold outreach will not close in
time), the partner's admin documents, two to three of their Annex 1 experience sheets with live
referees, a signed teaming or subcontract understanding, and their director's signature on the
Tenderer's Declaration.

### Option C — No-bid; convert the 54 hours into reusable capability
Not a failure state. The RFP itself shows evaluation runs 27 Aug – 14 Sep and DT Global issues this
family of RFPs regularly. The 15-page technical proposal for this stack is **~80% reusable** across
every donor-funded web RFP in this market. Building the template, the CV pack in the required
format, the experience-sheet format, and the compliance policy set now means the *next* one is a
one-day turnaround instead of a scramble.

### Recommendation

**Option B if a registered partner is already within reach today — otherwise Option C.**

Option A only if registration genuinely completed. Do not submit an incomplete Attachment 1 hoping
it slides: DT Global runs comprehensive due diligence with the preferred subcontractor before
signing, so a gap surfaces later anyway, and burns the relationship for future rounds.

**Run Option C's asset-building regardless of which path is chosen.** Under B it *is* the proposal
work. Under C it is the entire return on these 54 hours.

---

## 5. Ambiguities to convert into stated assumptions

The questions window closed on 20 Aug, so these can no longer be clarified. Address each explicitly
in the proposal as "our assumption — confirm at inception." Handling them visibly is itself a
scoring signal.

### 5.1 "Hosting provider (local)" vs the approved hosting list
The maintenance scope requires a **local** hosting provider (p.13). The 50% scoring table lists
**AWS / Azure / Vercel / Cloudflare Pages**. These pull in opposite directions.

Proposed resolution to state: primary workload in an Indonesia-resident region (e.g. AWS
`ap-southeast-3` Jakarta, or an Indonesian IDC provider) with Cloudflare at the edge for WAF/CDN —
satisfying both data-residency intent and the named-vendor list. Offer a fully domestic-provider
variant as an alternative at inception. Note that data residency also tends to matter to a GOI–DFAT
partnership program independently of this clause.

### 5.2 Named headless CMS vs the budget
Contentful and Sanity are named. Paid tiers on either consume a material share of a 150M ceiling
across 12 months, and the licence is a recurring cost that outlives the contract — a risk carried by
the *client*, not the bidder. §3.2.2's "advantages and disadvantages" clause is an explicit invitation
to propose alternatives. Present a comparison table (Sanity free tier vs Contentful vs self-hosted
Payload/Directus/Strapi) scored on: licence cost at year 2+, RBAC support, editorial UX for
non-technical staff, bilingual content modelling, and exit/portability. Recommend one, and show the
12-month and 36-month total cost of ownership.

### 5.3 "Accessibility audit including with people with disability"
The plain wording (p.12) calls for testing **with disabled people**, not merely automated WCAG
scanning. Most bidders will price axe/Lighthouse and move on. Budget genuine paid sessions with
disabled participants, name a partner disability organisation, and say so.

This is the single strongest differentiator in the document, because it connects the technical
proposal to **EOPO 3 — equal access to justice for women, children and persons with disabilities.**
A panel drawn from this program will recognise its own outcome framework. Very few bidders will make
that link.

### 5.4 Internal date inconsistencies
- Deliverable 3 "Developed Website" is dated **22 Jan 2026** — a typo for 2027 (the development
  stage runs 16 Oct 2026 – 22 Jan 2027).
- Deliverable 4 (CMS training) 22 Feb 2027 and Deliverables 5–6 (audit, post-launch report) 1 Mar
  2027 both fall **after** maintenance begins 29 Jan 2027.
- General Information gives the duration as ending 15 Jan 2028; the maintenance stage ends 28 Jan 2028.

Do not present these as corrections to the client. Present a workplan that is internally coherent,
with a one-line note that the schedule reflects the assumption that D3 is 22 Jan 2027 and that
D4–D6 are handled as launch-hardening within the first maintenance month.

---

## 6. Submission mechanics — non-negotiable

| Requirement | Value |
|---|---|
| To | `AIPJ.General@aipj.or.id` |
| Subject line | `Proposal_Website Development` (exact) |
| Deadline | 26 Aug 2026, 23:59 WIB — late submissions cannot be accepted |
| Max attachment size | 25 MB per attachment |
| Language | English |
| Font | minimum 12 point |
| Technical proposal length | max 15 A4 pages **excluding annexes** |
| Logos | AIPJ3/DFAT or other external logos must **not** be affixed |
| Hard copies | not required |
| Tender validity | 90 days from closing |
| Structure | Part A Company Profile → Part B Approach & Methodologies → Part C Key Personnel, **in that order** |

Annexes that sit outside the 15-page limit — use them, this is free scoring space:
Annex 1 Experience Sheet (≤3 examples, 1 page each, 2 referees each), Annex 1 Workplan (activity ×
month, ≤1 page), CV pack in the mandated format (each with 2 referees + signed declaration).

Referee constraints are strict: must comment in English, must be available during selection, and
must not be an employee/executive/business associate of the tenderer, a proposed consultant on this
bid, or a DT Global/DFAT employee. **Confirm referee availability before naming them** — this is a
common and avoidable failure.

---

## 7. 54-hour execution plan (if bidding)

### Gate — tonight, 24 Aug, before anything else
Confirm the bidding entity's akta + SK Kemenkumham + NPWP + domicile documents exist as scannable
files. **If they do not exist and cannot exist by 26 Aug, stop and switch to Option C.** Every hour
spent writing before this is confirmed is at risk of being wasted.

### Tue 25 Aug — content
- Download and complete the three DT Global templates (Due Diligence Preliminary Supplier Statement,
  Tenderer's Declaration, VAT Commitment Letter if PKP) — these need a director's signature, so start here
- Part A + Annex 1 experience sheets (3 × 1 page), referees contacted and confirmed
- Part C CVs in the mandated format, signed declarations, 2 confirmed referees each
- Draft Part B: methodology per phase, the four assumption statements from §5, CMS comparison table

### Wed 26 Aug — assembly, morning to mid-afternoon
- Financial proposal: allocation table, LOE table, payment terms, net-of-VAT statement
- Annex 1 workplan (one page, activity × month, Sep 2026 → Jan 2028)
- Compliance sweep: 15-page limit, 12pt, English, no external logos, correct part order
- Package check: attachments each under 25 MB, filenames clean

### Wed 26 Aug — send by 18:00 WIB
Six hours of buffer before the 23:59 cutoff. Email delivery failures, attachment size rejections,
and last-minute signature chases are the normal causes of a missed donor deadline — not slow
writing. **Do not plan to send at 23:00.**

---

## 8. What carries forward regardless of outcome

Whether this bid is submitted or not, these artefacts have value beyond 26 August and should exist
by the end of the week:

- Reusable 15-page technical proposal skeleton for donor-funded web RFPs
- CV pack in DT Global's mandated format, kept current
- Experience-sheet template in Annex 1 format, populated as projects complete
- Compliance policy set DFAT due diligence will require: anti-bribery/anti-corruption, safeguarding
  and PSEAH, child protection, basic financial governance — short, genuine, board-adopted
- A confirmed referee list, with availability pre-agreed
- A shortlist of registered partner entities for future KSO arrangements

The binding constraint on this bid was never technical capability. On the 50% block the stack
alignment is genuinely strong. It was corporate paperwork and a 54-hour window — and both of those
are fixable before the next one.
