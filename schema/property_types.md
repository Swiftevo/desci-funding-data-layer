# Property Types — DeSci Funding Data Layer

Version: V1

---

# Overview

This document defines the canonical property types used in the Notion database and structured exports.

The schema is optimized for:

* Notion compatibility
* CSV imports
* JSON exports
* AI readability
* future API interoperability

---

# Identity Properties

| Property          | Type |
| ----------------- | ---- |
| project_entity_id | Text |
| funding_round_id  | Text |
| participation_id  | Text |

---

# Core Properties

| Property     | Type         |
| ------------ | ------------ |
| Project name | Title        |
| Link         | URL          |
| Round        | Select       |
| Season       | Select       |
| Status       | Select       |
| Region       | Multi-select |

---

# Classification Properties

| Property      | Type         |
| ------------- | ------------ |
| Project type  | Multi-select |
| Domain        | Multi-select |
| Function      | Multi-select |
| Category      | Multi-select |
| Problem type  | Multi-select |
| Solution type | Multi-select |
| Target user   | Multi-select |
| Tags          | Multi-select |

---

# Content Properties

| Property            | Type |
| ------------------- | ---- |
| What are you making | Text |
| Impact              | Text |
| Progress            | Text |
| Why you             | Text |
| raw_text            | Text |
| Summary (AI)        | Text |

---

# Evaluation Properties

| Property          | Type   |
| ----------------- | ------ |
| DeSci alignment   | Number |
| Evidence level    | Select |
| Narrative clarity | Number |
| Risk flag         | Select |
| Fundability score | Number |
| Impact score      | Number |
| Execution score   | Number |

---

# Funding Properties

| Property             | Type   |
| -------------------- | ------ |
| raised_amount_usd    | Number |
| requested_amount_usd | Number |
| matching_amount_usd  | Number |
| donor_count          | Number |
| vote_count           | Number |
| funding_rank         | Number |

---

# Notes

## Text Fields

Long-form content fields use Text properties to maximize:

* import stability
* AI parsing
* multiline compatibility
* archival durability

---

## Multi-select Usage

Multi-select is preferred for:

* interoperability
* future ontology expansion
* ecosystem mapping
* AI retrieval flexibility

---

# Schema Freeze

This property structure is frozen under Schema V1.

Major structural changes should occur only in future schema versions.
