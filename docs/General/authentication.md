---
title: Authentication
excerpt: >-
  The Court Record Platform API supports two authentication mechanisms designed
  for different application architectures.
deprecated: false
hidden: false
metadata:
  robots: index
---

**Authentication**

All endpoints in the Court Record Platform API require authentication. Authentication is performed by including an API key in the `Authorization` header of every request.

**The Authorization Header**

```http
Authorization: Bearer <your_api_key>
```

The API key is prefixed with `cr_live_` for production keys and `cr_test_` for sandbox keys. Including the full string — prefix and random characters — is required.

**Example**

```bash
curl -X POST https://api.courtrecordplatform.in/api/v1/case-detail/searchByCnr \
  -H "Authorization: Bearer cr_live_abc123xyz789" \
  -H "Content-Type: application/json" \
  -d '{ "cnrNumber": "MHPN010123456789" }'
```

**Key Management**

API keys are created and managed through the Developer Portal under **Settings → API Keys**, or programmatically via the `/api-keys` endpoints. The table below summarises the available operations.

| Operation | Method | Endpoint |
| :--- | :--- | :--- |
| Create a key | `POST` | `/api-keys` |
| List all keys | `GET` | `/api-keys` |
| Get a key | `GET` | `/api-keys/{id}` |
| Update name or scopes | `PATCH` | `/api-keys/{id}` |
| Rotate a key | `POST` | `/api-keys/{id}/rotate` |
| Revoke a key | `DELETE` | `/api-keys/{id}` |

Rotating a key immediately invalidates the existing key and issues a replacement with identical configuration. The new plain key is returned in the rotation response and displayed only once.

**Security Practices**

Keep API keys out of source code and version control. Use environment variables or a dedicated secrets manager to inject keys at runtime. Assign each integration its own key with the minimum scopes needed for that integration. Revoke keys that are no longer in use and rotate keys periodically as part of routine security hygiene.
