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

# Authentication

The Court Record Platform API supports two authentication mechanisms designed for different application architectures.

---

## 1. Web Portal Authentication (JWT Cookies)
If you are building a frontend application that interacts with our user interface directly, authentication is handled via JSON Web Tokens (JWT) stored in HTTP-only, secure cookies (`accessToken` and `refreshToken`).

* Cookies are automatically set upon a successful call to `/auth/login` or `/auth/verify-otp`.
* Standard endpoints require the browser to automatically include these cookies on every request.
* To check if your session is active, call:
  ```bash
  curl -X GET https://api.yourcompany.com/api/v1/auth/status
  ```

---

## 2. Programmatic Integrations (API Keys)
If you are integrating our services into a background cron job, server-side system, or backend application, you should authenticate using an **API Key**.

### Authorization Header Format
API Keys must be passed in the HTTP `Authorization` header as a Bearer token:

```http
Authorization: Bearer <api_key>
```

#### Example Request
```bash
curl -X GET https://api.yourcompany.com/api/v1/wallet \
  -H "Authorization: Bearer cr_live_xyz789payg123456..."
```

---

## API Key Management & Lifecycle

You can manage your API keys via our API key management endpoints:

### Generate a Key
Generate a new API key by specifying a human-readable name and permissions scopes:

```bash
curl -X POST https://api.yourcompany.com/api/v1/api-keys \
  -H "Authorization: Bearer <your_jwt_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Cron Job Search Key",
    "scopes": ["cases:read"]
  }'
```

### Revoke a Key
If a key is leaked or no longer needed, you can delete it immediately to revoke access:

```bash
curl -X DELETE https://api.yourcompany.com/api/v1/api-keys/64b8f1a2c3d4e5f6a7b8c9d0 \
  -H "Authorization: Bearer <your_jwt_token>"
```

### Rotate a Key
To cycle a key (generate a new plain token while keeping the same configuration), call the rotate endpoint:

```bash
curl -X POST https://api.yourcompany.com/api/v1/api-keys/64b8f1a2c3d4e5f6a7b8c9d0/rotate \
  -H "Authorization: Bearer <your_jwt_token>"
```
