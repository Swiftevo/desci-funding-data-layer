# Property Types V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

V1.5 extends V1 property types from a single-table schema into a multi-table schema.

The first-phase Notion databases are:

```text
Projects
Funding Rounds
Participations
```

GitHub analysis tables are:

```text
Donations
Donors
Reviews
```

---

## General Type Rules

Use simple, portable types:

| Type | Use |
| --- | --- |
| text | IDs, names, addresses, status values when portability matters |
| number | scores, counts, USD amounts |
| date | dates without time |
| datetime | event timestamps |
| url | public web links |
| boolean | true/false flags |
| multi-select | controlled category lists in Notion |
| JSON/text | source-specific fields and nested source metadata |

CSV and JSON exports should preserve stable field names using snake_case.

---

## Projects Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| project_entity_id | text | yes |
| canonical_project_name | text / title | yes |
| aliases | JSON/text | yes |
| website | url | yes |
| project_twitter | text / url | yes |
| project_github | text / url | yes |
| user_github | text / url | yes |
| payout_addresses | JSON/text | yes |
| project_type | multi-select | yes |
| domain | multi-select | yes |
| function | multi-select | yes |
| region | multi-select | yes |
| project_status | select/text | yes |
| classification_status | select/text | yes |
| match_status | select/text | yes |
| confirmed_by | text | yes |
| confirmed_at | date | yes |
| notes | text | yes, public notes only |

---

## Funding Rounds Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| funding_round_id | text | yes |
| platform | select/text | yes |
| round_name | text / title | yes |
| round_family | text | yes |
| round_number | text | yes |
| time_period | text | yes |
| start_date | date | yes |
| end_date | date | yes |
| round_operator | text | yes |
| lead_team | text | yes |
| matching_pool_usd | number | yes |
| project_count | number | yes |
| donor_count | number | yes |
| round_status | select/text | yes |
| result_status | select/text | yes |
| source_url | url | yes |
| schema_version | text | yes |
| notes | text | yes, public notes only |

---

## Participations Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| participation_id | text | yes |
| project_entity_id | relation/text | yes |
| funding_round_id | relation/text | yes |
| platform | select/text | yes |
| round_family | text | yes |
| source_project_name | text / title | yes |
| source_project_id | text | yes |
| source_application_id | text | yes |
| source_status | select/text | yes |
| source_url | url | yes |
| application_status | select/text | yes |
| payout_address | text | yes |
| grant_address | text | yes |
| raw_text | text | yes, after private-field removal if needed |
| application_summary | text | yes |
| requested_amount_usd | number | yes |
| raised_amount_usd | number | yes |
| matching_amount_usd | number | yes |
| final_amount_usd | number | yes |
| donor_count | number | yes |
| unique_donor_count | number | yes |
| vote_count | number | yes |
| funding_rank | number | yes |
| review_status | select/text | yes |
| review_score_avg | number | yes |
| review_decision | select/text | yes |
| match_status | select/text | yes |
| matched_project_entity_id | text | yes |
| confirmed_by | text | yes |
| confirmed_at | date | yes |
| source_specific_fields_json | JSON/text | yes, excluding private fields |

---

## Donations Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| donation_id | text | yes |
| source_donation_id | text | yes |
| funding_round_id | text | yes |
| participation_id | text | yes when matched |
| project_entity_id | text | yes when matched |
| source_project_id | text | yes |
| source_application_id | text | yes |
| round_source_id | text | yes |
| token_address | text | yes |
| donor_wallet | text | yes |
| grant_address | text | yes |
| amount_raw | text/number | yes |
| amount_usd | number | yes |
| coefficient | number | yes |
| status | select/text | yes |
| score_type | text | yes |
| success | boolean | yes |
| raw_score | number | yes |
| threshold | number | yes |
| last_score_timestamp | datetime | yes |
| source_platform | select/text | yes |

---

## Donors Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| donor_id | text | yes |
| wallet_address | text | yes |
| first_seen_funding_round_id | text | yes |
| supported_round_count | number | yes |
| supported_project_count | number | yes |
| total_donation_count | number | yes |
| total_donated_usd | number | yes |
| notes | text | yes, public notes only |

---

## Reviews Properties

| Field | Recommended Type | Public |
| --- | --- | --- |
| review_id | text | yes |
| funding_round_id | text | yes |
| participation_id | text | yes |
| project_entity_id | text | yes |
| reviewer_id | text | yes, anonymized |
| reviewer_label | text | yes, anonymized |
| score | number | yes |
| score_scale | text | yes |
| is_tiebreaker | boolean | yes |
| decision | select/text | yes |
| review_status | select/text | yes |

---

## Private Fields

The following fields must not enter public exports:

```text
Email Address
Telegram username
reviewer real names
private notes
private reviewer comments
```

If private fields are needed for temporary work, keep them outside the public canonical archive.

