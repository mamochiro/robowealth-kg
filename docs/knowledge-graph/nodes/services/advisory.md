# Node: Advisory Service

## Identity
- Language: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Path: ~/rca/advisory
- Module: git.robodev.co/rca/advisory
- Jira label: [BE][advisory]
- Flux path: apps/base/rca/advisory/

## Exposes (REST)
- advised_portfolio — managed portfolio CRUD
- core_portfolio — core portfolio state
- core_portfolio_terms — terms & acceptance
- evaluate — rebalance evaluation
- trade — trade execution trigger
- trade_proposal — proposal CRUD & queries

## Depends on
- PostgreSQL: advisory_db (trade_proposals, core_portfolios, rebalance_records, terms)
- No external HTTP calls (other services call it)

## Key files
- internal/adapter/inbound/rest/       — HTTP handlers
- internal/adapter/outbound/postgres/  — DB queries
- internal/application/               — use-cases
- internal/domain/                    — entities & value objects
- internal/port/                      — interfaces
- migrations/postgres/                — goose migrations (DDL managed by postgres-migration)

## If this changes, also check
→ [[advisory-workflow]] (REST client calls advisory)
→ [[trading]] (reads advised portfolio state)
→ [[iic-dashboard]] modules/rca/ (FE display)
