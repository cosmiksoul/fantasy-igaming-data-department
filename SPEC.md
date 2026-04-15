# Fantasy iGaming LTD — Project Specification

## Overview

**Fantasy iGaming LTD** — open-source интерактивный справочник по аналитической функции вымышленной iGaming-компании. Мультистраничный static site на GitHub Pages. Каждая секция — отдельная HTML-страница. Чистый HTML/CSS/JS, без фреймворков.

Tone: не консалтинг, не учебник. Живой reference для data-комьюнити. Попсово, понятно, с оговоркой что это идеализированный стейт.

---

## Company Profile

- **Name:** Fantasy iGaming LTD
- **Product:** Sportsbook + Online Casino
- **Markets:** 3 geo — CIS (primary), LatAm (growing), Europe (new)
- **Scale:** ~300 employees, ~500K MAU, ~$5M NGR/month
- **Stage:** scale-up (past PMF, scaling)
- **Data team:** 20 people, 4 streams, 4 leads
- **Regulation:** Curaçao license + MGA application in progress

---

## File Structure

```
fantasy-igaming/
├── index.html                    # intro + section navigation
├── css/
│   └── style.css                 # shared styles, theme, components
├── js/
│   └── nav.js                    # shared navigation, burger menu, active state
├── pages/
│   ├── data-architecture.html    # 01
│   ├── org-structure.html        # 02
│   ├── data-model.html           # 03
│   ├── event-taxonomy.html       # 04
│   ├── metrics.html              # 05
│   ├── data-governance.html      # 06
│   ├── sla.html                  # 07
│   ├── dataops.html              # 08
│   ├── mlops.html                # 09
│   ├── data-lineage.html         # 10
│   ├── incident-response.html    # 11
│   ├── dashboards.html           # 12
│   ├── ab-testing.html           # 13
│   ├── management.html           # 14
│   ├── onboarding.html           # 15
│   ├── finops.html               # 16
│   └── roadmap.html              # 17
└── assets/
    └── og-image.png              # social preview
```

---

## Design System

### Theme (dark)
- Body bg: `#0e0e11`
- Card bg: `#16161c`
- Border: `#1e1e24`
- Text heading: `#f0eee6`
- Text body: `#c8c5be`
- Text secondary: `#8a8780`
- Text muted: `#5a5850`

### Typography
- Body: `DM Sans` (Google Fonts), 400/500/600
- Code: `JetBrains Mono` (Google Fonts), 400/500
- H1: 22px/600, H2: 18px/600, H3: 16px/500
- Body: 14px/400, line-height 1.6
- Small/captions: 12px, muted color

### Layout
- Mobile (<768px): single column, burger menu, min tap target 44px
- Tablet (768–1024px): sidebar collapses, 2-col grids where appropriate
- Desktop (>1024px): fixed sidebar 220px + content max-width 800px
- Border radius: 12px (cards), 8px (inner blocks), 20px (pills/badges)
- Borders: 1px solid `#1e1e24`

### Color Accents (by section category)
- Core sections: purple `#534AB7`, teal `#1D9E75`, blue `#378ADD`
- Operations: amber `#BA7517`, pink `#D4537E`, red `#E24B4A`, green `#639922`
- Advanced: coral `#D85A30`, gray `#888780`

### External Dependencies (CDN only)
- Google Fonts: DM Sans, JetBrains Mono
- mermaid.js (for ERD diagrams)
- No frameworks, no npm, no build tools

### Performance Target
- Each page < 100KB
- Lighthouse > 95

---

## Shared Components

### Navigation
- **Mobile:** burger icon → slide-out panel, sections grouped by category (Core / Operations / Practice / Advanced)
- **Desktop:** fixed left sidebar 220px, current section highlighted
- **Breadcrumbs:** Fantasy iGaming > Section Name (on every inner page)
- **Prev/Next:** bottom of every page — links to previous and next sections

### Reusable UI Components
- **Accordion** — collapsible sections (click to expand)
- **Tool card** — stack tool (name, description, alternative, trade-off)
- **Metric card** — metric (formula, SQL, benchmarks, pitfalls)
- **Person card** — role in org structure
- **SLA row** — matrix row
- **Timeline block** — roadmap element
- **Code block** — SQL/Python with syntax highlighting (CSS-only, no lib)
- **Mermaid block** — ERD and flowcharts (mermaid.js)
- **Alert box** — tip (green border-left) / warning (amber) / info (blue)

