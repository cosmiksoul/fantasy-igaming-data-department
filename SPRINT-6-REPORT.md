# Sprint 6: DataOps + Incident Response — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 08 and 11 — DataOps (CI/CD, monitoring, on-call, environments) and Incident Response (severity, protocol, post-mortem).

## Deliverables

### `pages/dataops.html` (14KB)

**CI/CD for Data (6-step timeline):**
- Feature Branch → PR (dbt compile + test CI) → Code Review → Merge to staging → Release to prod → Monitoring
- Git-flow diagram: main / develop / feature branches

**Monitoring (table + Data Health dashboard):**
- 6 monitoring areas: freshness, volume, schema, query perf, cost, DQ tests
- Data Health mockup: 5 marts × status (OK/WARN/ALERT) with freshness and DQ score

**On-call (4 runbook accordions):**
- Airflow DAG failed
- ClickHouse query timeout
- Source data delayed/missing
- DQ test failure in production
- Each: step-by-step troubleshooting guide

**Environments (table):**
- dev (local, subset data) → staging (full copy, auto-deploy) → prod (Airflow only)
- Promote rule: no changes to prod without staging

---

### `pages/incident-response.html` (13KB)

**Severity Levels:**
- P1 Critical: 30min ack / 4h fix / post-mortem required
- P2 High: 2h ack / 24h fix / post-mortem required
- P3 Medium: 1 day ack / 1 sprint fix / optional

**Response Protocol (6-step timeline):**
- Detect → Acknowledge → Diagnose → Fix → Communicate → Post-mortem

**Post-mortem — filled example:**
- Champions League final incident (mart_daily_kpi OOM failure)
- Full timeline: 05:00 DAG start → 05:47 first OOM → 07:00 SLA alert → 07:12 ack → 09:15 resolved
- Root cause: worker memory 4GB insufficient for 3.2x data spike
- What went well (4 items), what went wrong (4 items)
- Action items table (5 actions with owners and deadlines)

## Checklist

- [x] CI/CD flow (6-step timeline + git-flow diagram)
- [x] Monitoring table (6 areas) + Data Health dashboard mockup
- [x] On-call: 4 runbook accordions
- [x] Environments table (dev/staging/prod)
- [x] Severity levels (P1/P2/P3)
- [x] Response protocol (6-step timeline)
- [x] Post-mortem template with filled Champions League example
- [x] Navigation works on both pages
- [x] Both pages < 100KB (14KB + 13KB)
