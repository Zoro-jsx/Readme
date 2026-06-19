---
title: 'Pagination  '
excerpt: >-
  All endpoints that return a list of items (e.g. search results, transaction
  histories, usage logs, user notifications) are paginated to ensure optimal
  performance and fast response times.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Request Parameters

To paginate list results, include the following query parameters in your request:

| Parameter | Type     | Default | Description                                             |
| :-------- | :------- | :------ | :------------------------------------------------------ |
| `page`    | `number` | `1`     | The page index to fetch (1-indexed).                    |
| `limit`   | `number` | `20`    | The number of documents to return per page. Max: `100`. |

***

## Response Envelope

All paginated responses follow a standard envelope wrapper matching the Mongoose pagination schema:

```json
{
  "success": true,
  "response": {
    "docs": [
      // List of result objects (e.g. Cases, Transactions, Notifications)
    ],
    "totalDocs": 120,    // Total number of matching items in the database
    "limit": 20,         // Limit used in the query
    "page": 1,           // Current page number
    "totalPages": 6,     // Total pages available
    "pagingCounter": 1,  // The index of the first document on the current page
    "hasPrevPage": false,// True if a previous page exists
    "hasNextPage": true, // True if a next page exists
    "prevPage": null,    // Previous page index (null if first page)
    "nextPage": 2        // Next page index (null if last page)
  }
}
```

***

## Example Paginated Request

```bash
curl -X GET "https://api.yourcompany.com/api/v1/wallet/transactions?page=2&limit=10" \
  -H "Authorization: Bearer <your_api_key>"
```

<br />
