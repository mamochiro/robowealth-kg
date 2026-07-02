# Node: Portfolio Service

## Identity
- Language: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Path: ~/rca/portfolio
- Module: git.robodev.co/rca/portfolio
- Jira label: [BE][portfolio]
- Flux path: apps/base/rca/portfolio/ + portfolio-cronjob/

## Exposes (REST)
- position — current position reader
- position_snapshot — point-in-time position snapshot

## Depends on
- PostgreSQL: portfolio_db (positions, position_snapshots, fund_metadata, unitholder_balances)
- Kafka (consumer) — receives events: lot_upserted, lot_disposal, reservation_upserted, order_status_changed, allotted_transaction, dividend_transaction, nav_updated, fund_metadata_updated

## Key files
- internal/adapter/inbound/kafka/      — Kafka event handlers (lot/reservation/order events)
- internal/adapter/inbound/rest/       — REST read endpoints (position, position_snapshot)
- internal/adapter/outbound/postgres/  — position, snapshot, fund_metadata, unitholder_balance repos
- internal/application/               — projection logic
- internal/domain/                    — Position, Lot entities
- internal/port/inbound/              — Kafka handler contracts
- internal/port/outbound/             — DB repository contracts

## If this changes, also check
→ [[advisory-workflow]] (holdings source contract)
→ [[iic-dashboard]] modules/balance/ + modules/portfolio-model/ (position display)
→ Kafka event producers (lot/reservation schema)
