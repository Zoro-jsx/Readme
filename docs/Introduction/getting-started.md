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

**Getting Started**

This guide walks through everything required to make your first authenticated API call to the Court Record Platform. The process takes fewer than five minutes.

**Base URL**

All API requests are made to the following base URL:

```
https://api.courtrecordplatform.in/api/v1
```

**Creating an API Key**

1. Log in to the [Developer Portal](https://courtrecordplatform.in)
2. Navigate to **Settings → API Keys**
3. Click **Generate New Key**
4. Enter a descriptive name for the key (for example, "Production Integration" or "CI Pipeline")
5. Select the permission scopes required for your use case
6. Click **Generate** and copy the `plainKey` value immediately

> The plain key value is displayed exactly once at creation time and cannot be retrieved afterwards. Store it in a secrets manager or environment variable before closing the dialog. If a key is lost, rotate it immediately from the dashboard.

**Making Your First Request**

Pass the API key as a Bearer token in the `Authorization` header on every request.

```bash
curl -X POST https://api.courtrecordplatform.in/api/v1/case-search \
  -H "Authorization: Bearer cr_live_yourKeyHere" \
  -H "Content-Type: application/json" \
  -d '{
    "petitioner": "State of Maharashtra",
    "year": 2024
  }'
```

A successful response returns a paginated list of matching case summaries along with faceted counts for status, state, and case type.

**Next Steps**

Once authentication is working, the natural progression is:

1. Use [Case Search](reference/case-search) to locate cases by party name, advocate, judge, or FIR number
2. Use [Case Detail](reference/case-detail) with a `cnrNumber` from search results to retrieve the full case record
3. Use [Case Refresh](reference/case-refresh) to keep case data current for cases you are actively monitoring
