# Content Review — Fantasy iGaming Data Department

**Date:** 2026-04-15
**Scope:** All 19 pages + index

---

## Overall Assessment

Сайт впечатляюще проработан. Контент genuinely iGaming-специфичный, числа реалистичны для заявленного масштаба компании, русский текст естественный и профессиональный, кросс-ссылки консистентны. Ниже — конкретные находки, отсортированные по severity.

---

## Critical (ломает достоверность)

### 1. DAU на CEO Dashboard нереалистичен
**Где:** `dashboards.html` — CEO Daily Pulse
**Проблема:** Показано 18.2K DAU. При 500K MAU это ~3.6% DAU/MAU stickiness. На странице metrics.html бенчмарк: 15-25%. Реалистичный DAU: 75K-125K.
**Fix:** Поменять DAU на ~82K (или обосновать как специфичный день/регион).
Резолюция - исправить

### 2. stg_betting__bets не включает game_id
**Где:** `data-model.html`, `data-architecture.html`
**Проблема:** SQL для `stg_betting__bets` не SELECT'ит `game_id`, но `int_bets_enriched` делает JOIN по `b.game_id`. Pipeline сломан — intermediate модель ссылается на колонку, которую staging не пропускает.
**Fix:** Добавить `game_id` и `event_id` в staging SQL.
Резолюция - исправить

---

## Important (неточности, замечают внимательные читатели)

### 3. Дата инцидента — неправильный день недели
**Где:** `incident-response.html`
**Проблема:** "2026-06-02 (Monday)" — 2 июня 2026 это **вторник**.
**Fix:** Поменять на "(Tuesday)" или сдвинуть дату на 2026-06-01 (Monday).
Резолюция - исправить

### 4. SQL метрики Turnover обращается к mart как к raw
**Где:** `metrics.html` — метрика Turnover
**Проблема:** SQL использует `toDate(placed_at)` и `sum(bet_amount)` на `mart_daily_kpi`, который уже агрегирован. Там нет `placed_at` — есть `dt` и `turnover`.
**Fix:** Упростить до `SELECT dt, turnover FROM mart_daily_kpi` или переписать на `int_bets_enriched`.
Резолюция - исправить

### 5. Onboarding SQL ссылается на несуществующие колонки
**Где:** `onboarding.html` — "Первый SELECT"
**Проблема:** SQL запрашивает `date, geo, ggr, bonus_cost, provider_fees` из `mart_daily_kpi`. Но mart имеет колонки `dt, active_players, turnover, ggr, ngr, deposits, withdrawals, ftd_count`. Нет `geo`, `bonus_cost`, `provider_fees`.
**Fix:** Переписать SQL с правильными колонками: `SELECT dt, ngr, ggr FROM mart_daily_kpi WHERE dt >= today() - 7`.
Резолюция - исправить

### 6. Коллизия event_id в JSON payload
**Где:** `event-taxonomy.html` — `player_bet_placed`
**Проблема:** Top-level `event_id` (UUID трекинг-события) коллидирует с `properties.event_id` (ID спортивного события). Путаница для разработчиков.
**Fix:** Переименовать `properties.event_id` в `sports_event_id` или `match_id`.
Резолюция - исправить

### 7. Airbyte + Kafka — архитектурная нестыковка
**Где:** `data-lineage.html`
**Проблема:** Lineage показывает Kafka → Airbyte → ClickHouse (batch каждые 15 мин). Но на странице архитектуры Airbyte — batch из DB sources, а Debezium/CDC — real-time из PostgreSQL через Kafka. Airbyte читающий из Kafka — нетипичный паттерн, противоречит "near-real-time" из архитектуры.
**Fix:** Или заменить Airbyte на Kafka-ClickHouse sink connector в lineage, или уточнить что Airbyte используется для batch-backup а real-time идёт через прямой Kafka consumer.
Резолюция - исправить

---

## Nice-to-have (усилит качество)

### 8. Company card — "Стек: Самый попсовый"
**Где:** `index.html` — company card
**Проблема:** Неинформативно и слишком неформально для company card. SPEC просит stack summary.
**Fix:** Заменить на "ClickHouse, dbt, Airflow, Metabase" (или текущее значение, если было изменено пользователем намеренно).
Резолюция - оставить как есть (это намеренная шутка)

### 9. Нет упоминания лицензии в company card
**Где:** `index.html`
**Проблема:** SPEC указывает "Curaçao license + MGA application in progress" — важный iGaming-реализм. В карточке компании не упомянуто.
**Fix:** Добавить строку "Лицензия: Curaçao (MGA в процессе)".
Резолюция - исправить

### 10. SLA page — contradictory frequency
**Где:** `sla.html`
**Проблема:** "Ежемесячный SLA review на weekly Director <-> Leads" — monthly vs weekly конфликтует.
**Fix:** Уточнить: "SLA review проводится ежемесячно в рамках одной из еженедельных встреч Director <-> Leads."


### 11. Headcount 20 vs 21
**Где:** `org-structure.html`
**Проблема:** Director + 4 leads + 16 ICs = 21, но везде написано "20 человек". Если Director не считается в "data team of 20", тогда ОК, но нужна ясность.
**Fix:** Уточнить: "20 человек в 4 стримах + Director of Data".

### 12. Нет ссылки на полный каталог метрик
**Где:** `metrics.html`
**Проблема:** SPEC упоминает "Link to full catalog" (CSV с 50+ метриками). Страница показывает 18 и не ссылается на остальные.
**Fix:** Добавить alert-info: "Здесь 18 ключевых метрик. Полный каталог (50+ метрик) — в GitHub repo" или убрать обещание из спеки.

### 13. ClickHouse type inconsistency
**Где:** `finops.html` vs `data-model.html`
**Проблема:** `bet_id` — `UUID` в finops SQL но `String PK` в ERD data model.
**Fix:** Привести к единому типу (UUID логичнее для ClickHouse).

### 14. Airflow DAG code issues
**Где:** `data-architecture.html`
**Проблема:** Python код DAG цепляет extract задачи последовательно (`extract_betting >> extract_payments >> extract_players`), хотя они должны идти параллельно. Также task objects нигде не определены.
**Fix:** Переписать на `[extract_betting, extract_payments, extract_players] >> load_to_clickhouse >> ...` (параллельный extract) и добавить определения task через `PythonOperator` или `BashOperator`.

---

## Что сильно (не трогать)

- **MLOps "Model Utilization"** — как scores превращаются в бизнес-действия. Редкий и ценный контент.
- **A/B Testing grey zone + anti-patterns** — образовательный контент, выходит за рамки спеки в лучшую сторону.
- **Management capacity planning + delegation** — реалистичные примеры с числами.
- **Dashboard mockups в чистом CSS/SVG** — технически впечатляюще, fake data (кроме DAU) выдерживает проверку.
- **Incident post-mortem** — одна из самых реалистичных fictional post-mortem: поминутный timeline, CEO обнаружил проблему раньше команды, конкретные action items с дедлайнами.
- **Тон** — русский текст читается естественно. Английские термины используются там, где CIS data community их реально использует (pipeline, mart, on-call, stakeholder). Ни один пассаж не звучит "AI-generated".
