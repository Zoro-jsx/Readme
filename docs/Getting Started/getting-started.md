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

The API is versioned to ensure stability. The base URL for all programmatic requests is:

| Version | Base URL | Description |
| :--- | :--- | :--- |
| **Version 1** | `https://api.yourcompany.com/api/v1` | Main stable version for all public features. |

---

## Basic Integration Workflow

Integrating with the Court Record Platform typically involves these simple steps:

```mermaid
graph TD
    A[Generate API Key in Portal] --> B[Verify Wallet Balance]
    B --> C[Run Case Search]
    C --> D[Fetch Case Detail / CNR]
```

### 1. Generate API Key
To authenticate your programmatic requests, log in to the developer portal dashboard using your credentials, navigate to **Settings > API Keys**, and generate a new API Key with the required scopes (e.g., `cases:read`).

> [!WARNING]
> Copy the returned `plainKey` immediately. It is only shown once at creation and cannot be retrieved again.

### 2. Make Your First Query
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
