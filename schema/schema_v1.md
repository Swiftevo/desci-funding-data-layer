# Schema V1 — DeSci Funding Data Layer

Version: V1
Status: Schema Freeze
Date: 2026-05

---

# Overview

This document defines the V1 schema architecture for the DeSci Funding Data Layer.

The system is designed to:

* preserve decentralized science funding data
* support multi-round participation tracking
* maintain stable machine-readable identifiers
* support future interoperability across ecosystems

---

# Core Architecture

The schema uses a three-layer identity model:

## 1. Project Entity Layer

Represents the permanent identity of a project.

Example:

DSPJ-0001

A project entity may participate in multiple funding rounds across different ecosystems.

---

## 2. Funding Round Layer

Represents a funding round or grant program.

Example:

FR-ART-S6

A funding round contains many project participations.

---

## 3. Participation Layer

Represents a single participation instance of a project within a funding round.

Example:

DSPT-00001

This is the primary operational tracking layer for funding analytics.

---

# Property Structure

## Identity Layer

| Property          | Type |
| ----------------- | ---- |
| project_entity_id | text |
| funding_round_id  | text |
| participation_id  | text |

---

## Core Project Layer

| Property     | Type         |
| ------------ | ------------ |
| Project name | title        |
| Link         | url          |
| Round        | select       |
| Season       | select       |
| Status       | select       |
| Region       | multi-select |

---

## Classification Layer

| Property      | Type         |
| ------------- | ------------ |
| Project type  | multi-select |
| Domain        | multi-select |
| Function      | multi-select |
| Category      | multi-select |
| Problem type  | multi-select |
| Solution type | multi-select |
| Target user   | multi-select |
| Tags          | multi-select |

---

## Content Layer

| Property            | Type |
| ------------------- | ---- |
| What are you making | text |
| Impact              | text |
| Progress            | text |
| Why you             | text |
| raw_text            | text |
| Summary (AI)        | text |

---

## Evaluation Layer

| Property          | Type   |
| ----------------- | ------ |
| DeSci alignment   | number |
| Evidence level    | select |
| Narrative clarity | number |
| Risk flag         | select |
| Fundability score | number |
| Impact score      | number |
| Execution score   | number |

---

## Funding Layer

| Property             | Type   |
| -------------------- | ------ |
| raised_amount_usd    | number |
| requested_amount_usd | number |
| matching_amount_usd  | number |
| donor_count          | number |
| vote_count           | number |
| funding_rank         | number |

---

# Preservation Principles

## Raw Text Preservation

The field:

raw_text

stores original application content without compression or summarization.

This layer is preserved for:

* historical archiving
* AI retrieval
* future embeddings
* narrative analysis
* ecosystem research

---

# Source of Truth

GitHub is the canonical archive layer.

Notion serves as the human-facing management interface.

---

# Future Expansion

Future versions may include:

* reviewer layers
* contributor graphs
* funding analytics
* AI retrieval systems
* API integrations
* vector databases
* knowledge graphs

These are intentionally excluded from V1 to maintain schema stability.

---

# V1 Freeze Notes

The V1 schema prioritizes:

* simplicity
* interoperability
* long-term stability
* machine readability
* archival durability

Major structural changes should occur only in future schema versions.
