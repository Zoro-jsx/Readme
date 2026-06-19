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

All programmatic requests to the Court Record Platform API are authenticated using **API Keys**. 

---

## 1. Authentication Header (API Keys)

API Keys must be passed in the HTTP `Authorization` header as a Bearer token:

```http
Authorization: Bearer <api_key>
```

### Example Request
```bash
curl -X POST https://api.yourcompany.com/api/v1/case-search \
  -H "Authorization: Bearer cr_live_xyz789payg123456..." \
  -H "Content-Type: application/json" \
  -d '{
    "petitioner": "Tata Motors",
    "year": 2023
  }'
```

---

## 2. API Key Management

API Keys can be generated, managed, rotated, and revoked directly within the user settings panel of the **Developer Portal Dashboard**:

1. Log in to the Developer Portal.
2. Navigate to **Settings > API Keys**.
3. Click **Generate New Key**.
4. Give it a descriptive name and select the required permission scopes (e.g., `cases:read`).
5. Copy the plain key string immediately. It will only be shown once for security reasons.

If an API Key is compromised, you can revoke or rotate it instantly via the dashboard to protect your wallet balance and data access.
