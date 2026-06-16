# Schema V1.5 — DeSci Funding Data Layer

Version: V1.5  
Status: Draft for implementation  
Date: 2026-05

---

## Overview

Schema V1.5 extends the V1 DeSci Funding Data Layer from a single-round archive into a project-centric, multi-round funding data model.

V1.5 does not replace V1. It preserves the V1 identity model:

```text
Project Entity
Funding Round
Participation
```

and expands it into a relational structure that can support:

- Spark funding rounds
- Gitcoin DeSci community rounds
- cross-round project identity
- project participation history
- donation graph analysis
- anonymized review records
- AI-readable public archives

---

## Core Model

V1.5 uses three primary entity tables:

```text
projects
funding_rounds
participations
```

These are the first-phase Notion databases.

V1.5 also defines three analysis tables:

```text
donations
donors
reviews
```

These are stored in GitHub first and are not required in Notion Phase 1.

Related V1.5 extension documents:

```text
schema/id_system_v1_5.md
schema/category_system_v1_5.md
schema/property_types_v1_5.md
schema/entity_tables_v1_5.md
schema/donation_system.md
schema/review_system.md
schema/public_private_fields.md
```

---

## Conceptual Layers

```text
Projects = ecosystem identity
Funding Rounds = funding context
Participations = project-round history
Donations = funding graph
Donors = wallet identity graph
Reviews = evaluation history
```

---

## Project Entity Layer

A project entity represents a long-term DeSci project identity.

Rules:

- One real project should have one stable `project_entity_id`.
- Project IDs are not tied to any platform, round, wallet, or project name.
- Project names may change; the `project_entity_id` remains stable.
- Platform-specific names are stored as source names or aliases.

Example:

```text
DSPJ-0029 = DeSci Asia
```

---

## Funding Round Layer

A funding round represents a funding event or grant program.

Examples:

```text
FR-ART-S6
FR-GTC-GG23-DESCI
FR-GTC-GG21-DESCI
```

Rules:

- One funding round receives one stable `funding_round_id`.
- Round metadata is stored separately from project data.
- Round-level project count, donor count, and matching pool belong here.

---

## Participation Layer

A participation represents one project participating in one funding round.

Rules:

- One project in one round receives one `participation_id`.
- The same project can have many participations across multiple rounds.
- Round-specific application content, review outcome, and funding result belong here.

Example:

```text
project_entity_id: DSPJ-0029
funding_round_id: FR-GTC-GG23-DESCI
participation_id: DSPT-00120
```

---

## Analysis Layers

### Donations

The donations table preserves individual Gitcoin donation or vote events.

It supports:

- donor graph analysis
- repeat donor analysis
- anti-sybil research
- quadratic funding analysis
- cross-round donor behavior

### Donors

The donors table aggregates wallet-level donor identities.

Wallet addresses may be public because they are required for funding graph and anti-sybil analysis.

### Reviews

The reviews table preserves reviewer scores without exposing reviewer real names.

Reviewer identities are anonymized in public exports.

---

## Public Archive Policy

Public archive excludes:

```text
Email Address
Telegram username
reviewer real names
private notes
```

Public archive may include:

```text
project name
website
project Twitter
project GitHub
user GitHub
payout address
donor wallet
grant address
raw application text
donation amount
anonymized reviewer scores
funding result
```

---

## Matching Policy

Cross-round project matching uses the following statuses:

```text
provisional
confirmed
rejected
new_project
```

AI or scripts may suggest matches. Human confirmation is required before a match becomes canonical.

Recommended confirmation fields:

```text
confirmed_by
confirmed_at
match_notes
```

---

## Implementation Order

```text
1. Build V1.5 schema
2. Split Spark S6 into projects / funding_rounds / participations
3. Import Gitcoin GG23
4. Match Spark/GG23 projects
5. Build donations/reviews public archive
6. Backfill GG21
7. Backfill GG20
8. Backfill Beta
9. Backfill GR15
```
