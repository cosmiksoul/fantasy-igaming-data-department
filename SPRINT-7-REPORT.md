# Sprint 7: MLOps + Data Lineage — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 09 and 10 — MLOps (lifecycle, MLflow, Feature Store, monitoring, model cards) and Data Lineage (NGR end-to-end, churn pipeline).

## Deliverables

### `pages/mlops.html` (21KB)

**ML Lifecycle (7-step timeline):**
- Постановка задачи → Подготовка данных → Обучение → Валидация → Деплой → Мониторинг → Переобучение

**Experiment Tracking (MLflow):**
- Пример записи: ltv_prediction_v3, LightGBM, 47 фичей, MAE: $42.3

**Model Registry:**
- Таблица версий: 5 записей (3 модели × стадии staging/production/archived)
- Процесс промоушена: DS → Lead DS review → ML Engineer deploy → staging → production

**Feature Store (Feast):**
- Пример фичи: player_avg_bet_7d (описание, entity, источник, обновление, потребители)
- Код: Python пример получения фичей через Feast API

**Мониторинг моделей (таблица):**
- Model drift (PSI), Data drift (KS-test), бизнес-метрики vs baseline
- Пороги алертов и действия при деградации

**Model Cards (3 accordion):**

| Модель | Задача | Алгоритм | Ключевая метрика | Режим |
|--------|--------|----------|------------------|-------|
| LTV Prediction | Прогноз lifetime NGR 12 мес | LightGBM | MAE: $42.3 | batch daily |
| Churn Prediction | Вероятность ухода 30 дней | LightGBM | AUC: 0.84 | batch daily |
| Fraud Detection | Real-time фрод-скоринг | LightGBM + rules | AUC: 0.91, FPR: 3.2% | real-time <100ms |

Каждая карточка: задача, целевая переменная, алгоритм, метрики, переобучение, SLA, топ фичи (LTV), trade-off precision/recall (Churn), архитектура real-time (Fraud).

**Cross-links:** Data Architecture (01)

---

### `pages/data-lineage.html` (15KB)

**Пример 1: NGR lineage (mermaid flowchart + 6 accordion):**
- Betting Engine → Kafka → Airbyte → ClickHouse raw → stg → int → mart → Metabase
- Каждый шаг: что происходит, инструмент, владелец, DQ-проверки

**Пример 2: Churn prediction pipeline (mermaid flowchart + таблица):**
- fct_bets/deposits/sessions → Feature Store → ML model → churn_score → Census → CRM → бонус
- 5 этапов с инструментами и владельцами
- Замкнутый цикл: данные → модель → действие → результат → данные

**Mermaid diagrams:** 2 flowcharts с цветовым кодированием (source=purple, ML=pink, output=green)

**Cross-links:** Data Architecture (01)

## Checklist

- [x] ML lifecycle (7-step timeline)
- [x] MLflow experiment tracking (пример записи)
- [x] Model Registry (таблица версий + процесс)
- [x] Feature Store (пример фичи + Python код)
- [x] Мониторинг (drift detection таблица)
- [x] 3 model cards (LTV, Churn, Fraud)
- [x] NGR lineage (mermaid flowchart + 6 step-by-step accordion)
- [x] Churn pipeline (mermaid flowchart + таблица)
- [x] Весь narrative-текст на русском
- [x] Navigation works on both pages
- [x] Both pages < 100KB (21KB + 15KB)