### Footer
- GitHub repo link
- Author credit
- Disclaimer
- License (CC BY 4.0)

---

## Page Specifications

### 00. Index (`index.html`)

**Hero:**
- Title: Fantasy iGaming LTD
- Subtitle: The Ultimate Data Function Reference
- Description: 2-3 sentences about the project
- CTA button → first section (data-architecture)

**Company card:**
- Compact card with key parameters: product, markets, MAU, NGR, team size, stack summary

**Section grid:**
- Cards in grid (2 col desktop, 1 col mobile)
- Each card: number + title + 1-line description + category color accent
- Click → navigate to page

**Disclaimer:**
- "All data is fictional. Not best practice, not consulting. Starting point for discussion."

---

### 01. Data Architecture (`pages/data-architecture.html`)

Interactive stack diagram by layers. Each layer expands to show tools.

**Per layer content:**

**Sources:** PostgreSQL (production DB — accounts, bets, transactions, balances; never query directly for analytics), Kafka (real-time events — bets placed, deposits, sessions; millions of msgs/sec; multiple consumers), GA4+GTM (web analytics, marketing attribution), Adjust (mobile SDK — installs, attribution, in-app events), CRM (player lifecycle — segmentation, bonuses, comms), External APIs (odds feeds, match results, payment providers). Per source: 2-3 sentences what data comes from it.

**Ingestion:** Airbyte (primary, self-hosted; 300+ connectors; cheaper than Fivetran but needs DE support) + Debezium/CDC (real-time change capture from production PostgreSQL via Kafka Connect; captures deltas, minimal prod load). Alternative: Fivetran (managed, more expensive, less control). Trade-off explained.

**Storage:** ClickHouse (primary — columnar, fast aggregations, popular in CIS/iGaming; self-hosted = data control, needs DE team) + GCS data lake (cold/raw data, Parquet format, cheap). Alternatives: BigQuery (serverless, expensive at scale without partitioning), Snowflake (western standard, compute/storage separation). Trade-off: ClickHouse faster and cheaper but requires ops.

**Transformation:** dbt Core. Three layers with examples: staging (1:1 with source, type casting, dedup) → intermediate (business logic, joins, calculations) → marts (BI/DS-ready). Example chain: stg_bets → int_bets_enriched → mart_daily_kpi. Alternative: Spark (heavy batch jobs). Include 1 simplified SQL model example per layer (10-15 lines).

**Orchestration:** Apache Airflow. Example DAG: extract → load → dbt run → dbt test → alert. Explanation: why not cron (dependencies, retry, UI, alerting). Alternatives: Dagster, Prefect.

**DQ & Governance:** dbt tests (first line) + Great Expectations (complex validations) + DataHub (catalog). Cross-ref to section 06.

**BI:** Metabase (primary, self-service, open-source) + Looker Studio (marketing, free). Alternatives: Tableau (powerful, expensive), Power BI (MS stack), Looker (semantic layer). Cross-ref to section 12.

**ML:** Python/Jupyter (dev) + MLflow (lifecycle) + Feast (feature store). Cross-ref to section 09.

**Reverse ETL:** Census (DWH → CRM, ad platforms). Use case: churn score → CRM segment → personalized bonus.

**Tool card format:** Name → What it does (1-2 sentences) → Why chosen (1 sentence) → Alternative and why not (1 sentence) → Key trade-off.

---

### 02. Org Structure (`pages/org-structure.html`)

**Visual org chart:** Director → 4 leads → teams. Clickable — each node expands details.

**4 streams detail:**

**Data Engineering (5 people):**
- Lead DE + 2 Data Engineers (pipelines, DWH) + 1 Analytics Engineer (dbt models, DQ) + 1 Platform/DevOps (Airflow, ClickHouse, monitoring)
- Responsibility: ingestion, DWH, infrastructure, pipeline-level DQ, on-call
- Interacts with: Backend (data access), DevOps (infra), Analytics (mart requirements)
- Key deliverables: pipelines 24/7, data fresh by 7:00, SLA uptime 99.5%

