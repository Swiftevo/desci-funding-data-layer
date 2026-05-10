# ID System — DeSci Funding Data Layer

Version: V1

---

# Overview

This document defines the canonical identifier system used across the DeSci Funding Data Layer.

The ID system is designed for:

* long-term stability
* machine readability
* cross-round interoperability
* future API compatibility
* ecosystem-scale indexing

---

# Core Principles

## IDs must be:

* stable
* permanent
* non-semantic
* machine-friendly
* human-readable
* independent from platform naming

---

# 1. Project Entity ID

Represents the permanent identity of a project.

Format:

DSPJ-0001

Meaning:

| Component | Meaning                  |
| --------- | ------------------------ |
| DSPJ      | DeSci Project            |
| 0001      | Sequential entity number |

---

## Rules

* One permanent ID per project
* Same project keeps the same ID across all funding rounds
* IDs never recycled
* IDs remain stable even if project name changes

---

## Examples

| Project              | ID        |
| -------------------- | --------- |
| DeSci Asia           | DSPJ-0031 |
| FunDeSci             | DSPJ-0048 |
| InfiniteZero Network | DSPJ-0027 |

---

# 2. Funding Round ID

Represents a funding round or grant ecosystem.

Format:

FR-ART-S6

Meaning:

| Component | Meaning            |
| --------- | ------------------ |
| FR        | Funding Round      |
| ART       | Platform shorthand |
| S6        | Season 6           |

---

## Examples

| Round            | ID          |
| ---------------- | ----------- |
| Artizen Season 6 | FR-ART-S6   |
| Gitcoin GG23     | FR-GTC-GG23 |
| Giveth QF Round  | FR-GIV-QF01 |

---

# 3. Participation ID

Represents a unique participation instance.

Format:

DSPT-00001

Meaning:

| Component | Meaning                         |
| --------- | ------------------------------- |
| DSPT      | DeSci Participation             |
| 00001     | Sequential participation number |

---

## Rules

* Every participation receives a unique ID
* Same project entering multiple rounds gets multiple participation IDs
* Participation IDs are immutable

---

# Participation Model

Example:

| project_entity_id | funding_round_id | participation_id |
| ----------------- | ---------------- | ---------------- |
| DSPJ-0031         | FR-ART-S6        | DSPT-00031       |
| DSPJ-0031         | FR-GTC-GG24      | DSPT-00120       |

This allows:

* multi-round participation tracking
* funding analytics
* ecosystem mapping
* longitudinal research

---

# Reserved Future IDs

Future schema versions may include:

| Prefix | Purpose      |
| ------ | ------------ |
| DSRV   | Reviewer     |
| DSDN   | Donor        |
| DSOR   | Organization |
| DSEV   | Event        |
| DSTG   | Tag ontology |

These are intentionally excluded from V1 implementation.

---

# Naming Philosophy

IDs are intentionally:

* short
* neutral
* platform-independent
* future-compatible

The system avoids embedding:

* project categories
* chains
* countries
* domains
* funding outcomes

inside the IDs themselves.

This ensures long-term schema flexibility.
