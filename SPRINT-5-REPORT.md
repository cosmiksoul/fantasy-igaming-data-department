# Sprint 5: Data Governance + SLA — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 06 and 07 — Data Governance (roles, catalog, dictionary, RBAC, DQ, lifecycle) and SLA (matrix, severity levels, tracking).

## Deliverables

### `pages/data-governance.html` (23KB)

**Roles & Ownership:**
- 4 Data Owners (Head of Product, CFO, CMO, Head of Compliance) with domains and decision rights
- Data Steward example: Financial Analyst as steward for mart_daily_kpi
- Governance Council: composition, quarterly cadence, example decision (Churn Rate definition change)

**Data Catalog (DataHub):**
- Example table card: mart_daily_kpi with description, owner, steward, freshness, lineage, tags, popularity, DQ score

**Data Dictionary:**
- 7 standardized definitions (Active Player, FTD, GGR, NGR, Churn, Whale, Bonus Cost)
- Change process: 3-step timeline (Proposal → Review → Approve & Update)

**RBAC Matrix:**
- 5 roles × 4 data domains with access levels (read / masked / no / full)
- Row-level security SQL example
- PII masking explanation

**DQ Framework (5 accordions):**
- Completeness: NULL rate test (dbt YAML)
- Accuracy: RTP deviation check (SQL)
- Timeliness: staleness monitoring (SQL)
- Consistency: cross-table sum validation (SQL)
- Uniqueness: PK dedup test (dbt YAML)

**Data Lifecycle (timeline):**
- Hot (3 months, ClickHouse SSD) → Warm (1 year, ClickHouse HDD) → Cold (5+ years, GCS Parquet)
- PII retention warning (GDPR 30-day deletion)

**Cross-links:** Data Architecture (01)

---

### `pages/sla.html` (11KB)

**SLA Matrix (5 provider-consumer groups, 6 tables):**

| Provider → Consumer | SLA Items |
|---------------------|-----------|
| DE → Analytics | freshness by 07:00, completeness >99.5%, downtime <2h/mo |
| DE → DS | Feature Store by 08:00, training data within 24h |
| Analytics → Business | ad-hoc 3 days, research 2 weeks, dashboard 1 sprint |
| DS → Product | model MVP 4-6 weeks, monthly retraining, fraud <100ms |
| BI → All | uptime 99.5%, load <5s, data lag ≤1h |

Each row: service, SLA metric, target, measurement tool, escalation path.

**Incident Severity Levels:**
- P1 Critical: acknowledge 30 min, fix 4h
- P2 High: acknowledge 2h, fix 24h
- P3 Medium: acknowledge 1 day, fix 1 sprint

**Tracking & Breach Protocol:**
- Tools: Grafana, Airflow SLA alerts, Jira, Slack #data-alerts
- 5-step breach response process

**Cross-links:** Incident Response (11)

## Checklist

- [x] Data Owners table (4 domains)
- [x] Data Steward example
- [x] Governance Council section
- [x] DataHub catalog card example
- [x] Data Dictionary (7 terms + change process)
- [x] RBAC matrix (5 roles × 4 domains) + RLS example
- [x] DQ framework (5 dimensions with test examples)
- [x] Data lifecycle (3-tier retention + GDPR)
- [x] SLA matrix (5 groups, 14 SLA items)
- [x] Incident severity levels (P1/P2/P3)
- [x] Measurement and breach protocol
- [x] Navigation works on both pages
- [x] Both pages < 100KB (23KB + 11KB)
