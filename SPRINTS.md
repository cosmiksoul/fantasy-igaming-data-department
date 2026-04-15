# SPRINTS.md — Delivery Plan

## Sprint 0: Foundation
**Goal:** shared infrastructure, design system, working navigation

**Tasks:**
- [ ] Create `css/style.css` — full design system: CSS variables (colors, fonts, spacing, radii), base typography, layout (mobile/tablet/desktop), all reusable components (accordion, card, tool-card, metric-card, alert, code-block, badge, sla-row, person-card, timeline-block)
- [ ] Create `js/nav.js` — sidebar navigation (desktop: fixed, mobile: burger + slide-out panel), active page highlight, breadcrumb generation, prev/next links at page bottom, accordion toggle function
- [ ] Create `index.html` — hero (title, subtitle, description, CTA), company card, section grid (18 cards in 2-col grid desktop / 1-col mobile, each links to corresponding page), disclaimer, footer
- [ ] Create page template (`pages/_template.html`) — boilerplate with nav include, breadcrumbs, main content area, prev/next, footer. All subsequent pages copy from this.

**Done when:** index.html loads, navigation works on mobile and desktop, clicking a section card leads to a placeholder page with working nav.

---

## Sprint 1: Data Architecture
**Goal:** page 01 — full stack diagram with tool cards

**Tasks:**
- [ ] `pages/data-architecture.html` — interactive stack diagram (9 layers, each is an accordion)
- [ ] Per layer: 2-5 tool cards with descriptions, alternatives, trade-offs
- [ ] Layer content: Sources (7 tools), Ingestion (3), Storage (3), Transformation (3), Orchestration (3), DQ & Governance (3), BI (4), ML (3), Reverse ETL (2)
- [ ] Cross-links to related pages (governance → 06, BI → 12, ML → 09)

---

## Sprint 2: Org Structure
**Goal:** page 02 — org chart + stream details

**Tasks:**
- [ ] `pages/org-structure.html` — visual org chart (Director → 4 leads → teams). SVG or HTML/CSS based.
- [ ] 4 stream detail sections (accordion per stream): people, responsibilities, interactions, deliverables
- [ ] RACI matrix (HTML table)
- [ ] Skill matrix (HTML table)
- [ ] Career ladder section

---

## Sprint 3: Data Model + Event Taxonomy
**Goal:** pages 03 and 04

**Tasks:**
- [ ] `pages/data-model.html` — mermaid.js ERD diagram (8 core entities with relationships)
- [ ] Entity descriptions (accordion per table): all fields, types, descriptions
- [ ] dbt layers section: staging → intermediate → marts. 1 SQL example per layer.
- [ ] Mart descriptions: fields, source models, refresh frequency
- [ ] `pages/event-taxonomy.html` — naming convention section
- [ ] Event schema (standard structure with JSON examples)
- [ ] Tracking plan table (10-15 events)
- [ ] Change process section

---

## Sprint 4: Metrics Dictionary
**Goal:** page 05 — 15-20 metric cards

**Tasks:**
- [ ] `pages/metrics.html` — filter/group by category (Revenue, Unit Economics, Players, Marketing, Product)
- [ ] 15-20 metric cards: definition, formula, SQL example, benchmarks (EU/LatAm/SEA), alerts (red/yellow), owner, pitfalls, dependencies, dimensions
- [ ] SQL examples query mart tables from data model (page 03)
- [ ] Link to full CSV catalog (GitHub raw file)

**Source data:** `/uploads/Список_метрик_iGaming_*.csv`

---

## Sprint 5: Data Governance + SLA
**Goal:** pages 06 and 07

**Tasks:**
- [ ] `pages/data-governance.html` — roles section (owners, stewards, council with examples)
- [ ] Data Catalog section (DataHub card example)
- [ ] Data Dictionary section (definitions + change process)
- [ ] RBAC matrix (HTML table)
- [ ] DQ framework (5 dimensions with test examples)
- [ ] Data lifecycle (retention policy diagram)
- [ ] `pages/sla.html` — SLA matrix table (provider → consumer → service → target → escalation)
- [ ] Incident severity levels reference

