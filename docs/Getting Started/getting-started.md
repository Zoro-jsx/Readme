---
title: Getting Started
excerpt: >-
  Welcome to the **Court Record Platform API**! This API allows developers to
  programmatically search court cases, monitor case hearings, track case
  progression, and automate data retrieval from Indian district courts, high
  courts, and the supreme court
deprecated: false
hidden: false
metadata:
  robots: index
---

# Getting Started

Welcome to the **Court Record Platform API**! This API allows developers to programmatically search court cases, monitor case hearings, track case progression, and automate data retrieval from Indian district courts, high courts, and the supreme court.

---

## Base URLs

The API is versioned to ensure stability. Base URLs are relative to your deployment domain:

| Version | Base URL | Description |
| :--- | :--- | :--- |
| **Version 1** | `https://api.yourcompany.com/api/v1` | Main stable version for current features. |
| **Version 2** | `https://api.yourcompany.com/api/v2` | Advanced version containing breaking changes (e.g. restructured user data model). |

---

## Basic Workflow

Integrating with the API typically involves these steps:

```mermaid
graph TD
    A[Get Credentials] --> B[Authenticate]
    B --> C[Verify Wallet Balance]
    C --> D[Run Case Search]
    D --> E[Fetch Case Detail / CNR]
```

### 1. Register & Login (For Web/Portal Apps)
If you are building a web application using user credentials, first register and authenticate to get your session token:

```bash
curl -X POST https://api.yourcompany.com/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "developer@example.com",
    "password": "SecurePassword123!",
    "firstName": "John",
    "lastName": "Doe"
  }'
```

After verifying the OTP sent to your email, log in to set HTTP-only authentication cookies:

```bash
curl -X POST https://api.yourcompany.com/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "developer@example.com",
    "password": "SecurePassword123!"
  }'
```

### 2. Generate API Keys (For Programmatic/Server Apps)
If you are building server-side automation tools, log into the developer portal, go to your Profile settings, and call the API Key generation endpoint to get your API Token:

```bash
curl -X POST https://api.yourcompany.com/api/v1/api-keys \
  -H "Authorization: Bearer <your_jwt_token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Production Automation Key",
    "scopes": ["cases:read", "cases:write"]
  }'
```

> [!WARNING]
> Copy the returned `plainKey` immediately. It is only shown once at creation and cannot be retrieved again.

### 3. Make Your First Query
Use your API Key (passed as a Bearer token in the `Authorization` header) to run a case search:

```bash
curl -X POST https://api.yourcompany.com/api/v1/case-search \
  -H "Authorization: Bearer cr_live_yourPlainKeyHere" \
  -H "Content-Type: application/json" \
  -d '{
    "petitioner": "State of Maharashtra",
    "year": 2023
  }'
```
