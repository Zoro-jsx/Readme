---
title: Error Handling
excerpt: >-
  The Court Record Platform API returns standard HTTP status codes to indicate
  the success or failure of an API request. In addition, error responses contain
  a structured JSON body to help developers debug issues.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Error Response Schemas

### 1. General Error Response (`ErrorResponse`)

Returned for authentication, authorization, not found, or server errors:

```json
{
  "success": false,
  "message": "Error message details",
  "moreInfo": "Additional debug context or details."
}
```

- `success` (boolean): Always `false`.
- `message` (string): A readable explanation of what went wrong.
- `moreInfo` (string): Optional additional debug details (defaults to `"No additional info found."`).

***

### 2. Validation Error Response (`ValidationErrorResponse`)

Returned when request parameters, query values, or request bodies fail validation (HTTP `400`):

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email address"
    }
  ],
  "moreInfo": "No additional info found."
}
```

- `errors` (array): Detailed list of each field that failed validation.
  - `field` (string): The path parameter, query key, or body property name.
  - `message` (string): Reason for the validation check failure.

***

## HTTP Status Codes Reference

The API uses the following HTTP response status codes:

| Code  | Status                  | Description / Common Triggers                                                     |
| :---- | :---------------------- | :-------------------------------------------------------------------------------- |
| `200` | `OK`                    | Request succeeded. Response body contains requested resources.                    |
| `201` | `Created`               | Resource created successfully (e.g. subscription initiated, custom role created). |
| `400` | `Bad Request`           | Validation failure. Check body fields, query parameters, or route parameters.     |
| `401` | `Unauthorized`          | Missing or invalid authorization token (JWT cookies or API key header).           |
| `403` | `Forbidden`             | Authenticated, but user lacks administrative permissions for that resource.       |
| `404` | `Not Found`             | The requested resource (case detail, API key, notification, plan) does not exist. |
| `409` | `Conflict`              | Resource conflict (e.g. email already registered, plan already active).           |
| `422` | `Unprocessable Entity`  | Business logic constraints violated (e.g. pricing syncing errors).                |
| `429` | `Too Many Requests`     | Rate limit exceeded. Back off and wait before retrying.                           |
| `500` | `Internal Server Error` | An unexpected error occurred on our servers. Contact support.                     |

<br />
