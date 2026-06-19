---
title: Rate Limits
hidden: false
---

**Rate Limits**

The Court Record Platform API enforces rate limits to ensure consistent availability for all integrations. Limits are applied per API key and reset on a rolling basis.

**Request Limits by Plan**

| Plan | Requests / minute | Requests / hour |
| :--- | :--- | :--- |
| Free | 20 | 500 |
| Starter | 60 | 2,000 |
| Professional | 200 | 10,000 |
| Enterprise | Custom | Custom |

Limits apply to the total number of HTTP requests made with a key, regardless of which endpoint is called. Bulk endpoints that accept multiple CNR numbers count as a single request.

**Rate Limit Headers**

Every API response includes headers that describe the current state of your rate limit allowance.

| Header | Description |
| :--- | :--- |
| `X-RateLimit-Limit` | Maximum requests allowed in the current window |
| `X-RateLimit-Remaining` | Requests remaining in the current window |
| `X-RateLimit-Reset` | Unix timestamp when the current window resets |
| `Retry-After` | Seconds to wait before retrying (present only on 429 responses) |

**When You Are Rate Limited**

When the limit is exceeded the API responds with HTTP `429 Too Many Requests`:

```json
{
  "success": false,
  "message": "Too many requests. Please slow down.",
  "moreInfo": "Rate limit exceeded. Retry after 37 seconds."
}
```

**Handling Rate Limits**

Implement exponential backoff in your client: when you receive a `429`, read the `Retry-After` header and wait at least that many seconds before retrying. Do not immediately re-send the request — repeated fast retries prolong the backoff window.

```bash
# The Retry-After header tells you exactly when to retry
HTTP/1.1 429 Too Many Requests
Retry-After: 37
X-RateLimit-Reset: 1735689600
```

For high-volume workloads, use the bulk refresh and batch-capable endpoints to reduce request count. If your integration consistently reaches plan limits, consider upgrading to a higher plan or contacting support to discuss Enterprise limits.
