# Sprint 1: Data Architecture — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Page 01 — full stack diagram with tool cards.

## Deliverables

### `pages/data-architecture.html` (32KB)

Interactive stack diagram: 9 layers, each is an accordion that expands to show tool cards.

**Layers and tools:**

| # | Layer | Tools | Cards |
|---|-------|-------|-------|
| 1 | Sources | PostgreSQL, Kafka, GA4+GTM, Adjust, CRM, External APIs | 6 |
| 2 | Ingestion | Airbyte, Debezium/CDC | 2 |
| 3 | Storage | ClickHouse, GCS Data Lake | 2 |
| 4 | Transformation | dbt Core (+ 3 SQL examples: staging, intermediate, marts) | 1 |
| 5 | Orchestration | Apache Airflow (+ DAG example) | 1 |
| 6 | DQ & Governance | dbt tests, Great Expectations, DataHub | 3 |
| 7 | BI & Reporting | Metabase, Looker Studio | 2 |
| 8 | ML Platform | Python/Jupyter, MLflow, Feast | 3 |
| 9 | Reverse ETL | Census (+ use case: churn → CRM → bonus) | 1 |

**Total:** 9 accordions, 21 tool cards, 3 SQL code blocks, 1 Python code block.

**Each tool card includes:**
- Name + category badge
- Description (1-2 sentences, iGaming context)
- Alternative (with reasoning)
- Key trade-off

**Cross-links to related pages:**
- DQ & Governance → 06. Data Governance
- BI & Reporting → 12. Dashboards
- ML Platform → 09. MLOps

**Additional elements:**
- Info alert at top (instruction to click layers)
- Tip alert in Reverse ETL (use case example)
- SQL examples use correct table names: `stg_betting__bets`, `int_bets_enriched`, `mart_daily_kpi`

## Checklist

- [x] 9 accordion layers
- [x] 21 tool cards with descriptions, alternatives, trade-offs
- [x] 3 SQL examples (one per dbt layer: staging, intermediate, marts)
- [x] Cross-links to pages 06, 09, 12
- [x] Navigation works (sidebar, breadcrumbs, prev/next)
- [x] All accordions expand/collapse
- [x] No hardcoded colors
- [x] Page size 32KB (< 100KB target)
- [x] Content in Russian, code/classes in English
