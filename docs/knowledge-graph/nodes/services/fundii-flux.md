# Node: Fundii Flux (K8s GitOps)

## Identity
- Stack: FluxCD · Kustomize · SOPS
- Path: ~/fundii/fundii-flux
- Jira label: [INFRA]

## Structure
```
apps/
  base/          — base Kustomize manifests (image, env, resources)
    rca/         — advisory, advisory-workflow, fund-catalog, portfolio, trading + cronjobs
    fundii/      — platform services (auth, order, payment, etc.)
    ascend/      — iic-dashboard, fee-service
  develop/       — dev env overlays
  uat/           — UAT env overlays
  prod/          — prod env overlays
infrastructure/  — shared infra (kafka, elasticsearch, apisix, monitoring)
dependencies/    — FluxCD system dependencies per env
clusters/        — cluster-level bootstrap
```

## Key files per service
- apps/base/<ns>/<svc>/flux.yaml       — HelmRelease or Kustomization source
- apps/base/<ns>/<svc>/kustomization.yaml
- apps/<env>/<ns>/<svc>/patch.yaml     — env-specific image tag / replicas
- apps/<env>/<ns>/<svc>/secrets.yaml   — SOPS-encrypted secrets

## If this changes, also check
→ All services deployed in the affected namespace/env
→ SOPS key rotation affects secrets.yaml in all envs
→ Jira labels: [INFRA]
