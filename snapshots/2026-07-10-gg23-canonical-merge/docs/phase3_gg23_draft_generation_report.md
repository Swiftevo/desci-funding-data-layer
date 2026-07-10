# Phase 3 Gitcoin GG23 Draft Generation Report

Date: 2026-06-24  
Status: Draft tables generated for review  
Round: `FR-GTC-GG23-DESCI`

---

## Purpose

Generate normalized draft tables for Gitcoin GG23 without merging them into canonical project identity tables.

This step follows:

```text
docs/phase3_gg23_source_inspection_report.md
docs/phase3_gg23_mapping_plan.md
```

---

## Generated Draft Files

```text
data/participations/gitcoin_gg23_participations_draft.csv
data/participations/gitcoin_gg23_participations_draft.json
data/donations/gitcoin_gg23_donations_draft.csv
data/donations/gitcoin_gg23_donations_draft.json
data/donors/gitcoin_gg23_donors_draft.csv
data/donors/gitcoin_gg23_donors_draft.json
```

These are draft files.

They do not update:

```text
data/projects/projects_latest.csv
data/projects/projects_latest.json
data/participations/participations_latest.csv
data/participations/participations_latest.json
```

---

## Participation ID Strategy

Spark S6 already uses:

```text
DSPT-00001 through DSPT-00049
```

GG23 draft participations use:

```text
DSPT-00050 through DSPT-00070
```

These are participation IDs, not project IDs.

`project_entity_id` is intentionally empty for all GG23 draft participations until Spark/GG23 matching is reviewed.

---

## Project Identity Strategy

All GG23 draft participation records use:

```text
project_entity_id = empty
identity_status = pending_match
cross_round_match_status = pending_match
matched_project_entity_id = empty
```

Reason:

```text
Some GG23 projects may already exist in Spark S6.
Permanent DSPJ IDs should only be reused or newly assigned after match candidate review.
```

---

## Raw Text Strategy

GG23 application raw text is source-aware and uses:

```text
[PROJECT DESCRIPTION]
[DESCI MISSION ALIGNMENT]
[USE OF FUNDS]
[PAST ROUND WALLET]
[NEW UPDATES]
[OTHER INFORMATION]
```

No summarization, rewriting, or cleaning was applied.

---

## Donation Preservation Strategy

All donation events are preserved.

This includes:

```text
status = DONE
status = blank
success = TRUE
success = FALSE
success = blank
```

The following fields are preserved in every donation event where present:

```text
status
success
score_type
raw_score
threshold
coefficient
last_score_timestamp
```

Reason:

```text
Future analysis must distinguish successful, failed, blank-status, and threshold-related donation events.
```

---

## Validation Summary

### Participations

| Check | Result |
| --- | ---: |
| Rows | 21 |
| Unique participation_id | 21 |
| Empty project_entity_id | 21 |
| identity_status = pending_match | 21 |
| Empty raw_text | 0 |

### Donations

| Check | Result |
| --- | ---: |
| Rows | 274 |
| Unique donation_id | 274 |
| Unique source_donation_id | 274 |
| Unique voters | 80 |
| Empty participation_id | 0 |
| status = DONE | 238 |
| status = blank | 36 |
| success = TRUE | 147 |
| success = FALSE | 91 |
| success = blank | 36 |

### Donors

| Check | Result |
| --- | ---: |
| Rows | 80 |
| Unique donor_id | 80 |
| Unique wallet_address | 80 |
| Sum donation events | 274 |

---

## Funding Amount Semantics

Participation draft records include donation summary fields:

```text
total_donation_event_count
done_event_count
blank_status_event_count
success_true_event_count
success_false_event_count
total_amount_usd_all_events
done_amount_usd
blank_status_amount_usd
success_true_amount_usd
success_false_amount_usd
```

Canonical funding fields such as:

```text
raised_amount_usd
matching_amount_usd
final_amount_usd
```

remain empty at this stage.

Reason:

```text
The draft import preserves event-level data first.
Final funding semantics should be decided after matching and result review.
```

---

## Donor ID Strategy

One donor row is generated per unique `voter` wallet.

Draft donor IDs use:

```text
DSDN-000001 through DSDN-000080
```

The donor draft includes all event types and does not filter failed or blank-status events.

---

## Next Step

After this draft is reviewed, generate:

```text
data/matching/spark_gg23_match_candidates.csv
data/matching/spark_gg23_match_candidates.json
```

Do not canonical-merge GG23 into `projects_latest` or `participations_latest` until matching is reviewed.

