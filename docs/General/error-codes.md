---
title: Error Codes
hidden: false
---

**Error Codes**

All error responses from the Court Record Platform API follow a consistent structure. Successful responses carry `"success": true`; error responses carry `"success": false` accompanied by a human-readable message.

**Error Response Format**

```json
{
  "success": false,
  "message": "API key not found or has been revoked.",
  "moreInfo": "No additional info found."
}
```

| Field | Type | Description |
| :--- | :--- | :--- |
| `success` | boolean | Always `false` for error responses |
| `message` | string | Human-readable description of the error |
| `moreInfo` | string | Additional context when available |

**HTTP Status Codes**

| Status | Name | When it occurs |
| :--- | :--- | :--- |
| `200` | OK | The request succeeded and the response body contains the result |
| `400` | Bad Request | The request body or parameters failed validation. The `message` field specifies which field is invalid |
| `401` | Unauthorized | No `Authorization` header was provided, or the API key is missing, malformed, expired, or revoked |
| `403` | Forbidden | The API key is valid but does not have the required scope for the requested operation |
| `404` | Not Found | The resource (case, key, plan) does not exist |
| `409` | Conflict | The request conflicts with existing state — for example, attempting to subscribe to an already-active plan |
| `422` | Unprocessable Entity | The request is structurally valid but cannot be processed — for example, a CNR number that does not match any known court |
| `429` | Too Many Requests | The rate limit for the API key has been exceeded. See the `Retry-After` header |
| `500` | Internal Server Error | An unexpected error occurred on the server. These are logged automatically. If they persist, contact support |

**401 vs 403**

A `401 Unauthorized` response means the API key could not be authenticated at all — it is missing, expired, or revoked. A `403 Forbidden` response means the key authenticated successfully but the associated scopes do not include permission for the requested operation. To resolve a `403`, issue a new key that includes the required scope, or update the existing key's scopes via `PATCH /api-keys/{id}`.

**Validation Errors**

When a `400` is returned due to a schema validation failure, the `message` field identifies the offending field:

```json
{
  "success": false,
  "message": "cnrNumber: CNR number must be exactly 16 characters",
  "moreInfo": "No additional info found."
}
```

Correct the field value described in `message` and resubmit the request.
