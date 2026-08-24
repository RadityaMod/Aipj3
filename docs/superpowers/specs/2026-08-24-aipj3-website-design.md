# AIPJ3 Website — Build Design

**Status:** approved design, pre-implementation
**Date:** 24 August 2026
**Contract:** RFP/Website Development/018-08-2026 — AIPJ3 Website Development and Maintenance
**Scope of this document:** the system to be built assuming the bid succeeds. It is not proposal text.

---

## 1. Context

AIPJ3 (DT Global, DFAT-funded) is contracting a 16-month engagement: a four-month build of a
bilingual, accessible public website, followed by twelve months of hosting and maintenance,
inside a fixed ceiling of **IDR 150,000,000**.

Two constraints control every decision below.

**The fixed ceiling meets a contractual discovery phase.** Phase 1 (15 Sep – 15 Oct 2026)
produces the sitemap, content hierarchy and navigation taxonomy *with stakeholders*, and is
formally signed off as Deliverable 1. The architecture must therefore absorb discovery
outcomes as **configuration rather than rework**. Any design that requires new code per
content type converts every workshop decision into unbudgeted work.

**The SLA meets a small team.** The maintenance stage commits to 99.9% uptime, critical
security patches within 48 hours, and twelve months of monitoring and reporting. A small
team cannot safely carry those obligations on a live application stack. Reducing the
public runtime surface to zero is how that promise becomes cheap to keep.

---

## 2. Architecture

Two units, deployed separately, with deliberately asymmetric availability requirements.

**Public site.** Next.js 15, static output, built in CI, synced to Indonesia-resident
object storage, served through a CDN with WAF. No server process, no database connection,
no runtime secrets.

**Editorial platform.** Payload CMS v3 with PostgreSQL on a private, authenticated admin
host. Low traffic. Not on the public critical path.

The property this buys: **CMS downtime does not cause site downtime.** The last successful
build keeps serving, and a failed build leaves the previous bundle live. The 99.9%
commitment becomes a CDN commitment rather than an application one, and the public site
retains almost no OWASP attack surface.

This also satisfies the contract's required layers natively — Node 22 LTS, TypeScript,
PostgreSQL — so no part of the stack needs justifying as a substitution.

### 2.1 Publishing flow

```
Editor publishes in Payload
  → afterChange hook fires build webhook
  → GitHub Actions pulls content via Payload API
  → next build (static output)
  → sync to object storage
  → CDN cache purge
  → live in approximately 3-6 minutes
```

Build latency is acceptable because the contracted content cadence is weekly.

**Emergency fast-path.** A `workflow_dispatch` trigger on the same pipeline allows a
manual rebuild without a content change, for urgent corrections and rollbacks. Documented
in the runbook and demonstrated during training, so the expectation is set explicitly
rather than discovered during an incident.

### 2.2 Preview

Approvers must see drafts before publishing. `apps/web` supports two build modes from one
codebase, selected by the `BUILD_TARGET` environment variable:

- `BUILD_TARGET=static` — `output: 'export'`, used for production
- `BUILD_TARGET=server` — standard Next server with draft mode enabled, used for preview

The preview deployment runs authenticated on the admin host, and Payload's live preview
points at it. One codebase, two modes, no third application.

---

## 3. Content model

The following is a **strawman for Phase 1**, derived from the RFP's own stated purposes:
communicate identity, messages and values; document and disseminate progress, learning and
impact; connect stakeholders and partners; drive read, download, share and feedback.

It is explicitly expected to change during discovery. The block system below is what makes
that change cheap.

### 3.1 Collections

| Collection | Purpose |
|---|---|
| `pages` | Block-composed — About, Approach, Contact, landing pages |
| `news` | Updates and stories: hero, body blocks, date, EOPO tags |
| `publications` | Reports, briefs, guidelines — file, cover image, abstract, EOPO tags |
| `events` | Briefings, launches, workshops |
| `partners` | GOI institutions, CSOs, Australian agencies — logo, category, link |
| `people` | Program leads and spokespeople |
| `eopos` | Controlled taxonomy, four fixed entries |
| `media` | Uploads, with alt text required in both locales |

Globals: `navigation`, `siteSettings`, `footer`, `homepage`.

`people` is the thinnest collection here and the most likely candidate to be cut in
discovery. It is included so the question gets asked in the workshop rather than assumed.

### 3.2 The EOPO taxonomy is the structural spine

Every content item tags to one or more of the four end-of-program outcomes. This makes the
entire site navigable by outcome, which mirrors how DFAT and GOI already reason about the
program, and turns "document and disseminate progress" from an undifferentiated blog into
a real information architecture.

### 3.3 Accessibility enforced at the schema layer

