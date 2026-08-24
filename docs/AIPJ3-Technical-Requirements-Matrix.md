# AIPJ3 Website — Full Technical Requirements Matrix

**RFP:** RFP/Website Development/018-08-2026
**Purpose:** every technical requirement in the RFP, mapped to a decided response.
**Companion documents:** architecture in `superpowers/specs/2026-08-24-aipj3-website-design.md`;
commercial position in `AIPJ3-RFP-Strategy.md`.

*Written in English because it feeds Part B of the proposal, which the RFP requires to be in
English. An Indonesian rendering can be produced on request.*

## How to read the compliance column

| Mark | Meaning |
|---|---|
| **C** | Complies as specified |
| **C+** | Complies and exceeds the stated requirement |
| **D** | Deviates — an alternative is proposed, with advantages and disadvantages stated in §9 |
| **A** | Complies subject to a stated assumption (§10) |
| **P** | Partly within our control — shared with the client, noted in §11 |

---

## 1. Objectives (TOR §B) — 8 requirements

| # | Requirement | Response | |
|---|---|---|---|
| O1 | Modern, responsive, bilingual website to current standards | Next.js 15, TypeScript, mobile-first responsive; EN/ID as field-level localisation, not a translation plugin | **C** |
| O2 | Full compliance with WCAG 2.2 Level AA | Enforced as a CI build gate (axe-core), not a post-hoc audit; plus manual testing with disabled participants | **C+** |
| O3 | Strong Core Web Vitals (LCP, INP, CLS) | Static assets from CDN; Lighthouse CI budgets fail the build below threshold | **C+** |
| O4 | Support content updates on a weekly basis | Payload editorial workflow; publish triggers rebuild, live in 3–6 min | **C** |
| O5 | Analytics, consent management, privacy-compliant tracking | GA4 via GTM with Consent Mode v2; no non-essential tag fires pre-consent | **C** |
| O6 | Secure, scalable hosting with documented maintenance and support procedures | Indonesia-resident object storage + CDN/WAF; runbooks in repo | **C** |
| O7 | Regular content uploads | Contracted upload service within monthly hours allocation | **C** |
| O8 | Complete all phases within agreed timeline and budget | Phased plan mapped to the seven deliverables; allocation model within the IDR 150M ceiling | **C** |

---

## 2. Phase 1 — Design Concept (TOR §C.1, 15 Sep – 15 Oct 2026) — 6 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P1.1 | Client and stakeholder meetings to capture business requirements, user needs, content strategy | Two facilitated workshops plus written requirements register, signed off | **C** |
| P1.2 | UX research including persona development and user journey mapping | Three personas: GOI justice institution officials; DFAT/Australian accountability stakeholders; Indonesian civil society and general public. Journey maps per persona | **C** |
| P1.3 | Information architecture — sitemap, content hierarchy, navigation taxonomy | Sitemap plus the EOPO taxonomy as the navigational spine; strawman content model taken in as a starting point, not an output | **C** |
| P1.4 | Low-fidelity wireframes for key page templates (home, interior, contact, landing) | Wireframes for all four, both breakpoint families | **C** |
| P1.5 | Brand and visual direction — typography, colour palette, design language documentation | Design tokens defined as CSS custom properties from the outset, so the documentation and the implementation are the same artefact | **C+** |
| P1.6 | Formal sign-off for development stage | Deliverable 1 acceptance by the Strategic Communications Manager | **C** |

**Note.** Phase 1 also carries a technical gate of our own: confirming the hosting provider supports
custom response headers and a programmatic cache-purge API (§10, A3). This must close before any
infrastructure work begins.

---

## 3. Phase 2 — Development (TOR §C.2, 16 Oct 2026 – 22 Jan 2027)

### 3.1 UI/UX Design (§3.2.1) — 2 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.1 | High-fidelity mockups in Figma (or equivalent) for desktop, tablet, mobile | Figma, three breakpoints, built on the Phase 1 token set | **C** |
| P2.2 | Interactive prototype for stakeholder review and iterative feedback | Figma prototype; two structured feedback rounds scheduled | **C** |

