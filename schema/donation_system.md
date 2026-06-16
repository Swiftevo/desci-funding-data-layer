# Donation System V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

The donation system preserves individual donation or vote events, primarily for Gitcoin quadratic funding rounds.

This table is stored in GitHub first and is not part of the first-phase Notion database setup.

---

## Purpose

The donations table supports:

- donor graph analysis
- repeat donor analysis
- cross-round donor behavior
- donation amount distribution
- grant address linkage
- score threshold analysis
- anti-sybil research
- quadratic funding research

---

## Donation Event Table

One donation or vote event should have one row.

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| donation_id | text | Internal DeSci donation event ID |
| source_donation_id | text | Source event ID from Gitcoin or other platform |
| funding_round_id | text | Links to funding round |
| participation_id | text | Links to participation if matched |
| project_entity_id | text | Links to project if matched |
| source_project_id | text | Source platform project ID |
| source_application_id | text | Source platform application ID |
| round_source_id | text | Source platform round ID |
| token_address | text | Token contract address or native token placeholder |
| donor_wallet | text | Public donor wallet address |
| grant_address | text | Public project grant or payout address |
| amount_raw | text / number | Raw token amount in source units |
| amount_usd | number | USD value if available |
| coefficient | number | Source scoring or QF coefficient if available |
| status | select | Source event status |
| score_type | text | Source scoring check type |
| success | boolean | Whether the source score check succeeded |
| raw_score | number | Source raw score |
| threshold | number | Source threshold |
| last_score_timestamp | datetime | Source score timestamp |
| source_platform | select | Gitcoin, etc. |

---

## Gitcoin Source Field Mapping

Gitcoin donation source fields map as follows:

| Gitcoin Field | V1.5 Field |
| --- | --- |
| id | source_donation_id |
| projectId | source_project_id |
| applicationId | source_application_id |
| roundId | round_source_id |
| token | token_address |
| voter | donor_wallet |
| grantAddress | grant_address |
| amount | amount_raw |
| amountUSD | amount_usd |
| coefficient | coefficient |
| status | status |
| last_score_timestamp | last_score_timestamp |
| type | score_type |
| success | success |
| rawScore | raw_score |
| threshold | threshold |

---

## Donor Table

The donors table aggregates wallet-level donor identity.

One wallet address should have one row.

### Recommended Fields

| Field | Type | Notes |
| --- | --- | --- |
| donor_id | text | Stable internal donor ID, e.g. `DSDN-000001` |
| wallet_address | text | Public wallet address |
| first_seen_funding_round_id | text | First known round in this archive |
| supported_round_count | number | Count of rounds supported |
| supported_project_count | number | Count of unique projects supported |
| total_donation_count | number | Count of donation events |
| total_donated_usd | number | Total donation amount in USD |
| notes | text | Public notes only |

---

## Public Policy

Donor wallet addresses may be included in the public archive because they are necessary for:

- donation graph analysis
- repeat donor analysis
- anti-sybil research
- cross-round ecosystem analysis

No private off-chain donor identity should be inferred or added without explicit source evidence.

