# DeSci Funding Data Layer V1.5 Implementation Plan

Status: confirmed implementation plan  
Date: 2026-05-30

---

## Goal

Upgrade the DeSci Funding Data Layer from a single-round archive into a project-centric, multi-round data layer covering Spark and Gitcoin DeSci community rounds.

V1.5 extends V1. It does not replace it.

---

## Confirmed Decisions

Notion Phase 1 uses only three databases:

```text
Projects
Funding Rounds
Participations
```

GitHub stores these additional analysis tables first:

```text
Donations
Donors
Reviews
```

Public archive excludes:

```text
Email Address
Telegram username
reviewer real names
private notes
```

Public archive includes:

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

Project matching uses:

```text
provisional
confirmed
rejected
new_project
```

First detailed import:

```text
Spark S6
Gitcoin GG23 DeSci Community Round
```

Gitcoin five-round strategy:

```text
Create round metadata first.
Backfill detailed data one round at a time.
```

---

## Main Model

```text
Projects = ecosystem identity
Funding Rounds = funding context
Participations = project-round history
Donations = funding graph
Donors = wallet identity graph
Reviews = evaluation history
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

---

## Gitcoin DeSci Round Metadata

```text
Sep 2022 | GR15 | 567k | 82 projects | 2309 donors
May 2023 | Beta | 75k | 65 projects | 267 donors
Apr 2024 | GG20 | 25k | 29 projects | 292 donors
Aug 2024 | GG21 | 39k | 49 projects | 390 donors
Mar 2025 | GG23 | 5k | 21 projects | 80 donors
```

---

## Phase Gate Rule

Each phase should be reviewed and confirmed before moving to the next phase.