### 3.2 Front-End Development (§3.2.2) — 5 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.3 | Semantic HTML5 with ARIA landmarks and roles for screen readers | Landmark structure enforced per template; axe assertions in CI | **C** |
| P2.4 | CSS3 with custom properties (design tokens) and Tailwind CSS 4 | Tailwind 4 with the token layer as CSS custom properties | **C** |
| P2.5 | Selected application framework (JS ES2024 / TypeScript; React 19 / Next.js 15 or Vue 3 / Nuxt 3) | Next.js 15 + React 19 + TypeScript — from the named list, no justification burden | **C** |
| P2.6 | Mobile-first responsive layouts tested across Chrome, Firefox, Safari, Edge | Playwright matrix across all four engines; mobile-first authoring | **C** |
| P2.7 | Progressive enhancement principles | Content and navigation function without JavaScript; JS enhances only | **C** |

### 3.3 CMS Integration (§3.2.3) — 3 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.8 | Client-approved CMS | Payload v3 self-hosted, proposed for client approval — see deviation D2 | **D** |
| P2.9 | Custom page templates, reusable block components, structured content models | Twelve typed blocks; new page types are composition, not code | **C+** |
| P2.10 | Role-based access control (RBAC) | Four roles (contributor, editor, approver, admin) plus a draft→review→approved→published workflow implementing the DFAT approval mechanism | **C+** |

### 3.4 Back-End and Integrations (§3.2.4) — 2 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.11 | Propose API development where required | Payload REST/GraphQL consumed at build time. No public runtime API is proposed — the public site needs none, and every endpoint not shipped is attack surface not created | **D** |
| P2.12 | Optimal performance and SEO | Static delivery; per-locale sitemaps, `hreflang` pairs, canonical URLs, structured data for publications and events | **C** |

