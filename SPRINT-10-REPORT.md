# Sprint 10: Onboarding + FinOps + Roadmap — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 15, 16, 17 — Onboarding guide, FinOps cost model, Annual Roadmap.

## Deliverables

### `pages/onboarding.html` (15KB)

**День 1–3: Доступы и знакомство (4 accordion):**
- Доступы: таблица 8 систем (ClickHouse, Metabase, GitHub, Airflow, Slack, Jira, Confluence, DataHub)
- Buddy: роль, обязанности, что делает / не делает (таблица)
- Знакомство с командой: расписание Day 1–2 (Director, лиды, standup)
- Обязательное чтение: ссылки на Metrics Dictionary, Event Taxonomy, Data Governance

**Неделя 1: Data Tour (3 accordion):**
- Data Tour: 5-step timeline (от события до дашборда) с кросс-ссылками
- Архитектурный обзор с buddy
- Первый SELECT: SQL пример к mart_daily_kpi

**Неделя 2: Первые задачи (3 accordion):**
- Первый ad-hoc под buddy (примеры задач)
- Первый dbt PR: пример YAML-теста, процесс branch → PR → merge
- Compliance-тренинг: Data Privacy, Responsible Gambling, InfoSec

**Месяц 1: Самостоятельная работа (3 accordion):**
- Ожидания по ролям: таблица DE / Analyst / DS / BI (с badge по стримам)
- Участие в процессах: sprint planning, review, retro, standup
- Feedback-сессия с лидом: структура 45-минутной встречи

**Onboarding Checklist:**
- 16 checkbox items с localStorage persistence
- Progress counter (X / 16, NN%)
- Grouped by phase (Day 1–3, Week 1, Week 2, Month 1)

### `pages/finops.html` (16KB)

**Структура затрат (3 accordion + summary card):**
- Инфраструктура ~$18K/мес: таблица 6 компонентов (ClickHouse, Kafka, Airflow, GCS, K8s, Monitoring)
- SaaS ~$7K/мес: таблица 12 инструментов (8 self-hosted open-source, 4 paid)
- Люди ~$140K/мес: таблица 5 уровней (Director → Junior), 20 FTE
- Summary: общий бюджет $165K/мес, 3.3% от NGR

**Оптимизация (4 accordion):**
- ClickHouse: партиционирование (CREATE TABLE пример) + TTL (ALTER TABLE пример)
- Materialized Views: пример mv_daily_ggr
- Query Optimization: top-3 проблем с решениями (таблица)
- Reserved Instances & Spot: таблица workloads × тип × экономия

**Бюджетное планирование (3 accordion):**
- Годовой бюджет 2026: таблица 5 статей ($2.025M total)
- Защита перед CFO: ROI framework, метрики для CFO
- Квартальный cost review: чеклист из 4 пунктов

### `pages/roadmap.html` (16KB)

**Visual Timeline:**
- 4 квартала в grid (1 col mobile → 2 col tablet → 4 col desktop)
- Milestone status: done (teal dot), in-progress (amber), planned (gray outline)
- Q1: 5 milestones (all done), Q2: 5 (3 in-progress, 2 planned), Q3: 5 (all planned), Q4: 5 (all planned)

**Quarterly Details (4 sections, each with 2-3 accordion):**
- Q1 Stabilize: DQ Framework, SLA & On-call, Governance & Dictionary
- Q2 Self-service: Semantic Layer & Metabase, Data Literacy Program (3 workshops)
- Q3 ML to Prod: Models table (LTV, Churn, A/B), Feature Store & MLOps
- Q4 Scale: Real-time Analytics (4 metrics), Reverse ETL closed loop, Cost Optimization, Data Mesh Evaluation

**Dependencies table:**
- 8 deliverables with dependency chains (Q1 → Q2 → Q3 → Q4)
- Risk callout: Feature Store delay cascades

### CSS additions (`css/style.css`)

New components:
- `.checklist-item` — checkbox label with line-through on checked
- `.checklist-progress` — progress counter styling
- `.roadmap-timeline` — responsive grid (1 → 2 → 4 col)
- `.roadmap-quarter`, `.roadmap-q1/q2/q3/q4` — quarter cards with colored top border
- `.roadmap-milestone`, `.done/.in-progress/.planned` — milestone dots with status colors

## Checklist

- [x] Onboarding: Day 1-3, Week 1, Week 2, Month 1 sections (13 accordions)
- [x] Interactive checklist (16 items with localStorage)
- [x] FinOps: cost structure (infra + SaaS + people, summary card)
- [x] Optimization techniques (4 accordion with SQL examples)
- [x] Budget planning (annual budget, CFO framework, quarterly review)
- [x] Roadmap: visual timeline (4 quarters, 20 milestones)
- [x] Quarterly detail sections with deliverables and owners
- [x] Dependencies table with risk callout
- [x] Cross-links to related pages on all 3 pages
- [x] Navigation works (sidebar, breadcrumbs, prev/next)
- [x] All pages < 100KB (15KB + 16KB + 16KB)
- [x] No hardcoded colors — all from CSS variables
- [x] Content in Russian, code/classes in English
