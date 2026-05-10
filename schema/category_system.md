# Category System — DeSci Funding Data Layer

Version: V1

---

# Overview

This document defines the V1 category system used to classify DeSci funding projects.

The category system is designed to support:

* human review
* AI retrieval
* ecosystem mapping
* future analytics
* cross-round comparison

---

# Layer A — Project Type

Project Type describes what the project fundamentally is.

## Canonical Values

* Infrastructure
* Research
* Product
* Community
* Education
* Media / Narrative
* Funding Mechanism
* Platform
* Experimental / Speculative

---

# Layer B — Domain

Domain describes the main field or ecosystem area of the project.

## Canonical Values

* Biotech / Health
* Environment / Climate
* AI / Data
* Space / Physics
* Social / Community
* Education
* Agriculture
* Ocean / Marine
* Governance / DAO
* Art / Culture
* General / Meta

---

# Layer C — Function

Function describes what the project actually does.

## Canonical Values

* Data Collection
* Data Infrastructure
* Research Generation
* Knowledge Sharing
* Funding
* Community Building
* Education
* Tooling
* Marketplace
* Identity
* Experimentation
* Simulation
* Storytelling
* Coordination
* Publishing
* Automation
* Evaluation
* Training
* Discovery
* Standardization
* Regeneration
* Treatment
* Prediction
* Data Ownership
* Advocacy
* Citizen Science
* Analysis

---

# Classification Principles

## 1. Prefer functional clarity over hype

Classify projects based on what they do, not only what they claim.

---

## 2. Use multi-select when necessary

A project may belong to more than one type, domain, or function.

Example:

A project that combines AI tools and biotech research may use:

* Project Type: Platform
* Domain: AI / Data, Biotech / Health
* Function: Data Infrastructure, Research Generation

---

## 3. Do not create new categories casually

New category values should only be introduced when existing values are insufficient.

This prevents fragmentation such as:

* AI
* ai
* Artificial Intelligence
* A.I.

---

# Future Notes

Future schema versions may introduce:

* confidence scores
* evidence weighting
* ontology mappings
* cross-round category normalization
* ecosystem cluster analysis

These are intentionally excluded from V1.
