# Node: Advisory Workflow Service

## Identity
- Language: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Path: ~/rca/advisory-workflow
- Module: git.robodev.co/rca/advisory-workflow
- Jira label: [BE][advisory-workflow]
- Flux path: apps/base/rca/advisory-workflow/

## Exposes (REST)
- advised_portfolio — workflow entry point (subscribe/redeem/order triggers)
- core_portfolio — portfolio state for workflow
- order — order management
- redemption — redemption workflow
- subscription — subscription workflow

## Depends on
- PostgreSQL: workflow_db (lots, lot_disposals, lot_reservations, orders, order_events, outbox, account_profiles)
- advisory service (REST client) — reads trade proposals
- fund-catalog service (REST client) — reads fund rules
- portfolio service (REST client) — reads current holdings
- unitholder (REST client) — reads unitholder data
- FCN (external REST) — places subscription/redemption at fund company
- Kafka (outbox pattern) — publishes lot/order events

## Key files
- internal/adapter/inbound/rest/         — HTTP handlers
- internal/adapter/outbound/advisory/    — advisory REST client
- internal/adapter/outbound/fundcatalog/ — fund-catalog REST client
- internal/adapter/outbound/portfolio/   — portfolio REST client
- internal/adapter/outbound/fcn/         — FCN external API client
- internal/adapter/outbound/kafka/       — Kafka publisher (outbox)
- internal/adapter/outbound/postgres/    — local DB (lots, orders, outbox)
- internal/application/                  — use-cases / orchestration
- internal/domain/                       — entities & value objects
- internal/port/                         — interfaces

## If this changes, also check
→ [[advisory]] (trade proposal contract)
→ [[fund-catalog]] (fund rules API)
→ [[portfolio]] (holdings API)
→ Kafka consumers (lot/order event schema)
→ [[iic-dashboard]] modules/rca/ (order/redemption flows)
