# CLAUDE.md — Robowealth Project

## Role
You are a senior technical assistant for the Robowealth project.
When asked to plan tasks, always use the knowledge graph first.

## Knowledge Graph
Located in `docs/knowledge-graph/`.

### Reading order for task planning:
1. `docs/knowledge-graph/index.md` — find affected nodes
2. `docs/knowledge-graph/edges/impact-map.md` — find ripple effects
3. `docs/knowledge-graph/nodes/services/<name>.md` — get file paths
4. Scan actual code files listed in the node

## Graphify — per-service code graph
When `graphify-out/` exists inside a service repo, use `/graphify` **before** grep, find, or Explore agents for any code question about that service.

| Service | graphify-out? |
|---------|---------------|
| iic-dashboard | ✅ ~/iic/iic-dashboard/graphify-out/ |
| advisory | ❌ use grep/Explore |
| advisory-workflow | ❌ use grep/Explore |
| fund-catalog | ❌ use grep/Explore |
| portfolio | ❌ use grep/Explore |
| trading | ❌ use grep/Explore |

## Jira Ticket Format
Always output tickets in this format:

**[LAYER][service-name] Title**
- What changes: ...
- Files affected: ...
- Depends on ticket: ...
- Label: [FE] / [BE] / [DB] / [INFRA] / [SERVICE] / [QA]

## Stack
- Backend: Go 1.26 · Hexagonal / ports-and-adapters · Uber fx
- Frontend: Next.js 14 · TypeScript · Tailwind
- Infra: GCP · K8s · FluxCD · Kafka · Elasticsearch
- DB migrations: ~/fundii/postgres-migration (goose, centralised DDL)
- K8s GitOps: ~/fundii/fundii-flux
- Jira project key: IIC

## Real Service Paths
| Service | Repo path |
|---------|-----------|
| advisory | ~/rca/advisory |
| advisory-workflow | ~/rca/advisory-workflow |
| fund-catalog | ~/rca/fund-catalog |
| portfolio | ~/rca/portfolio |
| trading | ~/rca/trading |
| iic-dashboard | ~/iic/iic-dashboard |
| postgres-migration | ~/fundii/postgres-migration |
| fundii-flux | ~/fundii/fundii-flux |
