# Node: Trading Service

## Identity
- Language: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Path: ~/rca/trading
- Module: git.robodev.co/rca/trading
- Jira label: [BE][trading]
- Flux path: apps/base/rca/trading/ + trading-cronjob/

## Exposes (REST)
- order — order management
- transaction — transaction reader
- position — position reader
- lot — lot management

## Depends on
- PostgreSQL: trading_db (orders, transactions, lots, outbox, account_profiles)
- advisory service (REST client) — reads advised portfolio state
- fund-catalog service (REST client) — reads fund data
- FCN (external REST) — order execution at fund company (subscription/redemption)
- GCS — file storage (trade confirmations, reports)
- Kafka (outbox pattern) — publishes transaction/lot events

## Key files
- internal/adapter/inbound/rest/          — HTTP handlers (order, transaction, position, lot)
- internal/adapter/outbound/rest/         — REST clients (advisory, fund-catalog)
- internal/adapter/outbound/fcn/          — FCN external API client
- internal/adapter/outbound/gcs/          — GCS file storage
- internal/adapter/outbound/kafka/        — Kafka publisher
- internal/adapter/outbound/postgres/     — local DB repos
- internal/application/                   — use-cases
- internal/domain/                        — Order, Transaction, Lot entities
- internal/port/                          — interfaces

## If this changes, also check
→ [[advisory]] (advised portfolio contract)
→ [[fund-catalog]] (fund catalog API)
→ Kafka consumers (transaction event schema)
→ [[iic-dashboard]] modules/transaction/ + modules/allotted-transaction/