**Analytics (8 people):**
- Lead Analyst + 3 Product Analysts (sports, casino, payments) + 2 Marketing Analysts (acquisition, retention/CRM) + 1 Financial Analyst (P&L, unit economics) + 1 BI Developer (dashboards, semantic layer)
- Responsibility: reporting, research, ad-hoc, cohort analysis, funnels
- Interacts with: Product, Marketing, Finance, C-level
- Key deliverables: dashboards, weekly/monthly reports, ad-hoc in 3 days, research in 2 weeks

**Data Science (4 people):**
- Lead DS + 1 ML Engineer (model deployment, MLOps) + 1 DS (LTV, churn, recommendations) + 1 DS (fraud detection, risk scoring, anomaly detection)
- Responsibility: predictive models, A/B testing (methodology + analysis), experimentation platform
- Interacts with: Product (use cases), DE (data, feature store), Risk/Compliance (fraud)
- Key deliverables: models in prod, A/B reports, fraud scoring

**BI Engineering (3 people):**
- Lead BI + 1 BI Developer (Metabase, complex dashboards) + 1 Data Literacy Specialist (training, self-service, documentation)
- Responsibility: semantic layer, reporting standardization, self-service tools, data literacy program
- Interacts with: all business functions (dashboard end users)
- Key deliverables: self-service coverage, training, standardized templates

**Additional content:**
- RACI matrix for key processes (new dashboard, new pipeline, new model, incident)
- Skill matrix: roles × skills (SQL, Python, dbt, BI, statistics, ML, communication, domain). Levels: basic / proficient / expert
- Career ladder: Junior → Middle → Senior → Lead → Head/Director. Expectations per level.

---

### 03. Data Model (`pages/data-model.html`)

**ERD diagram:** mermaid.js erDiagram with relationships. Clickable — click table → field descriptions.

**Core entities:**

```
dim_players (player_id PK, registered_at, geo, acquisition_channel, acquisition_campaign, device, platform, kyc_status, kyc_verified_at, vip_tier, segment, is_self_excluded, created_at, updated_at)

dim_games (game_id PK, provider, game_name, game_type [slot/table/live/crash], rtp_theoretical, category, is_active)

dim_sports_events (event_id PK, sport, league, home_team, away_team, start_time, status [pre/live/settled], result)

fct_bets (bet_id PK, player_id FK, product [casino/sports], game_id/event_id FK, bet_amount, payout_amount, bet_type [single/combo/system], odds, placed_at, settled_at, status [open/won/lost/void], is_bonus_bet, bonus_id FK)

fct_deposits (deposit_id PK, player_id FK, amount, currency, payment_method, status [pending/completed/failed], is_first_deposit, fee_amount, created_at)

fct_withdrawals (withdrawal_id PK, player_id FK, amount, currency, payment_method, status [pending/approved/rejected/completed], processing_time_hours, created_at)

fct_sessions (session_id PK, player_id FK, started_at, ended_at, duration_sec, platform [web/ios/android], device_type, pages_viewed, geo_ip)

fct_bonuses (bonus_id PK, player_id FK, bonus_type [welcome/reload/cashback/freebet/freespin], amount, wagering_requirement, wagered_amount, status [active/completed/expired/cancelled], issued_at, expires_at)

fct_events_raw (event_id PK, player_id FK, event_name, event_params JSON, timestamp, session_id FK, platform)
```

**dbt layers with examples:**
- Staging (stg_): 1:1 with source, cleaning. Example: stg_betting__bets — simplified SQL (10-15 lines)
- Intermediate (int_): business logic, joins. Example: int_bets_enriched — join bet + player + game
- Marts (mart_): final business views. Examples: mart_daily_kpi, mart_player_lifetime, mart_cohort_analysis, mart_marketing_performance

Per mart: list of fields, source intermediate models, refresh frequency.

---

### 04. Event Taxonomy (`pages/event-taxonomy.html`)

**Naming convention:** `{domain}_{object}_{action}`
- Domains: player, session, marketing, system
- Objects: bet, deposit, withdrawal, bonus, session, page, registration, kyc
- Actions: placed, completed, started, viewed, settled, issued, expired

