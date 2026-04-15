# Sprint 3: Data Model + Event Taxonomy — Report

**Status:** Done
**Date:** 2026-04-15

## Goal

Pages 03 and 04 — Data Model (ERD + entities + dbt layers + marts) and Event Taxonomy (naming + schema + tracking plan + change process).

## Deliverables

### `pages/data-model.html` (31KB)

**ERD Diagram (mermaid.js):**
- 9 entities with relationships rendered as erDiagram
- Dark theme config matching site palette
- Dimensions: dim_players, dim_games, dim_sports_events
- Facts: fct_bets, fct_deposits, fct_withdrawals, fct_sessions, fct_bonuses, fct_events_raw

**Entity Descriptions (9 accordions):**
- Each entity: full field list with types and descriptions
- iGaming-specific context (KYC, VIP tiers, wagering, RTP, bet types)
- FK references annotated (→ target table)

**dbt Layers:**
- Staging SQL example: stg_betting__bets (type casting, cleanup)
- Intermediate SQL example: int_bets_enriched (player + game joins)
- Description of mart layer

**Mart Descriptions (4 accordions):**

| Mart | Refresh | Sources |
|------|---------|---------|
| mart_daily_kpi | daily | int_bets_enriched, int_daily_costs |
| mart_player_lifetime | daily | int_bets_enriched, int_deposits, int_sessions |
| mart_cohort_analysis | weekly | int_bets_enriched, stg_players |
| mart_marketing_performance | daily | int_deposits, stg_players, stg_marketing_spend |

**Cross-links:** Data Architecture (01), Event Taxonomy (04)

---

### `pages/event-taxonomy.html` (24KB)

**Naming Convention:**
- Format: `{domain}_{object}_{action}`
- 4 domains, objects list, actions list
- Tip alert with naming rule

**Event Schema (3 accordions):**
- Required fields (6): event_name, event_id, player_id, timestamp, session_id, platform
- Context fields (5): auto-collected (geo_ip, device_type, app_version, etc.)
- Event-specific fields: varies per event type

**JSON Payloads (4 accordions):**
- player_bet_placed (sports live bet with full context)
- player_deposit_completed (card deposit with fees)
- session_page_viewed (page navigation)
- player_registration_completed (paid_search acquisition)

**Tracking Plan (HTML table, 15 events):**
- 13 live + 2 planned events
- Columns: event, trigger, key params, source (frontend/backend/server), owner, status
- Covers: registration, KYC, deposits, withdrawals, bets, bonuses, sessions, games, marketing, compliance, system

**Change Process (timeline, 6 steps):**
- Request → Review → Spec → Implementation → QA → Deploy
- Deprecation warning (30-day grace period)

## Checklist

- [x] mermaid.js ERD (9 entities with relationships)
- [x] 9 entity accordions with full field descriptions
- [x] dbt layers: 2 SQL examples (staging, intermediate)
- [x] 4 mart descriptions with fields, sources, refresh frequency
- [x] Naming convention with domains/objects/actions
- [x] Event schema (required + context + specific)
- [x] 4 JSON payload examples
- [x] Tracking plan table (15 events)
- [x] Change process (6-step timeline)
- [x] Navigation works on both pages
- [x] Cross-links between pages
- [x] Both pages < 100KB (31KB + 24KB)
