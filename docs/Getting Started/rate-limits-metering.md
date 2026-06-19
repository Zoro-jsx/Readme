---
title: Rate Limits & Metering
excerpt: >-
  To ensure platform reliability and fair credit usage, all API requests are
  subject to rate limiting and credits-based metering.
deprecated: false
hidden: false
metadata:
  robots: index
---

# Rate Limits & Metering

To ensure platform reliability, fair resource allocation, and system stability, the Court Record Platform API enforces rate limits (throttling) and credits-based metering.

---

## 1. Throttling & Rate Limits

Rate limits are enforced at the API Gateway level based on your client IP address and authenticated credentials.

### Throttle Limits

| Client Category | Rate Limit | Burst Limit | Description |
| :--- | :--- | :--- | :--- |
| **Anonymous / Public Routes** | 5 requests / min | 10 requests | Tight limits applied to prevent scraping of public information. |
| **Standard API Keys / JWT** | 60 requests / min | 120 requests | Default programmatic tier for general integrations. |
| **Enterprise Tiers** | 300 requests / min | 600 requests | Customized limits for high-volume background scrapers. |

When a client exceeds these limits, the gateway returns an **HTTP 429 Too Many Requests** error.

---

## 2. API Metering & Credit Pools

Programmatic operations consume credits from your organization's wallet balance. Credits are divided into two distinct pools:

1. **Subscription Credits**: Monthly credits granted with your active subscription plan. These expire at the end of the billing cycle.
2. **Purchased Credits (Top-ups)**: Credits purchased as a pay-as-you-go top-up. These **do not expire** and are consumed only after your Subscription Credits are fully exhausted.

### Credit Cost Schedule

| Endpoint Code | Rate (Credits) | Target Endpoint | Description |
| :--- | :--- | :--- | :--- |
| **`SEARCH_CASE`** | `5` | `POST /api/v1/case-search` | Querying lists of cases by petitioner, respondent, or advocate. |
| **`GET_CASE_DETAIL`** | `10` | `POST /api/v1/case-detail/searchByCnr` | Fetching the full historical case record by CNR number. |
| **`REFRESH_CASE`** | `15` | `POST /api/v1/case-refresh` | Enqueuing a worker to pull live scraping updates from eCourts. |
| **`COURT_STRUCTURE`** | `1` | `GET /api/v1/court-structure` | Fetching static lists of states, districts, and complexes. |

---

## 3. Rate Limit Response Headers

Each response contains headers to help you track your current rate limit usage:

```http
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 42
X-RateLimit-Reset: 1718804700
```

* **`X-RateLimit-Limit`**: The maximum number of requests allowed in the current time window.
* **`X-RateLimit-Remaining`**: The number of requests remaining in the current time window.
* **`X-RateLimit-Reset`**: The Unix timestamp indicating when the current rate limit window resets.

---

## Best Practices

To ensure uninterrupted service and minimize cost, we recommend incorporating the following patterns in your client application:

1. **Implement Caching**: Cache static details (such as court structures and historical closed cases) in a local database or memory store (e.g. Redis) to avoid redundant requests.
2. **Handle HTTP 429 Gracefully**: Check for HTTP 429 status codes and parse the `X-RateLimit-Reset` header.
3. **Exponential Backoff**: When retrying failed requests, use an exponential backoff strategy with random jitter to avoid flooding the API Gateway.
4. **Monitor Credit Balances**: Programmatically query `/api/v1/wallet` to check credit levels and set up alerts for when credits fall below a critical threshold.
