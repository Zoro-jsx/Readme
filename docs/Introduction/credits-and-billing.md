---
title: Credits & Billing
hidden: false
---

**Credits & Billing**

API usage on the Court Record Platform is metered through a credit system. Every billable API call deducts a fixed number of credits from your account balance. Credits come from two pools, consumed in priority order.

**Credit Pools**

**Subscription Credits** are issued monthly as part of an active subscription plan. They reset at the start of each billing cycle and expire if unused. Subscription credits are always consumed first.

**Purchased Credits** are acquired through one-time top-up packages. They never expire and are drawn upon only after the subscription credit pool is exhausted. Purchased credits carry over indefinitely between billing cycles.

**Credit Costs**

| Endpoint | Credits per Call |
| :--- | :--- |
| `POST /case-search` | 5 |
| `POST /case-detail/searchByCnr` | 10 |
| `POST /case-detail/searchByCnr/bulk` | 10 per CNR found |
| `POST /case-refresh` | 15 |
| `POST /case-refresh/bulk` | 15 per case refreshed |
| `GET /court-structure/*` | 1 |

Current rates are always available programmatically at `GET /api-billing/pricing`, which returns both pay-as-you-go and subscriber rates for every endpoint.

**Subscription Plans**

Subscription plans provide a fixed monthly credit allocation at a discounted per-credit rate compared to pay-as-you-go pricing. Available plans are listed at `GET /api-billing/plans`. To subscribe, send a `POST /api-billing/subscribe` request with the chosen `planId`.

**Top-Up Packages**

One-time credit packages are available for accounts that need additional credits beyond their subscription allocation, or for accounts operating without a subscription. Available packages are listed at `GET /api-billing/packages`. Purchases are processed through `POST /api-billing/topup`.

**Monitoring Usage**

Your current credit balance is available at any time via `GET /api-billing/credits`. This endpoint returns separate counts for subscription credits and purchased credits, along with the total available. Your transaction history — including each debit with the endpoint description and timestamp — is available at `GET /api-billing/transactions`.

> Implement balance monitoring in your application and alert before credits reach zero. Requests made with an insufficient balance will be rejected with a `402 Payment Required` response.