---

## Sprint 6: DataOps + Incident Response
**Goal:** pages 08 and 11

**Tasks:**
- [ ] `pages/dataops.html` — CI/CD flow diagram (feature branch → prod)
- [ ] Monitoring section (what's monitored, where alerts go)
- [ ] Data Health dashboard mockup (table of marts × status)
- [ ] On-call section (rotation, runbook examples)
- [ ] Environments section (dev → staging → prod)
- [ ] `pages/incident-response.html` — severity levels
- [ ] Response protocol diagram
- [ ] Post-mortem template (filled example)
- [ ] Example incident narrative

---

## Sprint 7: MLOps + Data Lineage
**Goal:** pages 09 and 10

**Tasks:**
- [ ] `pages/mlops.html` — ML lifecycle diagram
- [ ] Experiment tracking section (MLflow example)
- [ ] Model registry section
- [ ] Feature Store section (Feast example)
- [ ] Monitoring section (drift detection)
- [ ] 3 model cards (LTV, Churn, Fraud)
- [ ] `pages/data-lineage.html` — NGR end-to-end lineage diagram (event → dashboard)
- [ ] Per-step annotations (tool, owner, DQ tests)
- [ ] Second example: churn prediction pipeline (shorter)

---

## Sprint 8: Dashboard Mockups
**Goal:** page 12 — 6 interactive mockups with fake data

**Tasks:**
- [ ] `pages/dashboards.html` — 6 dashboard mockups (HTML/CSS, fake data)
- [ ] CEO daily pulse: metric cards + sparklines + geo breakdown
- [ ] Marketing performance: funnel + CAC/LTV by channel + ROAS trend
- [ ] Casino product: GGR by provider + RTP scatter + top games
- [ ] Sports product: handle/margin by league + pre-match vs live
- [ ] Cohort analysis: retention heatmap + cumulative NGR curves
- [ ] Data health: mart status table + freshness timeline
- [ ] Per mockup: audience description, decisions it supports, source marts

---

## Sprint 9: A/B Testing + Management
**Goal:** pages 13 and 14

**Tasks:**
- [ ] `pages/ab-testing.html` — HADI cycle diagram
- [ ] Hypothesis backlog template (5-7 filled examples)
- [ ] Launch checklist (8 items)
- [ ] Report template
- [ ] Full test case with fake numbers (deposit form optimization)
- [ ] `pages/management.html` — sprint structure timeline
- [ ] Meeting cadence calendar grid
- [ ] 1-on-1 structure section
- [ ] OKR example
- [ ] Backlog management process
- [ ] Knowledge management / wiki structure

---

## Sprint 10: Onboarding + FinOps + Roadmap
**Goal:** pages 15, 16, 17 — final pages

**Tasks:**
- [ ] `pages/onboarding.html` — day 1-3, week 1, week 2, month 1 sections
- [ ] Interactive checklist (checkboxes)
- [ ] `pages/finops.html` — cost structure breakdown
- [ ] Optimization techniques section
- [ ] Budget planning example
- [ ] `pages/roadmap.html` — visual horizontal timeline (Q1-Q4)
- [ ] Milestones and dependencies per quarter

---

## Sprint 11: Polish
**Goal:** final QA, cross-linking, OG images

**Tasks:**
- [ ] Cross-link audit: every reference to another section is a working link
- [ ] Mobile QA: test all 18 pages on 375px viewport
- [ ] Navigation QA: sidebar, breadcrumbs, prev/next on every page
- [ ] Content QA: all SQL references use correct table names from data model
- [ ] OG image: create `assets/og-image.png` (1200x630)
- [ ] Per-page OG tags: unique title and description
- [ ] README.md for GitHub repo
- [ ] Final Lighthouse audit (target >95 per page)
- [ ] Deploy to GitHub Pages
