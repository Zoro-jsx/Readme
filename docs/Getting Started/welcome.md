---
title: Welcome
hidden: false
---

# Welcome to the Court Record Platform

Welcome to the official developer hub for the **Court Record Platform**! Our API gateway provides real-time access to query, track, and monitor court case details, litigation histories, and upcoming hearing calendars across Indian district courts, state high courts, and the Supreme Court of India.

---

## What You Can Do with the Platform

* **Real-time Case Search**: Locate court cases dynamically by petitioner, respondent, advocate, judge name, or filing number.
* **Direct CNR Details Retrieval**: Fetch the complete expanded history, status, and advocate calendars using a single, unique Case National Record (CNR) number.
* **Automated Live Refreshes**: Trigger background workers to scrape and pull the absolute latest live updates directly from eCourts.
* **Platform Credit Wallet**: Manage prepaid credit packages, top up balances programmatically, and query transaction histories.

---

## Quick Navigation

Get started with your integration using these resources:

<div style="display: flex; flex-direction: row; gap: 20px; flex-wrap: wrap; margin-bottom: 20px;">
  <div style="flex: 1; min-width: 250px; border: 1px solid rgba(120, 120, 120, 0.2); border-radius: 8px; padding: 16px; background-color: rgba(120, 120, 120, 0.05);">
    <h3 style="margin-top: 0;">🚀 <a href="/docs/getting-started">Getting Started</a></h3>
    <p style="margin-bottom: 0;">Learn the basic workflow, set up your development environment, and make your first API request.</p>
  </div>
  <div style="flex: 1; min-width: 250px; border: 1px solid rgba(120, 120, 120, 0.2); border-radius: 8px; padding: 16px; background-color: rgba(120, 120, 120, 0.05);">
    <h3 style="margin-top: 0;">🔑 <a href="/docs/authentication">Authentication</a></h3>
    <p style="margin-bottom: 0;">Authenticate using Bearer JWT tokens for web portals, or secure API Keys for programmatic background scripts.</p>
  </div>
</div>
<div style="display: flex; flex-direction: row; gap: 20px; flex-wrap: wrap; margin-bottom: 20px;">
  <div style="flex: 1; min-width: 250px; border: 1px solid rgba(120, 120, 120, 0.2); border-radius: 8px; padding: 16px; background-color: rgba(120, 120, 120, 0.05);">
    <h3 style="margin-top: 0;">⚡ <a href="/docs/rate-limits-metering">Rate Limits & Metering</a></h3>
    <p style="margin-bottom: 0;">Understand request rate limits, credit pools (subscription vs top-up), and the credit rate per API call.</p>
  </div>
  <div style="flex: 1; min-width: 250px; border: 1px solid rgba(120, 120, 120, 0.2); border-radius: 8px; padding: 16px; background-color: rgba(120, 120, 120, 0.05);">
    <h3 style="margin-top: 0;">🔍 <a href="/docs/search-syntax">Search Syntax</a></h3>
    <p style="margin-bottom: 0;">Master the search parameters, required conditions, and court filtering rules for case searches.</p>
  </div>
</div>


---

## Core API References

Once you have uploaded the OpenAPI spec, you can try out live endpoints in the interactive reference panel:

| Area | Resource Path | Primary Method | Description |
| :--- | :--- | :--- | :--- |
| **Case Search** | `/case-search` | `POST` | Find case summaries across all courts. |
| **Case Detail** | `/case-detail/searchByCnr` | `POST` | Retrieve full case history, judges, and hearings. |
| **Case Refresh**| `/case-refresh` | `POST` | Enqueue a case for live updates from eCourts. |
| **API Keys** | `/api-keys` | `POST`, `GET` | Create, list, rotate, or revoke API access tokens. |
| **Wallet** | `/wallet` | `GET`, `POST` | Monitor your prepaid balance and trigger top-ups. |

---

## Need Support?
* **Developer Dashboard**: Log in to view your credentials, API usage, and billing history.
* **API Status Page**: Check the health and uptime of our scraper workers and endpoints.
* **Technical Support**: Have questions about our scraper or case schema? Email us at `developer-support@yourcompany.com`.