### 3.5 Security (§3.2.5) — 4 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.13 | HTTPS enforcement | TLS 1.3 at CDN, HSTS with preload, HTTP→HTTPS redirect | **C** |
| P2.14 | HTTP security headers | CSP, HSTS, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`, `X-Frame-Options` — set as CDN response headers, since static hosting cannot set them from application code | **C** |
| P2.15 | OWASP Top 10 mitigation | Reviewed per release. The public site is inert files, so most categories have no public surface; the residual surface is the private admin host | **C** |
| P2.16 | Other configuration as identified | WAF rules, bot mitigation, rate limiting on admin, dependency scanning in CI | **C** |

### 3.6 Testing and QA (§3.2.6) — 5 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P2.17 | Cross-browser and cross-device matrix (desktop, tablet, mobile; iOS and Android) | Playwright across Chromium, Firefox, WebKit; iOS Safari and Android Chrome device profiles | **C** |
| P2.18 | Automated, manual and integration tests | Vitest unit; Payload local-API integration including the exhaustive role × collection × operation access-control matrix; Playwright E2E; scripted manual UAT | **C+** |
| P2.19 | Accessibility audit including with people with disability, WCAG 2.2 AA | Automated gates in CI **plus** paid testing sessions with disabled participants through a named partner organisation. Directly serves EOPO 3 | **C+** |
| P2.20 | Performance audit using Lighthouse and WebPageTest; target ≥ 90 all categories | Lighthouse CI budgets enforced per build; WebPageTest run at UAT and at launch. See §11 R1 on the GTM tension | **C** |
| P2.21 | User Acceptance Testing with nominated client representatives | Scripted UAT against the requirements register from P1.1; defect triage and re-test cycle | **C** |

---

## 4. Phase 3 — Launch (TOR §C.3, 23–29 Jan 2027) — 5 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P3.1 | Pre-launch trial | Full staging rehearsal on production-equivalent infrastructure | **C** |
| P3.2 | DNS migration, SSL/TLS configuration, temporary site transition coordination | Runbook with lowered TTL ahead of cutover, certificate provisioning and validation, documented rollback | **C** |
| P3.3 | Production deployment | Pipeline-driven; the previous bundle stays live until the new one is verified | **C+** |
| P3.4 | Post-launch testing including real user monitoring and error tracking | RUM for field Core Web Vitals; client-side error tracking with alerting | **C** |
| P3.5 | GA4 and Search Console baseline report within 5 business days of go-live | Property and Search Console verified pre-launch so the baseline window starts at go-live, not after setup | **C** |

---

## 5. Phase 4 — Maintenance (TOR §C.4, 29 Jan 2027 – 28 Jan 2028) — 7 requirements

| # | Requirement | Response | |
|---|---|---|---|
| P4.1 | CMS core, plugin and updates; critical security patches within 48 hours of release | Weekly automated dependency PRs; documented 48-hour critical-CVE path with named responsible party | **C** |
| P4.2 | Monthly automated backup verification and off-site backup management | Nightly Postgres dump and media sync to a **different provider in a different failure domain**, plus a **monthly restore drill** into a clean database — verification means restoring, not confirming a file exists | **C+** |
| P4.3 | Uptime monitoring, ≥ 99.9% SLA | External monitoring with alerting; records retained as SLA evidence. Static-first means this is a CDN commitment, not an application one — see §11 R2 on measurement | **C** |
| P4.4 | Monthly and six-monthly performance reports, Core Web Vitals dashboard | Monthly: uptime, CWV, traffic, content published, incidents. Six-monthly: deeper performance and accessibility re-audit | **C** |
| P4.5 | Content uploads and bug fixes within agreed monthly hours allocation | AIPJ3 supplies final publications and photos; editor uploads; approver publishes. Hours tracked and reported monthly | **C** |
| P4.6 | Security protocol document, annual comprehensive security audit and penetration testing recommendation | Security protocol at handover; annual audit; penetration testing **recommendation** — the RFP wording is advisory, so scoping and procurement of an actual test sits with AIPJ3 (§11 R4) | **A** |
| P4.7 | Hosting provider (local) | Indonesia-resident infrastructure — see deviation D3 and assumption A1 | **D/A** |

---

## 6. Deliverables and acceptance criteria (TOR §D) — 7 deliverables

| # | Deliverable | Acceptance criterion | Due | Response |
|---|---|---|---|---|
| D1 | Design Concept | Signed off by Strategic Communications Manager | 15 Oct 2026 | Requirements register, personas, sitemap, wireframes |
| D2 | UI Design Mockups | Design approval in writing | 30 Nov 2026 | Figma, three breakpoints, interactive prototype |
| D3 | Developed Website | UAT test result | 22 Jan 2027 *(RFP prints 2026 — read as 2027, §10 A4)* | Full site, both locales, CI gates green |
| D4 | CMS and Admin Training | Attendance documentation | 22 Feb 2027 | Two-hour live session, recorded, bilingual admin guide |
| D5 | Accessibility and Performance Audit | Audit report delivered | 1 Mar 2027 | WCAG 2.2 AA report incl. disabled-participant findings; Lighthouse ≥ 90 evidence |
| D6 | Post-Launch Report | Report accepted in writing | 1 Mar 2027 | Analytics baseline, uptime confirmation, issue log |
| D7 | Maintenance Agreement | Security protocol, performance reports, weekly content support, hosting | 29 Jan 2027 – 28 Jan 2028 | Per §5 above |

---

## 7. Technology stack — Selection Criteria §H (50% weight)

| Layer | RFP requirement | Proposed | |
|---|---|---|---|
| Front-End | HTML5, CSS3, JavaScript ES2024, TypeScript | As specified | **C** |
| Frameworks | React 19 / Next.js 15 **or** Vue 3 / Nuxt 3 **or as proposed** | Next.js 15 + React 19 | **C** |
| Styling | Tailwind CSS 4, CSS custom properties | As specified | **C** |
| CMS | Headless CMS (Contentful, Sanity) | Payload v3, self-hosted — **D2** | **D** |
| Back-End / API | Node.js 22 LTS, REST or GraphQL | Node 22 LTS; Payload exposes both, consumed at build time | **C** |
| Database | PostgreSQL / MySQL or serverless | PostgreSQL | **C** |
| Hosting / Infra | AWS / Azure / Vercel / Cloudflare Pages | Indonesia-resident storage + CDN/WAF — **D3** | **D** |
| Version Control | Git (GitHub / GitLab), CI/CD pipelines | GitHub + GitHub Actions | **C** |
| Security | HTTPS/TLS 1.3, CSP headers, WAF, OWASP Top 10 | As specified, at the CDN edge | **C** |
| Accessibility | WCAG 2.2 Level AA, ARIA landmarks | As specified, enforced in CI | **C+** |
| Analytics | GA4 + Consent Mode v2, Google Tag Manager | As specified | **C** |
| Performance KPIs | LCP < 2.5s, INP < 200ms, CLS < 0.1 | Enforced as CI budgets | **C+** |

**Ten of twelve layers match the named list exactly.** Only CMS and hosting deviate, and both are
argued under the clause the RFP itself provides.

---

## 8. Key personnel — technical competencies (Selection Criteria §H, 30% weight)

| Role | Minimum experience | Technical competencies required |
|---|---|---|
| Project Manager | 8 years managing website development projects | Preferably development, private and/or public sector |
| Front-end developer | 5 years | HTML, CSS, JavaScript; React/Vue; browser devtools; API integration; performance and accessibility optimisation |
| Back-end developer | 5 years | Server languages, database management, API design, cloud services |
| DevOps engineer | 5 years | Configuration management, version control, security, scalable automated testing, scalable applications |
| QA engineer | 5 years | Automation tools, API testing |

**Status: not yet staffed.** This block is 30% of the technical score and currently has no CVs, no
signed declarations, and no confirmed referees. Each CV additionally requires two referees who can
comment in English, are available during selection, and are not employees, executives, business
associates, proposed consultants, or DT Global/DFAT staff. This is the largest open gap in the
submission and it is a recruitment task, not a writing task.

---

## 9. Deviation register

The RFP invites this directly: *"The following list is for reference only. Provider could identify
other than the list with description of its advantages and disadvantages."* Each deviation below
states real disadvantages, because a register listing only benefits is not a register.

### D1 — Static-first delivery rather than a server-rendered application

**Advantages.** Near-zero public runtime attack surface. The 99.9% uptime SLA becomes a CDN
commitment rather than an application one. CMS downtime cannot cause site downtime, and a failed
build leaves the previous bundle serving. Best achievable Core Web Vitals. Hosting cost low enough
to fit the ceiling alongside twelve months of maintenance.

**Disadvantages.** Published changes appear in 3–6 minutes rather than instantly, mitigated by a
documented emergency rebuild path. No server-side personalisation or real-time features — none are
in scope. Build duration grows with content volume; at the scale of this program it is not a
constraint within the contract term.

### D2 — Payload v3 self-hosted rather than Contentful or Sanity

**Advantages.** No licence cost in perpetuity — material because the subscription would become
AIPJ3's recurring cost after handover, not ours. Full data residency, consistent with D3. Native
RBAC and draft/publish workflow without a paid tier. Node 22 / TypeScript / PostgreSQL matches three
required stack layers natively. MIT licensed, so no vendor lock-in at contract end.

**Disadvantages.** We operate it, where a SaaS vendor would. Smaller ecosystem and fewer
off-the-shelf integrations than Contentful. The admin host must be patched and monitored — real work
we are taking on. No third-party vendor SLA to point to; the availability commitment is ours. This
is the deviation most likely to draw a question, and the answer is that the operational burden is
bounded because the admin host is not on the public critical path.

### D3 — Indonesia-resident hosting rather than the named platforms

**Advantages.** Satisfies the maintenance clause's *local* requirement literally rather than by
argument. Data residency is appropriate for a GOI–DFAT partnership program independently of the
clause. Lower latency for the primary Indonesian audience.

**Disadvantages.** Local providers vary in tooling maturity — custom response headers and a
programmatic purge API are not universal, which is exactly why this is a Phase 1 gate (A3). Less
mature infrastructure-as-code ecosystem than AWS or Vercel. If the provider check fails, the
fallback is a CDN in front of a local origin, which preserves residency at some added complexity.

### D4 — Pagefind static search rather than a hosted search service

**Advantages.** No server, no subscription, no operational surface. Multilingual out of the box.
Index builds as part of the existing pipeline.

**Disadvantages.** Index ships to the client, so size grows with the corpus — acceptable at this
scale, not at tens of thousands of documents. Query analytics require separate client-side
instrumentation rather than arriving from a search vendor's dashboard.

### D5 — No public runtime API

**Advantages.** Endpoints not shipped cannot be attacked, rate-limited, or left unpatched. Nothing
in the scope requires one.

**Disadvantages.** Any future requirement for third-party data consumption would need a new
component. Flagged now so it is a conscious choice rather than a discovered limitation.

---

## 10. Assumptions to state at inception

The written-questions window closed on 20 August 2026, so these cannot be clarified before
submission and must be stated in the proposal.

| # | Assumption |
|---|---|
| **A1** | "Hosting provider (local)" is read as requiring Indonesia-resident infrastructure. A variant using an approved global platform can be provided if AIPJ3 intends "local" as contracting presence only. |
| **A2** | "Client-approved CMS" permits a headless CMS outside the two named examples, consistent with §3.2.2's invitation to propose alternatives. |
| **A3** | The selected hosting provider supports custom HTTP response headers and a programmatic cache-purge API. **Verified as a Phase 1 gate before infrastructure work begins.** |
| **A4** | Deliverable 3's date of 22 January 2026 is read as 2027, consistent with the development stage ending 22 January 2027. Deliverables 4–6 are treated as launch-hardening within the first maintenance month. |
| **A5** | Accessibility testing "with people with disability" means paid sessions with disabled participants, and their recruitment is budgeted within Phase 2. |
| **A6** | The program's VAT exemption under PMK 59/2024 applies; pricing is quoted net of VAT. |

---

## 11. Risks and honest tensions

**R1 — GA4/GTM versus Lighthouse ≥ 90.** The RFP requires both Google Tag Manager and a Lighthouse
score of at least 90 across all categories. A default GTM container measurably costs Performance
points. Mitigation: consent-gated loading so no tag executes before opt-in, deferred initialisation
until browser idle, and a minimal container. We commit to ≥ 90 measured under the consent state a
first-time visitor actually experiences, and will report the post-consent figure separately. This
tension is real and stating it is more credible than promising both without qualification.

**R2 — 99.9% uptime measurement.** 99.9% allows roughly 43 minutes of downtime per month. The
measurement method, monitoring location, and what counts as an outage should be agreed at inception,
because an unstated definition is the usual source of SLA disputes. Static-first delivery makes the
target comfortably achievable; the definition still needs writing down.

**R3 — WCAG 2.2 AA is partly content-dependent.** Automated gates and required bilingual alt text
cannot prevent an editor writing uninformative link text or poor heading order in rich text.
Mitigation: CMS-level validation where mechanically checkable, plus editorial guidance in the D4
training. Ongoing conformance is a shared responsibility and should be described as one.

**R4 — Penetration testing is advisory.** The TOR asks for a "penetration testing recommendation",
not a test. We will produce the recommendation and scope; commissioning an actual test sits with
AIPJ3 and is not priced here. Worth confirming at inception, since it is easily misread in both
directions.

**R5 — Personnel block unstaffed.** 30% of the technical score currently has no CVs and no confirmed
referees (§8). Unlike every other item in this matrix, this cannot be resolved by writing.

---

## 12. Coverage summary

| Area | Requirements | Complies | Exceeds | Deviates | Assumption-bound |
|---|---:|---:|---:|---:|---:|
| Objectives | 8 | 6 | 2 | — | — |
| Phase 1 Design Concept | 6 | 5 | 1 | — | — |
| Phase 2 Development | 21 | 16 | 3 | 2 | — |
| Phase 3 Launch | 5 | 4 | 1 | — | — |
| Phase 4 Maintenance | 7 | 4 | 1 | 1 | 1 |
| Technology stack | 12 | 8 | 2 | 2 | — |
| **Total** | **59** | **43** | **10** | **5** | **1** |

Every deviation is argued under the clause the RFP itself provides, and ten of twelve stack layers
match the named list exactly. The technical response is not the constraint on this bid — §8 and §11
R5 are.