`media.alt` is a required, localised field. An image without alt text in both locales
cannot be saved, so it cannot reach review, let alone publication. Accessibility becomes a
property of the data model rather than a review-time checklist item.

### 3.4 Block library

`richText`, `mediaWithCaption`, `quote`, `statistic`, `accordion`, `cardGrid`,
`callToAction`, `embed`, `publicationList`, `newsList`, `partnerLogos`, `timeline`.

Each is a typed Payload block with a matching React component in `packages/ui`. Adding a
page type during Phase 1 means composing existing blocks — no new code. This is the
mechanism that converts discovery outcomes into configuration, and it is the single most
important structural decision in this document.

### 3.5 Localisation

Payload field-level localisation. Locales `en` and `id`; `en` is default and fallback.
Routes are `/en/...` and `/id/...`, with reciprocal `hreflang` tags and a locale switcher
that preserves the current document rather than returning to the homepage.

Publication *files* are themselves localised fields, so a report existing only in Bahasa
Indonesia is representable within the model instead of being an exception to it.

**Missing-translation policy.** When a document has no translation for the requested
locale, serve the English content with a visible notice stating the Indonesian version is
not yet available, and set `lang="en"` on that content region. Never silently mix
languages within a page — it misleads sighted readers and gives screen readers the wrong
pronunciation.

---

## 4. Access control and editorial workflow

The contract requires RBAC explicitly. The Background section adds that the Communications
Team holds narrative control "following DFAT's approval mechanism" — a workflow
requirement, not merely a permissions one.

| Role | Capability |
|---|---|
| `contributor` | Create and edit drafts only |
| `editor` | Create, edit, submit for approval — the comms team |
| `approver` | Publish rights — the Strategic Communications Manager |
| `admin` | Technical administration and user management |

Document states: **draft → in review → approved → published**, implemented with Payload's
native `_status` plus a `reviewState` field. Payload's version history provides the audit
trail. The publish operation is gated on the `approver` role in collection access control.

This makes the DFAT approval mechanism mechanical rather than procedural — it cannot be
bypassed by someone in a hurry.

---

## 5. Accessibility as a build gate

WCAG 2.2 Level AA is enforced in CI, not audited afterwards:

- **axe-core via Playwright** on every template in both locales — the build fails on any violation
- **Lighthouse CI** budgets: LCP < 2.5s, INP < 200ms, CLS < 0.1, score ≥ 90 across all categories — the build fails below threshold
- **eslint-plugin-jsx-a11y** in the lint stage
- Bilingual alt text required at the CMS layer (§3.3)

Manual testing sessions with disabled participants are contracted and budgeted within
Phase 2. The automated gates exist so that those sessions surface genuine usability
problems instead of consuming their time on missing alt attributes.

---

## 6. Security

TLS 1.3 terminated at the CDN. Content-Security-Policy, HSTS, `X-Content-Type-Options`,
`Referrer-Policy` and `Permissions-Policy` are configured as **CDN response headers** —
static hosting cannot set headers from application code, so this belongs in `infra/` and
must be verified early rather than assumed. WAF at the edge.

The Payload admin host is protected by Payload authentication with two-factor enabled,
request rate limiting, and a network access layer at the CDN restricting `/admin` to
authenticated staff. Dependabot and `npm audit` run in CI; an OWASP Top 10 review
checklist is completed per release.

Because the public site is inert files, the majority of the OWASP Top 10 has no public
attack surface. The residual surface is the admin host, which is private.

---

## 7. Supporting decisions

**Search — Pagefind.** Builds a static index at build time, runs entirely client-side,
handles both locales, and costs nothing to operate. Publication filtering by EOPO, type
and year is static faceting over the same index. Chosen because it is the only search
approach that preserves the zero-runtime property.

**Analytics — GA4 via Google Tag Manager with Consent Mode v2.** No non-essential tag
fires before opt-in; no analytics cookies are set pre-consent. Search Console is verified
at launch and the baseline report is delivered within five business days of go-live, as
the contract requires.

---

## 8. Repository structure

pnpm workspaces monorepo:

```
apps/
  web/           Next.js 15 — static export (production) and server mode (preview)
  cms/           Payload v3 + PostgreSQL
packages/
  ui/            design system and block components
  content/       generated Payload types, shared schema contracts
  config/        eslint, tsconfig, tailwind preset
infra/           IaC, CDN configuration, response headers, backup scripts
docs/            runbooks, training material, ADRs
.github/workflows/
```

---

## 9. Testing strategy

