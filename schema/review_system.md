# Review System V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

The review system preserves reviewer scores for funding round applications without exposing reviewer real names in public exports.

Review records are stored in GitHub first and are not part of the first-phase Notion database setup.

---

## Purpose

The reviews table supports:

- review score comparison
- reviewer disagreement analysis
- tiebreaker analysis
- funding outcome versus review score analysis
- cross-round evaluation history

---

## Review Table

One reviewer score for one participation should have one row.

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| review_id | text | Stable review record ID |
| funding_round_id | text | Links to funding round |
| participation_id | text | Links to participation |
| project_entity_id | text | Links to project |
| reviewer_id | text | Anonymized reviewer ID |
| reviewer_label | text | Public label, e.g. Reviewer 1 |
| score | number | Reviewer score |
| score_scale | text | e.g. 0-1 |
| is_tiebreaker | boolean | True if this review was a tiebreaker |
| decision | select | approved, rejected, unknown |
| review_status | select | submitted, missing, excluded, unknown |

---

## Reviewer Anonymization

Reviewer real names are not included in public exports.

Use anonymized reviewer IDs:

```text
GTC-GG23-RV01
GTC-GG23-RV02
GTC-GG23-RV03
GTC-GG23-RV04
```

Reviewer labels may be used for readability:

```text
Reviewer 1
Reviewer 2
Reviewer 3
Tiebreaker Reviewer
```

---

## Participation Summary Fields

The participation table may store review summary fields:

```text
review_status
review_score_avg
review_score_min
review_score_max
review_score_disagreement
tiebreaker_used
review_decision
```

Detailed reviewer-level scores remain in `reviews`.

---

## Public Policy

Public archive includes:

- anonymized reviewer IDs
- anonymized reviewer labels
- scores
- score scale
- tiebreaker flag
- decision

Public archive excludes:

- reviewer real names
- private reviewer notes
- internal conflict discussions

