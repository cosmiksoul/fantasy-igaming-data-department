# Sprint 9: A/B Testing + Management — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 13 and 14 — A/B Testing Framework and Management Practices.

## Deliverables

### `pages/ab-testing.html` (18KB)

**HADI-цикл (4-step timeline):**
- Hypothesis → Action → Data → Insight (loop)

**Бэклог гипотез (таблица, 6 записей):**
- AB-01 (done): упрощение депозита, Reg→FTD +15%
- AB-02 (running): рекомендации игр, session duration +10%
- AB-03 (backlog): cashback vs freebet, LTV 30d +8%
- AB-04 (backlog): live-стриминг, live handle +20%
- AB-05 (backlog): timing push-уведомлений, CTR +30%
- AB-06 (rejected): скрытие вейджера — заблокирован Compliance

**Чеклист запуска (8 пунктов):**
- Гипотеза, метрики, sample size, рандомизация, длительность, sign-off, no-peek, rollback

**Шаблон отчёта:**
- Гипотеза → Setup → Результат → Сегментация → Рекомендация → Learnings

**Полный кейс AB-01 (3 accordion):**
- Расчёт: baseline 33%, MDE +15%, sample 1,800/group, 7 дней
- Результаты: Reg→FTD +14.2% (p=0.003), time-to-deposit -33%, guardrail OK
- Сегментация: mobile +23.5%, desktop +3.9%, CIS +14.6%, LatAm +15.8%
- Решение: раскатить. Expected impact: +38 FTD/день, +$2,280/день NGR
- Conditional formatting в таблицах результатов

---

### `pages/management.html` (14KB)

**Структура спринта (5-step timeline):**
- Planning → Standups → Mid-sprint check → Review → Retro
- 70% roadmap / 30% ad-hoc буфер

**Регулярные встречи (таблица, 5 встреч):**
- 1-on-1 weekly, C-level bi-weekly, all-hands monthly, Governance quarterly, cross-functional weekly

**1-on-1 с лидом:**
- 3 блока: People / Process / Strategy (card grid)

**OKR (пример Q2 2026):**
- Objective + 4 Key Results с target, текущим значением и conditional formatting

**Управление бэклогом:**
- Каналы поступления (Jira, Slack, cross-functional sync)
- RICE приоритизация (формула + таблица факторов)
- Коммуникация: Slack-бот + weekly digest

**База знаний:**
- 5 разделов wiki (Architecture, Metrics, Processes, Runbooks, Onboarding)
- Правило двух раз: вопрос задали дважды в Slack → ответ в wiki

## Checklist

- [x] HADI-цикл (4-step timeline)
- [x] Бэклог гипотез (6 записей с ICE)
- [x] Чеклист запуска (8 пунктов)
- [x] Шаблон отчёта
- [x] Полный кейс AB-01 с числами и сегментацией
- [x] Sprint structure (5-step timeline)
- [x] Meeting cadence (5 встреч)
- [x] 1-on-1 structure (People/Process/Strategy)
- [x] OKR example (Q2 2026, 4 KRs)
- [x] Backlog management (RICE)
- [x] Knowledge management (wiki)
- [x] Navigation works on both pages
- [x] Both pages < 100KB (18KB + 14KB)