**Event schema (standard structure):**
- Required: event_name, event_id (UUID), player_id, timestamp (ISO 8601), session_id, platform (web/ios/android)
- Context (auto-collected): geo_ip, device_type, app_version, page_url
- Event-specific: varies (amount, game_id, method, etc.)

**Example JSON payloads:** full structure for player_bet_placed, player_deposit_completed, session_page_viewed, player_registration_completed

**Tracking plan table:** event_name | trigger (when fires) | parameters (list) | source (frontend/backend/server) | owner (team) | status (live/planned/deprecated). 10-15 key events filled in.

**Change process:** how to add new event: request → review (analytics + DE) → spec → implementation → QA → deploy. Who approves, how versioned.

---

### 05. Metrics Dictionary (`pages/metrics.html`)

**Source:** CSV with 50+ metrics. MVP: 15-20 key metrics (L1 Must). Link to full catalog.

**Metric groups:**
- Revenue (5): Turnover/Handle, GGR, GGR Margin, NGR, NGR Margin
- Unit Economics (4): LTV, LTV:CAC, CAC, Payback Period
- Players (4): Active Players (DAU/WAU/MAU), FTD Count, Retention D1/D7/D30, Churn Rate
- Marketing (3): CPA/CPD, ROAS, Conversion funnel (Visit→Reg→FTD)
- Product (2): Revenue Concentration, Bonus Cost Ratio

**Metric card format:**
- Name + category badge
- Definition: 1-2 sentences, plain language
- Formula: numerator / denominator
- SQL example: 5-10 lines, querying mart tables
- Benchmarks: EU / LatAm / SEA (from CSV)
- Alert thresholds: red / yellow (from CSV)
- Owner: Product / Marketing / Finance
- Pitfalls: 2-3 common interpretation errors (from CSV)
- Dependencies: which other metrics it depends on
- Dimensions: geo, channel, product, segment

---

### 06. Data Governance (`pages/data-governance.html`)

**Roles:**
- Data Owners by domain: Head of Product (betting), CFO (finance), CMO (marketing), Head of Compliance (player PII). Per owner: what they "own", what decisions they make.
- Data Stewards: assigned analyst/DE per domain. Example: mart_daily_kpi steward — who, what they check.
- Governance Council: composition, cadence (quarterly), typical agenda, example decision.

**Data Catalog (DataHub):** example table card — name, description, owner, steward, freshness, lineage, tags, popularity.

**Data Dictionary:** standardized definitions. Active Player = placed bet in last 30 days. FTD = first-time depositor. Process: how to propose definition change, who approves.

**Access policies (RBAC):** matrix: Analyst / DS / BI Dev / Lead / Director × data domains (betting, finance, player PII, marketing). Row-level security example.

**DQ framework:** 5 dimensions with test example each:
- Completeness: "% NULL in payment_method < 1%"
- Accuracy: "actual RTP vs theoretical ±2pp"
- Timeliness: "mart updated by 7:00 UTC"
- Consistency: "sum(fct_bets.amount) = mart_daily_kpi.turnover ±0.01%"
- Uniqueness: "0 duplicates on bet_id"

**Data lifecycle:** retention policy. Hot (3 months, ClickHouse) → warm (1 year, ClickHouse cold storage) → cold (5 years, GCS Parquet). Regulatory: betting data 5+ years.

---

### 07. SLA (`pages/sla.html`)

Matrix table: Provider → Consumer → Service → SLA metric → Target → Measurement → Escalation

- DE → Analytics: data in DWH by 7:00 UTC | completeness >99.5% | critical mart downtime <2h/month
- DE → DS: feature store updated by 8:00 | training data available within 24h of request
- Analytics → Business: ad-hoc 3 business days | research 2 weeks | new dashboard 1 sprint
- DS → Product: new model task-to-MVP 4-6 weeks | retraining monthly | fraud scoring latency <100ms
- BI → All: critical dashboards uptime 99.5% | load time <5 sec | data update ≤1h after DWH
- Incident response: P1 acknowledge 30 min / fix 4h | P2 acknowledge 2h / fix 24h | P3 acknowledge 1 day / fix 1 sprint

