# Node: Fund Catalog Service

## Identity
- Language: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Path: ~/rca/fund-catalog
- Module: git.robodev.co/rca/fund-catalog
- Jira label: [BE][fund-catalog]
- Flux path: apps/base/rca/fund-catalog/ + fund-catalog-cronjob/

## Exposes (REST)
- fund — fund master data CRUD & search
- identity — fund identity/code mapping
- publicholiday — trading calendar
- review — fund review data
- sync — manual sync trigger
- openapi — public API spec

## Depends on
- PostgreSQL: fund_catalog_db (funds, identities, navs, public_holidays, outbox)
- FundConnext (external REST) — authoritative source for fund data/NAV
- Elasticsearch — fund search index
- Kafka (outbox pattern) — publishes fund/NAV update events

## Key files
- internal/adapter/inbound/rest/              — HTTP handlers
- internal/adapter/outbound/fundconnext/      — FundConnext REST client
- internal/adapter/outbound/elasticsearch/    — ES index writes
- internal/adapter/outbound/kafka/            — Kafka publisher
- internal/adapter/outbound/postgres/         — fund, identity, nav, outbox repos
- internal/application/                       — use-cases
- internal/domain/                            — fund entity, NAV, trading rules
- internal/port/                              — interfaces

## If this changes, also check
→ [[advisory-workflow]] (fund rules contract)
→ [[trading]] (fund catalog API)
→ Elasticsearch index mapping (fund search)
→ Kafka consumers (fund/NAV event schema)
→ [[iic-dashboard]] modules/fund/ (fund display)
