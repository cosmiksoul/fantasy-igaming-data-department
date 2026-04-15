# Sprint 11: Glossary + About — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 18 and 19 — Glossary (terms from all pages) and About (project story, author, resources, contributing).

## Deliverables

### `pages/glossary.html` (28KB)

**100+ терминов в 20 алфавитных accordion (A-W):**

| Letter | Terms | Count |
|--------|-------|-------|
| A | A/B Testing, Acquisition, Active Player, Adjust, Airbyte, Airflow, Analytics Engineer, Attribution, AUC | 9 |
| B | Batch, BI, BigQuery, Bonus Cost, Bonus Cost Ratio, Buddy | 6 |
| C | CAC, CDC, Census, Churn Rate, ClickHouse, Cohort Analysis, Confidence Interval, Conversion, CPA, CRM, Cross-validation | 11 |
| D | DAG, Data Catalog, Data Dictionary, Data Drift, Data Governance, Data Lake, Data Lineage, Data Mesh, Data Owner, Data Quality, Data Steward, DataHub, dbt, Debezium, DWH | 15 |
| E | ELT/ETL, ERD, Event Taxonomy | 3 |
| F | Feast, Feature Store, FinOps, FPR, FTD | 5 |
| G | GA4, GCS, GGR, Grafana, Great Expectations, GTM, Guardrail Metric | 7 |
| H | HADI Cycle, Hold %, Hypothesis | 3 |
| I | ICE/RICE, Incident | 2 |
| K | Kafka, KPI, KYC | 3 |
| L | Lakehouse, LightGBM, LTV, LTV:CAC | 4 |
| M | MAE, MAPE, Mart, Materialized View, MAU/DAU/WAU, MDE, Metabase, MLflow, MLOps, Model Drift, Model Registry | 11 |
| N | NGR | 1 |
| O | OKR, On-call, Overfitting | 3 |
| P | P-value, Parquet, Partitioning, Payback Period, PII, Post-mortem, Power, Precision, PSI | 9 |
| R | RACI, RBAC, Recall, Retention, Reverse ETL, ROAS, Row-level Security, RTP, Runbook | 9 |
| S | Sample Size, Semantic Layer, SLA, Snowflake, Staging, Statistical Significance | 6 |
| T | Taxonomy, Timeliness, Tracking Plan, TTL, Turnover, Type I/II Error | 6 |
| U | Unit Economics | 1 |
| W | Wagering, Whale | 2 |

Each term: name (English), definition (Russian, 1-2 sentences), link to source page.

---

### `pages/about.html` (10KB)

**О проекте:**
- Origin story (от первого лица, подготовка к собеседованию → идея проекта)
- Целевая аудитория (5 групп: data-лиды, аналитики, DE, кандидаты, CTO)
- Disclaimer

**Об авторе:**
- Author card с фото (circular PNG, 140×140)
- Константин Гупалов, Head of Analytics / Data Strategy Leader
- 12+ лет опыта, ключевые компании: SOFTSWISS, Parimatch, Admixer, EPAM, Wargaming
- Core strengths summary
- LinkedIn link

**Полезные материалы:**
- A/B Testing 101: The Anatomy of Evidence (PDF download)
- SQL 101: Рецепты продуктового аналитика (PDF download)

**Contributing (3 accordion):**
- GitHub Issues — предложения и баги
- Pull Requests — гайд для контрибуторов
- Обратная связь — LinkedIn

**Changelog:**
- v1.0 — Апрель 2026 (timeline block)

### Assets

- `assets/author.png` (61KB) — circular crop of me.jpg, 200×200, transparent background

### CSS additions (`css/style.css`)

New components:
- `.glossary-list`, `.glossary-list dt`, `.glossary-list dd` — definition list styling
- `.author-card`, `.author-card-photo`, `.author-card-info`, `.author-card-role`, `.author-card-links` — author bio card (responsive: column → row)
- `.resource-grid` — 1 → 2 column grid for resource cards

## Checklist

- [x] Glossary: 100+ terms from all project pages
- [x] Alphabetical order (A-Z), accordion per letter
- [x] Each term: name, definition (Russian), link to source page
- [x] About: project story (от первого лица)
- [x] Author card with photo + LinkedIn
- [x] Resources: 2 PDF books with download links
- [x] Contributing: Issues, PRs, contact (3 accordion)
- [x] Changelog (timeline block)
- [x] Author photo: circular PNG in assets/
- [x] Navigation works on both pages
- [x] Both pages < 100KB (28KB + 10KB)
- [x] No hardcoded colors
- [x] Content in Russian, code/classes in English
