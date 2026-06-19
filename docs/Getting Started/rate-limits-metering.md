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
## 1. Rate Limiting

Endpoints are limited based on your client IP address and your authentication method:

- **Authenticated (JWT or API Key) requests**: Rate limits are higher and scale based on your subscription tier (e.g. 60 requests per minute).
- **Public / Anonymous requests**: Tight limits are applied to prevent scraping of public lists (e.g. 5 requests per minute).

When you exceed the rate limit, the API returns a `429 Too Many Requests` error with the standard `ErrorResponse` payload.

***

## 2. API Metering & Credit Pools

programmatic calls using API keys consume credits from your wallet. Credits are divided into two pools:

1. **Subscription Credits**: Monthly credits granted with your active subscription plan. These expire at the end of the billing cycle.
2. **Purchased Credits (Top-ups)**: Credits purchased as a pay-as-you-go top-up. These do not expire and are consumed only after your Subscription Credits are fully exhausted.

***

## 3. Credit Consumption Rates

Each API endpoint code carries a different rate in credits per call. Here is the pricing schedule:

| Endpoint Code     | Rate (Credits) | Description                                                                     |
| :---------------- | :------------- | :------------------------------------------------------------------------------ |
| `SEARCH_CASE`     | `5`            | Querying the list of cases via `POST /case-search`.                             |
| `GET_CASE_DETAIL` | `10`           | Retrieving full details of a specific case via `POST /case-detail/searchByCnr`. |
| `REFRESH_CASE`    | `15`           | Requesting a live scrape and update of a case from eCourts.                     |
| `COURT_STRUCTURE` | `1`            | Fetching court, complex, state, or district lists.                              |

***

## Checking Your Balance

To programmatically check your current credit balance and daily usage summary, query:

```bash
curl -X GET https://api.yourcompany.com/api/v1/wallet \
  -H "Authorization: Bearer <your_api_key>"
```

<br />