How measured, where tracked, what happens on SLA breach.

---

### 08. DataOps (`pages/dataops.html`)

**CI/CD for data:** visual flow: feature branch → PR → dbt compile + test (CI) → code review → merge → dbt run (CD) → monitoring. Git-flow: main (prod), develop (staging), feature branches.

**Monitoring:** what's monitored (freshness, volume, schema changes, query performance, cost). Alerts go to Slack #data-alerts. Example Data Health dashboard: table of marts × status (green/yellow/red).

**On-call:** DE rotation (1 week). Runbook: typical incidents and how to fix. Example: "Airflow DAG failed → check logs → retry → if not fixed → escalate to Lead DE".

**Environments:** dev (local dbt) → staging (prod copy, data subset) → prod. How to promote changes.

---

### 09. MLOps (`pages/mlops.html`)

**ML lifecycle:** visual diagram — Problem framing → Data prep → Training → Validation → Deploy → Monitor → Retrain

**Experiment tracking (MLflow):** example record: experiment name, run parameters, metrics (AUC, MAE), artifacts. Mockup of UI.

**Model registry:** versions: v1.0 (staging) → v1.1 (prod) → v0.9 (archived). Process: DS commits → Lead DS reviews → ML Engineer deploys.

**Feature Store (Feast):** example feature: player_avg_bet_7d. Source, update frequency, consumers.

**Monitoring:** model drift (PSI), data drift (input feature distributions), prod metrics vs baseline.

**Model cards (3):**
1. LTV Prediction: task, target, features (top 10), algorithm (LightGBM), metrics (MAE, MAPE), retraining (monthly), SLA
2. Churn Prediction: similar, recall vs precision trade-off
3. Fraud Detection: real-time scoring, latency SLA <100ms, false positive rate

---

### 10. Data Lineage (`pages/data-lineage.html`)

**Full end-to-end example: how NGR is calculated**

Betting Engine (bet placed) → Kafka → Airbyte → ClickHouse raw → stg_bets → int_bets_enriched (join players, games) → int_daily_ggr (sum bets - sum payouts) → mart_daily_kpi (GGR - bonus_cost - provider_fees - payment_fees = NGR) → Metabase dashboard (CEO daily pulse)

Visual flowchart. Per step: what happens to data, which tool, who owns, which DQ tests.

**Second example (shorter): churn prediction pipeline**

fct_bets + fct_deposits + fct_sessions → Feature Store (player features) → ML model (LightGBM) → churn_score → Census → CRM → personalized bonus

---

### 11. Incident Response (`pages/incident-response.html`)

**Severity levels:** P1 (critical mart/pipeline down, CEO report broken, fraud scoring offline) → P2 (non-critical dashboard stale, DQ test failed on non-critical field) → P3 (minor DQ issue, documentation outdated)

**Response protocol:** visual flow: Detect (alert) → Acknowledge (assign owner, ETA) → Diagnose (root cause) → Fix → Communicate (stakeholders) → Post-mortem

**Post-mortem template:** filled example. Title, Date, Severity, Duration, Impact, Timeline (minute-by-minute), Root cause, What went well, What went wrong, Action items (with owner and deadline)

**Example incident:** "Monday 7:30. mart_daily_kpi not updated. CEO writes: weekend numbers look wrong. Root cause: Airflow worker OOM due to data spike after Champions League final. Fix: increased memory limit, added partitioning. Preventive: OOM alert, autoscaling."

---

### 12. Dashboard Mockups (`pages/dashboards.html`)

6 mockups (HTML/SVG with fake data):

1. **CEO daily pulse:** 4 metric cards (NGR, GGR, Active Players, Deposits) + sparklines WoW + geo breakdown + alert indicators
2. **Marketing performance:** funnel Visit→Reg→FTD (conversion rates), CAC and LTV:CAC by channel, ROAS trend, top-5 campaigns
3. **Casino product:** GGR by provider (bar chart), RTP actual vs theoretical (scatter), top-10 games by GGR, retention by game type
4. **Sports product:** Handle and margin by league, pre-match vs live split, upcoming events, margin trend
5. **Cohort analysis:** retention heatmap (cohort × day), cumulative NGR curves, LTV by cohort and channel
6. **Data health:** mart table × status (green/yellow/red), freshness timeline, DQ score trend, open incidents