| Layer | Tool | Covers |
|---|---|---|
| Unit | Vitest | Block renderers, localisation fallback, formatting |
| Integration | Vitest + Payload local API | Access control: role × collection × operation matrix |
| End-to-end | Playwright | Publish→build→appear, locale switching, search, download |
| Accessibility | axe-core + Playwright | Every template, both locales |
| Performance | Lighthouse CI | Core Web Vitals budgets |

The access-control matrix is tested exhaustively rather than by sampling. A role
escalation here means unapproved content reaching a DFAT-facing public site, which is the
highest-consequence failure available in this system.

Visual regression testing is deliberately excluded — its maintenance cost is not justified
at this budget.

---

## 10. Maintenance runbook

The twelve-month obligation, stated as operable procedures:

- Uptime monitoring with alerting; records retained as SLA evidence
- Nightly PostgreSQL dump and media sync to off-site storage held with a **different
  provider in a different failure domain** from primary hosting
- **Monthly restore drill** — restore the dump into a clean database and verify content
  integrity. The contract requires backup *verification*, which means restoring, not
  confirming that a file exists
- Weekly automated dependency PRs; a documented path for applying critical CVE patches
  within the contracted 48 hours
- Monthly report: uptime, Core Web Vitals, traffic, content published, incidents
- Six-monthly deeper performance and accessibility re-audit
- Annual penetration testing recommendation (advisory, per contract)
- Content upload service: AIPJ3 supplies final publications and photos; editor uploads;
  approver publishes — within the agreed monthly hours allocation

## 11. Handover and exit

IaC, runbooks and architecture decision records live in the repository. The two-hour live
training session (Deliverable 4) is recorded, accompanied by a bilingual admin guide.

Every component is MIT-licensed or standard infrastructure — Payload, PostgreSQL, object
storage — so at contract end AIPJ3 can retender or self-host with no licence negotiation
and no vendor lock-in. This is a direct value-for-money argument and should be stated as
one in reporting.

---

## 12. Delivery phases mapped to contract deliverables

| Phase | Window | Deliverables |
|---|---|---|
| 1 — Design Concept | 15 Sep – 15 Oct 2026 | D1: requirements, personas, sitemap, wireframes |
| 2 — Development | 16 Oct 2026 – 22 Jan 2027 | D2: Figma mockups (30 Nov) · D3: built site, UAT (22 Jan) |
| 3 — Launch | 23 – 29 Jan 2027 | DNS/SSL cutover, GA4 and Search Console baseline |
| 4 — Maintenance | 29 Jan 2027 – 28 Jan 2028 | D4 training · D5 audit · D6 post-launch report · D7 maintenance |

**Note on contract dates.** Deliverable 3 is written as "22 Jan 2026" in the RFP; this is
read as 2027, consistent with the development stage ending 22 January 2027. Deliverables 4
through 6 fall after the maintenance stage begins and are treated as launch-hardening
within the first maintenance month. Both readings are stated as assumptions at inception
rather than raised as corrections.

**Build order within Phase 2:** infrastructure and CI, then the block platform and design
system, then collections and access control, then page templates, then search and
analytics, then hardening. Access control lands early because the shape of everything
downstream depends on it.

---

## 13. Risks

| Risk | Mitigation |
|---|---|
| Discovery reshapes the information architecture | Block platform absorbs it as configuration (§3.4) |
| Static rebuild too slow for an urgent correction | Documented emergency fast-path (§2.1); expectations set in training |
| Local object storage may not support custom response headers or a cache purge API | **Phase 1 gate** — verify before committing; fallback is a CDN in front of a local origin |
| Recruiting disabled participants has lead time | Book during Phase 1, run sessions in Phase 2 |
| Bus factor of one at this budget | ADRs, runbooks and IaC maintained from day one |

Row three is the only risk that can invalidate the hosting decision itself, which is why
it is a Phase 1 gate rather than a Phase 2 discovery. The provider must be confirmed to
support custom response headers and programmatic cache invalidation before any
infrastructure work begins.

---

## 14. Verification

The system is correct when all of the following hold:

1. `pnpm test` passes — unit, integration, and the complete access-control matrix
2. `pnpm test:e2e` passes — Playwright, including the publish→build→appear path against a
   seeded Payload instance
3. `pnpm test:a11y` reports zero axe violations across every template in both locales
4. Lighthouse CI meets all four budgets against the built static output
5. **Manual role check:** signed in as `editor`, create a bilingual publication and confirm
   the publish action is refused; signed in as `approver`, publish it; confirm it appears
   on the CDN within the build window in both locales, is reachable through Pagefind
   search, and that the attached file downloads
6. **Restore drill:** take a nightly dump, restore it into a clean database, and verify
   content integrity

Steps 5 and 6 prove the contract obligations. Steps 1 through 4 prove the code.
