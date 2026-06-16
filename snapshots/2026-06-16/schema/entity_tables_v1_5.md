# Entity Tables V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

This document defines the three main V1.5 entity tables:

```text
projects
funding_rounds
participations
```

These tables map to the first-phase Notion databases.

---

## 1. Projects

Purpose: preserve long-term DeSci project identity.

One real project should have one row.

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| project_entity_id | text | Stable DeSci project ID, e.g. `DSPJ-0001` |
| canonical_project_name | text | Standard project name used by this archive |
| aliases | multi-text / JSON | Other names used across platforms or rounds |
| website | url | Public project website |
| project_twitter | url / text | Project Twitter/X profile |
| project_github | url / text | Project GitHub organization or repository |
| user_github | url / text | Public GitHub profile if relevant |
| payout_addresses | JSON / multi-text | Known public payout or grant addresses |
| project_type | multi-select | Uses V1 category system |
| domain | multi-select | Uses V1 category system |
| function | multi-select | Uses V1 category system |
| region | multi-select | Optional regional classification |
| project_status | select | Active, inactive, unknown, archived |
| classification_status | select | unclassified, provisional, confirmed |
| match_status | select | provisional, confirmed, rejected, new_project |
| confirmed_by | text | Human who confirmed identity or match |
| confirmed_at | date | Date of confirmation |
| notes | text | Public notes only |

### Exclusions

Do not store round-specific information in `projects`, including:

- application text
- donor count
- review score
- single-round funding outcome
- single-round status

---

## 2. Funding Rounds

Purpose: preserve round-level metadata.

One funding round should have one row.

### Initial Round IDs

| funding_round_id | Round |
| --- | --- |
| FR-ART-S6 | Artizen Season 6 — Spark DeSci Round |
| FR-GTC-GG23-DESCI | Gitcoin GG23 DeSci Community Round |
| FR-GTC-GG21-DESCI | Gitcoin GG21 DeSci Community Round |
| FR-GTC-GG20-DESCI | Gitcoin GG20 DeSci Community Round |
| FR-GTC-BETA-DESCI | Gitcoin Beta DeSci Community Round |
| FR-GTC-GR15-DESCI | Gitcoin GR15 DeSci Community Round |

### Gitcoin DeSci Round Summary

| Time | Round | Matching Pool | Number of Projects | Number of Donors |
| --- | --- | ---: | ---: | ---: |
| Sep 2022 | GR15 | 567000 | 82 | 2309 |
| May 2023 | Beta | 75000 | 65 | 267 |
| Apr 2024 | GG20 | 25000 | 29 | 292 |
| Aug 2024 | GG21 | 39000 | 49 | 390 |
| Mar 2025 | GG23 | 5000 | 21 | 80 |

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| funding_round_id | text | Stable round ID |
| platform | select | Gitcoin, Artizen, etc. |
| round_name | text | Human-readable round name |
| round_family | text | e.g. Gitcoin DeSci Community Round, Spark DeSci |
| round_number | text | e.g. GR15, Beta, GG20, GG21, GG23, S6 |
| time_period | text | Human-readable timing |
| start_date | date | Optional |
| end_date | date | Optional |
| round_operator | text | Operator or steward group |
| lead_team | text | Public lead team names or group |
| matching_pool_usd | number | Round-level matching pool |
| project_count | number | Number of projects in the round |
| donor_count | number | Number of donors in the round |
| round_status | select | planned, active, completed, archived |
| result_status | select | pending, partial, final, unknown |
| source_url | url | Public round source |
| schema_version | text | e.g. V1.5 |
| notes | text | Public notes only |

---

## 3. Participations

Purpose: preserve one project participation in one funding round.

One project participating in one round should have one row.

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| participation_id | text | Stable DeSci participation ID, e.g. `DSPT-00001` |
| project_entity_id | text / relation | Links to `projects` |
| funding_round_id | text / relation | Links to `funding_rounds` |
| platform | select | Source platform |
| round_family | text | Round family name |
| source_project_name | text | Project name as shown on source platform |
| source_project_id | text | Source platform project ID |
| source_application_id | text | Source platform application ID |
| source_status | select | Source-native status |
| source_url | url | Source application or project URL |
| application_status | select | approved, rejected, pending, unknown |
| payout_address | text | Public project payout address |
| grant_address | text | Public grant address if available |
| raw_text | text | Source-aware preserved application text |
| application_summary | text | Short human/AI-readable summary |
| requested_amount_usd | number | Requested amount if available |
| raised_amount_usd | number | Direct raised amount |
| matching_amount_usd | number | Matching amount |
| final_amount_usd | number | Total final funding amount |
| donor_count | number | Total donor count |
| unique_donor_count | number | Unique donor count |
| vote_count | number | Vote count if applicable |
| funding_rank | number | Funding rank if available |
| review_status | select | not_reviewed, reviewed, tiebreaker, unknown |
| review_score_avg | number | Summary only |
| review_decision | select | approved, rejected, unknown |
| match_status | select | provisional, confirmed, rejected, new_project |
| matched_project_entity_id | text | Candidate or confirmed project ID |
| confirmed_by | text | Human confirmer |
| confirmed_at | date | Confirmation date |
| source_specific_fields_json | JSON/text | Platform-specific fields that do not belong in the core schema |

---

## Source-Specific Fields

Do not split participations by platform.

Use one unified participation table, and preserve platform-specific fields in:

```text
source_specific_fields_json
```

This keeps project-round history queryable across platforms while preserving source detail.

