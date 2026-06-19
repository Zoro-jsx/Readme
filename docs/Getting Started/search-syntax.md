---
title: Search Syntax
excerpt: >-
  The case search endpoint (`POST /case-search`) allows you to find case
  summaries across district, high, and supreme courts.
deprecated: false
hidden: false
metadata:
  robots: index
---

# Search Syntax

The case search endpoint (`POST /case-search`) allows you to find case summaries across district, high, and supreme courts.

---

## Query Validation Constraints

To perform a search, **at least one** of the following core search parameters must be provided:

* `petitioner`
* `respondent`
* `litigant`
* `advocate`
* `judge`
* `filingNumber`
* `firNumber`

If a search is submitted with all of these fields empty or omitted, the API will return a validation failure (`400 Bad Request`).

---

## Filter Options

You can narrow your queries by combining the search parameters with optional location and time filters:

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `year` | `number` | The filing year of the case. | `2023` |
| `state` | `string` | Hierarchical State code of the court. | `"MH"` (Maharashtra) |
| `district` | `string` | District code under the specified state. | `"PUNE"` |
| `complex` | `string` | Specific court complex code. | `"MHPN01"` |
| `courtType` | `string` | Level filter: `"district"`, `"high"`, or `"supreme"`. | `"district"` |

---

## Search Examples

### 1. Search by Petitioner in a Specific State
```json
{
  "petitioner": "Tata Motors",
  "state": "MH",
  "year": 2022
}
```

### 2. Search by Advocate across High Courts
```json
{
  "advocate": "Abhishek Manu Singhvi",
  "courtType": "high"
}
```

### 3. Search by FIR Number in a District Court
```json
{
  "firNumber": "120/2021",
  "state": "MH",
  "district": "PUNE"
}
```