Per mockup: audience, what decisions it supports, which mart tables feed it.

---

### 13. A/B Testing Framework (`pages/ab-testing.html`)

**HADI cycle:** visual: Hypothesis → Action → Data → Insight → (loop). Each step explained.

**Hypothesis backlog:** template table: ID, hypothesis (format: "if [change], then [metric] [direction] by [MDE], because [rationale]"), primary metric, MDE, ICE score, status (backlog/running/done), owner. 5-7 filled iGaming examples.

**Launch checklist:** 8 items — hypothesis, metrics (primary/secondary/guardrail), sample size calc, randomization, duration, stakeholder sign-off, no-peek commitment, rollback plan.

**Report template:** hypothesis → setup (sample size, duration, split) → result (CI, p-value, effect size) → segmentation → recommendation (roll out / iterate / kill) → learnings.

**Full case:** deposit form simplification test. Hypothesis → calculation → launch → result → decision. With concrete (fake) numbers.

---

### 14. Management Practices (`pages/management.html`)

**Sprint structure:** 2-week sprints. Visual timeline: Planning (Mon, 1h) → Daily standups (15 min) → Mid-sprint check → Review (Fri week 2, 1h) → Retro (30 min). 70% roadmap / 30% ad-hoc buffer.

**Meeting cadence:** visual calendar grid. Director ↔ Leads: weekly 1-on-1 (30 min). Director ↔ C-level: bi-weekly. All-hands data: monthly. Governance Council: quarterly. Cross-functional (Product/Marketing/Finance): weekly.

**1-on-1 with lead:** structure: People → Process → Strategy. 30 min, lead sets agenda.

**OKR framework:** quarterly OKR example. Objective: "Enable data-driven decision making". KR1: 100% critical marts with SLA. KR2: 80% ad-hoc via self-service. KR3: LTV model in prod with MAPE <20%.

**Backlog management:** how requests arrive (Jira/Linear form), prioritization (RICE), status communication (Slack bot + weekly digest).

**Knowledge management:** wiki structure — Architecture, Metrics, Processes, Runbooks, Onboarding. Rule: "if you explained in Slack — write in wiki".

---

### 15. Onboarding Guide (`pages/onboarding.html`)

**Day 1-3:** access (DWH, BI, Git, Slack, Jira), buddy assigned, meet team, read Data Dictionary and Event Taxonomy.

**Week 1:** "Data tour" — follow event-to-dashboard path (Lineage section). Architecture review (section 01). First SELECT to DWH.

**Week 2:** first ad-hoc under buddy supervision. First dbt PR — add test or fix model. Code review from lead.

**Month 1:** independent ad-hoc, first dashboard/research, participate in sprint planning and retro. Feedback session with lead.

**Interactive checklist:** checkboxes — what read, what accessed, what tasks completed.

---

### 16. FinOps / Cost Model (`pages/finops.html`)

**Cost structure:** infrastructure (ClickHouse cluster, GCS, Airflow, Kafka — approximate $/month) + SaaS (Metabase, DataHub, Airbyte, MLflow — self-hosted vs managed trade-offs) + people (20 FTE × avg salary ranges)

**Optimization:** partitioning, materialized views, TTL policies, reserved instances, query optimization tips.

**Budget planning:** example annual budget: payroll, infrastructure, software, training, conferences. How to defend before CFO.

---

### 17. Annual Roadmap (`pages/roadmap.html`)

Visual horizontal timeline (4 quarters) with milestones and dependencies.

- **Q1 — Stabilize:** DQ framework live, SLA defined, Data Dictionary v1, governance roles assigned, on-call rotation launched
- **Q2 — Self-service:** semantic layer, Metabase rollout, data literacy workshops (3 sessions), 80% ad-hoc via self-service
- **Q3 — ML to prod:** LTV model deployed, churn prediction MVP, A/B testing framework operational, Feature Store live
- **Q4 — Scale:** real-time analytics (streaming marts), Reverse ETL → CRM, fraud model v2, platform cost optimization (-20%)
