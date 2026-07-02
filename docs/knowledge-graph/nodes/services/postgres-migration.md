# Node: Postgres Migration

## Identity
- Language: Go · goose migrations
- Path: ~/fundii/postgres-migration
- Jira label: [DB][postgres-migration]
- Flux path: apps/base/fundii/postgres-migration/

## Responsibility
Single DDL authority for all service databases. Services own no AutoMigrate.
Local dev DDL via per-service goose migrations; prod schema is deployed by this service.

## Key files
- migrations/   — versioned goose SQL files per service schema
- cmd/          — migration runner entrypoint
- configs/      — DB connection config per env

## If this changes, also check
→ [[advisory]], [[advisory-workflow]], [[fund-catalog]], [[portfolio]], [[trading]]
→ Jira labels: [DB][BE]
