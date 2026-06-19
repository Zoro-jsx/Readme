---
title: Roles
hidden: false
---

**Roles**

Every account on the Court Record Platform is assigned a single role that determines which resources and operations are accessible. Roles exist at the account level and apply across all API keys generated under that account. An API key can be granted any subset of the permissions its parent account role permits — but never more.

**The Three Roles**

**Client**

The standard role for legal technology companies, compliance teams, and individual developers consuming court record data. A Client account can search cases, retrieve full case details, browse the court directory, manage its own API keys, and monitor its credit balance and transaction history.

**Lawyer**

An extended role for legal professionals and law firms that require the ability to keep case data current. In addition to all Client capabilities, a Lawyer account may trigger live data refreshes for specific cases, ensuring that hearing dates, case status, and order information reflect the most recent available state.

**Admin**

The platform management role, reserved for platform operators. Admin accounts have unrestricted access across all resources and can manage users, subscription plans, credit packages, and endpoint pricing. Admin operations are not part of the public API and are not documented in this reference.

**API Key Scopes**

When generating an API key, you select which permission scopes to attach. A key can only carry scopes that your account role permits. Granting a key a narrower scope than your account allows is good security practice — especially for keys used in automated pipelines or shared environments.

| Scope | Permission |
| :--- | :--- |
| `cases:read` | Search cases and retrieve full case records |
| `cases:write` | Trigger live data refreshes for cases |
| `api-keys:read` | List API keys on the account |
| `api-keys:write` | Create, update, rotate, and revoke API keys |
| `wallet:read` | View credit balance and transaction history |
