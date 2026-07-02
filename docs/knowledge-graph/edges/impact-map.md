# Impact Map
> "If X changes → what else breaks or needs updating"

## advisory
→ [[iic-dashboard]]: portfolio/rebalance UI reads advisory REST
→ [[advisory-workflow]]: reads trade proposals via advisory REST client
→ [[trading]]: reads advised portfolio state
→ Jira labels: [BE][SERVICE]

## advisory-workflow
→ [[iic-dashboard]]: triggers workflow (order/redemption/subscription endpoints)
→ [[advisory]]: calls advisory REST to read trade proposals
→ [[fund-catalog]]: reads fund rules before placing order
→ [[portfolio]]: reads holdings before rebalancing
→ FCN: places subscription/redemption at fund company
→ Kafka: publishes order/lot events consumed by [[portfolio]]
→ Jira labels: [BE][SERVICE]

## fund-catalog
→ [[advisory-workflow]]: fund rules used to validate rebalance
→ [[trading]]: fund data read before order execution
→ [[iic-dashboard]]: fund list/detail pages
→ Elasticsearch: fund search index must stay in sync
→ Jira labels: [BE][SERVICE][DB]

## portfolio
→ [[advisory-workflow]]: holdings used to compute rebalance delta
→ [[iic-dashboard]]: position/balance display
→ Kafka consumers: receives lot/reservation events from [[advisory-workflow]]
→ Jira labels: [BE][SERVICE]

## trading
→ [[iic-dashboard]]: order/transaction/position display
→ [[advisory]]: reads advised portfolio state
→ [[fund-catalog]]: reads catalog before executing
→ FCN: order execution calls external fund network
→ Kafka: publishes transaction events
→ Jira labels: [BE][SERVICE]

## iic-dashboard
→ [[advisory]], [[advisory-workflow]], [[trading]]: API base URL / auth token changes affect FE
→ Jira labels: [FE]

## postgres-migration
→ [[advisory]], [[advisory-workflow]], [[fund-catalog]], [[portfolio]], [[trading]]: schema DDL owner
→ Jira labels: [DB][BE]

## fundii-flux
→ [[advisory]], [[advisory-workflow]], [[fund-catalog]], [[portfolio]], [[trading]], [[iic-dashboard]]: k8s deploy config
→ Jira labels: [INFRA]

## Kafka topic change
→ publishing service: update outbox/publisher
→ consuming service: update handler contract
→ Jira labels: [BE][SERVICE]
