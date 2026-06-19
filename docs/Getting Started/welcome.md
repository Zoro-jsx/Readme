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

* **🚀 [Getting Started](getting-started)**: Learn the basic workflow, set up your development environment, and make your first API request.
* **🔑 [Authentication](authentication)**: Authenticate using Bearer JWT tokens for web portals, or secure API Keys for programmatic background scripts.
* **⚡ [Rate Limits & Metering](rate-limits-metering)**: Understand request rate limits, credit pools (subscription vs top-up), and the credit rate per API call.
* **🔍 [Search Syntax](search-syntax)**: Master the search parameters, required conditions, and court filtering rules for case searches.


---

## Core API References

You can test these endpoints dynamically in the interactive API reference playground:

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
