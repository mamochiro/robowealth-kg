# Node: IIC Dashboard

## Identity
- Language: TypeScript · Next.js 14 · Tailwind
- Path: ~/iic/iic-dashboard
- Jira label: [FE][iic-dashboard]
- Flux path: apps/base/ascend/iic-dashboard/ + apps/base/fundii/iic-dashboard/
- **Architecture: Full-stack Next.js — has significant server-side backend, NOT pure frontend**
  - `app/api/` — REST API routes (webhooks, cron jobs, FCN proxies)
  - `app/api/line/chat/route.ts` — LINE OA webhook receiver (already handles SUB/RED/SWO/XSWO postbacks)
  - `app/api/cron/` — cron job routes secured with CRON_SECRET
  - `integrations/line/` — LINE Messaging API: pushRawMessage, handlePostback, Flex Message builders
  - `modules/transaction/transaction.service.ts` — direct FCN calls (approve/cancel subscription, redemption, switching)
  - `prisma/` — Prisma ORM with direct Postgres access
  - Check here first before routing work to Go RCA services

## Key modules
- modules/portfolio-model/ — PortfolioModelDetail, repository, service, mapper, types
- modules/transaction/     — transaction service, repository, types, filter (single-fund orders)
- modules/customer/        — customer repository, service, mapper, types
- modules/rca/trading/     — by-lot redemption / switching order logic
- modules/rca/portfolio/   — lot service
- modules/balance/         — unitholder balance display
- modules/allotted-transaction/ — allotted transaction records
- modules/fund/            — fund catalog display
- modules/fee-*/           — fee management UI
- modules/user/, modules/team/ — user & team management
- modules/permission/      — permission constants registry

## Calls (via integrations/rca/)
- integrations/rca/advisory-service/portfolio-model.client.ts — fetchPortfolioModels, fetchPortfolioModelDetail
- integrations/rca/advisory-workflow-service/ — portfolio model subscription orders (order.client.ts — to be created for IIC-323)
- integrations/rca/portfolio-service/
- integrations/rca/trading-service/
- integrations/rca/rca-gateway.ts — shared auth headers

## Key file layout
- app/(protected)/          — authenticated Next.js App Router pages
- app/(protected)/transactions/create/ — SubscriptionForm, RedemptionForm, SwitchingForm, CrossAmcSwitchingForm
- modules/<domain>/         — service, repository, types, mapper per domain
- integrations/rca/<svc>/   — API clients for each backend service
- components/               — shared UI components
- lib/number.ts, lib/utils.ts — number formatting, misc utilities
- hooks/                    — shared React hooks

## If this changes, also check
→ [[advisory]], [[advisory-workflow]], [[trading]], [[fund-catalog]] (API contract)
→ [[fundii-flux]] image tag (apps/*/fundii/iic-dashboard/ or apps/*/ascend/iic-dashboard/)
