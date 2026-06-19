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

## API Scopes & Permissions

When generating an API Key, you can limit its scope by choosing a subset of the permissions allowed by your user role:

* **`cases:read`**: Permission to search cases and query case details or court structures. *(Allowed for: Client, Lawyer, Admin)*
* **`cases:write`**: Permission to trigger live scraper refreshes on cases. *(Allowed for: Lawyer, Admin)*
* **`api-keys:read` / `api-keys:write`**: Permission to view, create, rotate, or revoke your API Keys. *(Allowed for: Client, Lawyer, Admin)*
* **`wallet:read`**: Permission to check prepaid credit balance and transaction logs. *(Allowed for: Client, Lawyer, Admin)*

---

## Dynamic Access Checks

When an API request is made, the platform's authorization layer performs the following validation:
1. **Token Verification**: Ensures the Bearer JWT or API Key is valid and active.
2. **Permission Match**: Checks if the matched endpoint requires a permission (e.g. `write:cases` for `/case-refresh`) and ensures the token holds that scope.
3. **Admin Exemption**: Users holding the `admin` role bypass path-specific permissions automatically via the `manage:all` override.
