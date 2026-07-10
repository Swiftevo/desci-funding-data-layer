# Phase 3 Gitcoin GG23 Mapping Plan

Date: 2026-06-18  
Status: Draft plan for confirmation  
Round: `FR-GTC-GG23-DESCI`

---

## Purpose

Define the import and matching workflow for Gitcoin GG23 DeSci Community Round before generating formal V1.5 tables.

This plan follows the phase-gate rule:

```text
inspect source
confirm mapping
generate draft tables
review draft tables
merge into canonical outputs
```

---

## Confirmed Source Files

Local source files:

```text
C:\Users\User\Desktop\gitcoin grant 23 desci community round project information.txt
C:\Users\User\Desktop\gitcoin grant 23 desci community round small donation.txt
```

Confirmed source interpretation:

```text
project information file = complete approved project/application source for GG23
small donation file = complete GG23 donation source
```

---

## Confirmed Preservation Decisions

### Donation Rows

All donation rows should be preserved.

This includes:

```text
status = DONE
status = blank
success = TRUE
success = FALSE
success = blank
```

Reason:

```text
Future AI agents and analysts must be able to distinguish successful, failed, blank-status, and threshold-related donation events.
If status and success are collapsed or filtered out, future analysis may incorrectly treat all donation events as successful.
```

The following fields must be preserved:

```text
status
success
type
rawScore
threshold
coefficient
last_score_timestamp
```

---

## Shared Payout Address Decision

GG23 contains:

```text
21 approved projects
19 unique payout/grant addresses
```

One payout address appears across three projects:

```text
0x9b9dbC177fbE6A32bBc92A44B04B5d6711e151de
```

Associated projects:

```text
The DeSci Journals v4 (Celo)
Register deSci MAXi
Maxi DeSci Metaverse
```

Decision:

```text
Preserve this exactly.
Do not deduplicate by payout address.
Do not treat shared payout address as an error.
```

Reason:

```text
These projects share the same founder.
The shared payout address is useful for project identity graph, founder-linked analysis, payout graph, and future anti-sybil research.
```

---

## Cross-Round Project Identity Issue

Some GG23 projects may also appear in Spark S6.

Therefore, the same real project may currently have:

```text
one Spark project_entity_id
one GG23 source project/application identity
```

This must be handled carefully to avoid creating duplicate permanent DeSci project IDs.

---

## Import Strategy

GG23 should not be merged directly into canonical `projects_latest` and `participations_latest` before matching.

Use a staged import:

```text
Step A: normalized draft import
Step B: Spark/GG23 match candidate generation
Step C: human confirmation
Step D: canonical merge
```

---

## Step A — Normalized Draft Import

Generate draft source-normalized tables:

```text
data/participations/gitcoin_gg23_participations_draft.csv
data/participations/gitcoin_gg23_participations_draft.json
data/donations/gitcoin_gg23_donations_draft.csv
data/donations/gitcoin_gg23_donations_draft.json
data/donors/gitcoin_gg23_donors_draft.csv
data/donors/gitcoin_gg23_donors_draft.json
```

The GG23 participation draft should include source identity fields, but should not immediately assign permanent new `DSPJ` IDs.

Recommended fields:

```text
participation_id
project_entity_id
funding_round_id
platform
round_family
source_project_name
source_project_id
source_application_id
source_status
source_url
application_status
payout_address
grant_address
raw_text
application_summary
requested_amount_usd
raised_amount_usd
matching_amount_usd
final_amount_usd
donor_count
unique_donor_count
vote_count
funding_rank
review_status
review_score_avg
review_decision
identity_status
cross_round_match_status
matched_project_entity_id
confirmed_by
confirmed_at
source_specific_fields_json
```

For GG23 draft import:

```text
project_entity_id = empty
identity_status = pending_match
cross_round_match_status = pending_match
matched_project_entity_id = empty
```

Reason:

```text
Permanent project_entity_id should be assigned or reused only after Spark/GG23 matching is reviewed.
```

---

## Step B — Match Candidate Generation

Generate:

```text
data/matching/spark_gg23_match_candidates.csv
data/matching/spark_gg23_match_candidates.json
```

Candidate matching should compare GG23 against existing Spark S6 projects using:

```text
project name
website
project_twitter
project_github
user_github
payout_address
past payout wallet text
raw_text similarity
manual knowledge
```

Recommended fields:

```text
match_candidate_id
gg23_source_application_id
gg23_source_project_id
gg23_project_name
gg23_payout_address
spark_candidate_project_entity_id
spark_candidate_project_name
spark_participation_id
match_basis
match_confidence
match_status
confirmed_by
confirmed_at
match_notes
```

Allowed match statuses:

```text
provisional
confirmed
rejected
new_project
```

Rule:

```text
AI or scripts may suggest provisional matches.
Human confirmation is required before a match becomes confirmed.
```

---

## Step C — Human Confirmation

The project curator confirms match candidates.

Confirmed matches should include:

```text
confirmed_by
confirmed_at
match_notes
```

If a GG23 project does not match any Spark S6 project:

```text
match_status = new_project
```

Only after this step should new permanent `DSPJ` IDs be assigned.

---

## Step D — Canonical Merge

After matching confirmation:

Update canonical:

```text
data/projects/projects_latest.csv
data/projects/projects_latest.json
data/participations/participations_latest.csv
data/participations/participations_latest.json
```

Rules:

```text
confirmed match -> reuse existing Spark project_entity_id
new_project -> assign next available DSPJ ID
rejected match -> do not merge with candidate Spark project
provisional -> do not finalize as canonical confirmed identity
```

---

## Draft Donation Mapping

Source file:

```text
gitcoin grant 23 desci community round small donation.txt
```

Map to:

```text
data/donations/gitcoin_gg23_donations_draft.csv
```

Mapping:

| Source Field | Target Field |
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

Additional fields:

```text
funding_round_id = FR-GTC-GG23-DESCI
source_platform = Gitcoin
participation_id = empty until draft participation IDs are assigned
project_entity_id = empty until matching confirmation
```

---

## Draft Donor Mapping

Generate one donor row per unique `voter` wallet:

```text
data/donors/gitcoin_gg23_donors_draft.csv
```

Recommended fields:

```text
donor_id
wallet_address
first_seen_funding_round_id
supported_round_count
supported_project_count
total_donation_count
total_donated_usd
notes
```

For GG23 draft:

```text
first_seen_funding_round_id = FR-GTC-GG23-DESCI
supported_round_count = 1
```

Donor IDs may be assigned as:

```text
DSDN-000001
DSDN-000002
...
```

---

## Draft Raw Text Format

GG23 application raw text should be source-aware.

Recommended format:

```text
[PROJECT DESCRIPTION]
...

[DESCI MISSION ALIGNMENT]
...

[USE OF FUNDS]
...

[PAST ROUND WALLET]
...

[NEW UPDATES]
...

[OTHER INFORMATION]
...
```

Do not summarize, rewrite, or clean source application text during raw text generation.

---

## Public Archive Rules

Public GG23 draft archive may include:

```text
project name
website
projectTwitter
projectGithub
userGithub
payoutAddress
donor wallet
grantAddress
application raw text
donation amount
status
success
rawScore
threshold
```

Public archive must exclude:

```text
Email Address
Telegram username
reviewer real names
private reviewer notes
private internal notes
```

The current inspected GG23 project source file does not include email, Telegram username, or reviewer real names.

---

## Phase 3 Next Action

After this plan is confirmed:

```text
Generate GG23 draft participations, donations, and donors tables.
```

Do not update canonical `projects_latest` or `participations_latest` yet.

Canonical merge happens only after match candidate review.

