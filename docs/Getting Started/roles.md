---
title: Access Control & Roles
hidden: false
---

# Access Control & Roles

To ensure security and proper delegation of capabilities, the Court Record Platform API enforces a Role-Based Access Control (RBAC) model. 

Every user account or API key is assigned to a specific role, which determines the set of API actions and resources they are allowed to access.

---

## System Roles & Privileges

The platform defines three default system roles. These system roles are protected and cannot be deleted or modified.

| Role | Description | Key System Privileges |
| :--- | :--- | :--- |
| **Client** | Standard consumer of the platform (e.g. legal tech integrations, corporate compliance teams). | Search cases, retrieve CNR details, view search history, manage personal API Keys, monitor credit wallet, and purchase plans. |
| **Lawyer** | Legal professional or firm requiring write privileges and deep analytics. | All Client privileges + trigger scrape updates (refreshes) on court cases, upload and manage case documents, and access write/export analytics. |
| **Administrator** | Platform owner or supervisor with global access. | All lawyer privileges + full system management (manage users, plans, billing packages, custom roles, pricing structures, and system configurations). |

---

## Permissions & Scope Table

When generating an API Key, you can limit its scope by choosing a subset of the permissions allowed by your user role. The default permissions mapped to each system role include:

### 1. Case & Scraper Management
* **`read:cases`**: Query cases via `/case-search` and `/case-detail`. *(Client, Lawyer, Admin)*
* **`write:cases`**: Scrape, refresh, or update case details on the platform. *(Lawyer, Admin)*
* **`read:documents`**: View court-related documents or uploaded case summaries. *(Client, Lawyer, Admin)*
* **`write:documents`**: Upload new PDFs or evidentiary case files. *(Lawyer, Admin)*
* **`read:courtStructure`**: Retrieve listing guides for states, districts, and establishments. *(Client, Lawyer, Admin)*
* **`read:recentSearches`** / **`delete:recentSearches`**: Access or clear the history of search terms. *(Client, Lawyer, Admin)*

### 2. API Credentials & Analytics
* **`read:apiKeys`** / **`write:apiKeys`** / **`delete:apiKeys`**: Manage programmatic access credentials. *(Client, Lawyer, Admin)*
* **`read:analytics`**: Retrieve personal endpoint usage statistics. *(Client, Lawyer, Admin)*
* **`write:analytics`**: Configure advanced analytical dashboards or export metrics. *(Lawyer, Admin)*

### 3. Credit Pool & Wallet
* **`read:wallet`** / **`write:wallet`**: Query credit balance, top-up histories, and verify Razorpay orders. *(Client, Lawyer, Admin)*
* **`read:billing`**: Retrieve invoices and billing receipts. *(Client, Lawyer, Admin)*
* **`read:packages`** / **`read:plans`**: View available credit tiers and subscription models. *(Client, Lawyer, Admin)*
* **`read:subscriptions`** / **`write:subscriptions`**: Initiate, cancel, or switch recurring plans. *(Client, Lawyer, Admin)*

---

## Dynamic Access Checks

When an API request is made, the platform's authorization layer performs the following validation:
1. **Token Verification**: Ensures the Bearer JWT or API Key is valid and active.
2. **Permission Match**: Checks if the matched endpoint requires a permission (e.g. `write:cases` for `/case-refresh`) and ensures the token holds that scope.
3. **Admin Exemption**: Users holding the `admin` role bypass path-specific permissions automatically via the `manage:all` override.
