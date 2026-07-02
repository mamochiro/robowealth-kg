# Knowledge Graph Index

## Service Nodes

| Node | Path | Type | Label |
|------|------|------|-------|
| advisory | nodes/services/advisory.md | Go service | [BE][SERVICE] |
| advisory-workflow | nodes/services/advisory-workflow.md | Go service (worker) | [BE][SERVICE] |
| fund-catalog | nodes/services/fund-catalog.md | Go service | [BE][SERVICE] |
| portfolio | nodes/services/portfolio.md | Go service | [BE][SERVICE] |
| trading | nodes/services/trading.md | Go service | [BE][SERVICE] |
| iic-dashboard | nodes/services/iic-dashboard.md | Next.js frontend | [FE] |
| postgres-migration | nodes/services/postgres-migration.md | DB migrations | [DB] |
| fundii-flux | nodes/services/fundii-flux.md | K8s FluxCD | [INFRA] |

## Dependency Graph

```
iic-dashboard
  └─► advisory            (REST)
  └─► advisory-workflow   (REST)

advisory-workflow
  └─► advisory            (REST client — reads trade proposals)
  └─► fund-catalog        (REST client — reads fund rules)
  └─► portfolio           (REST client — reads holdings)
  └─► FCN                 (external REST — places orders at fund company)
  └─► Kafka               (publish order events)

trading
  └─► advisory            (REST client — reads advised portfolios)
  └─► fund-catalog        (REST client — reads fund catalog)
  └─► FCN                 (external REST — order execution)
  └─► Kafka               (publish transaction events)
  └─► GCS                 (file storage)

portfolio
  └─ Kafka ──►            (consume lot/reservation events)

fund-catalog
  └─► FundConnext         (external REST — sync fund data/NAV)
  └─► Elasticsearch       (index fund data)
  └─► Kafka               (publish fund events)

postgres-migration ──► all services (DDL owner)
fundii-flux        ──► all services (k8s deploy)
```

## Environments

| Env | Namespace | Flux path |
|-----|-----------|-----------|
| develop | rca-dev | apps/develop/rca/ |
| uat | rca-uat | apps/uat/rca/ |
| prod | rca | apps/prod/rca/ |
