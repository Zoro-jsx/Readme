---
title: Pagination
excerpt: >-
  All endpoints that return a list of items (e.g. search results, transaction
  histories, usage logs, user notifications) are paginated to ensure optimal
  performance and fast response times.
deprecated: false
hidden: false
metadata:
  robots: index
---

**Pagination**

Endpoints that return lists — case search results and transaction history — support pagination through two request parameters.

**Request Parameters**

| Parameter | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `page` | integer | `1` | The page number to retrieve, starting from 1 |
| `perPage` | integer | `20` | Number of results per page. Maximum is `100` |

For `POST` endpoints such as `/case-search`, these parameters are included in the JSON request body. For `GET` endpoints such as `/api-billing/transactions`, they are passed as query parameters.

**Response Envelope**

All paginated responses include the following fields alongside the results array.

```json
{
  "success": true,
  "response": {
    "totalCount": 84,
    "page": 2,
    "limit": 20,
    "pages": 5,
    "cases": [ ... ]
  }
}
```

| Field | Description |
| :--- | :--- |
| `totalCount` | Total number of records matching the query across all pages |
| `page` | The page returned in this response |
| `limit` | The page size used for this response |
| `pages` | Total number of available pages |

To determine whether more results exist, check whether `page` is less than `pages`. When they are equal, the current page is the last.

**Iterating Through Pages**

```bash
# Page 1
curl -X POST https://api.courtrecordplatform.in/api/v1/case-search \
  -H "Authorization: Bearer cr_live_yourKey" \
  -H "Content-Type: application/json" \
  -d '{ "petitioner": "Reliance Industries", "page": 1, "perPage": 20 }'

# Page 2
curl -X POST https://api.courtrecordplatform.in/api/v1/case-search \
  -H "Authorization: Bearer cr_live_yourKey" \
  -H "Content-Type: application/json" \
  -d '{ "petitioner": "Reliance Industries", "page": 2, "perPage": 20 }'
```

Each page request for a search endpoint consumes credits. When iterating through large result sets, cache results locally to avoid redundant requests. The `totalCount` field on the first page response can be used to determine in advance how many pages to expect.
