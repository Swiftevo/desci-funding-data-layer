# Phase 3 GG23 Canonical Merge Plan

Date: 2026-06-28  
Status: Allocation preview generated for review

---

## Purpose

Define how reviewed Gitcoin GG23 draft records should be merged into the canonical V1.5 data layer.

This plan does not perform the canonical merge yet.

---

## Inputs

Reviewed match file:

```text
data/matching/spark_gg23_match_candidates.csv
data/matching/spark_gg23_match_candidates.json
```

GG23 draft files:

```text
data/participations/gitcoin_gg23_participations_draft.csv
data/donations/gitcoin_gg23_donations_draft.csv
data/donors/gitcoin_gg23_donors_draft.csv
```

Current canonical files:

```text
data/projects/projects_latest.csv
data/participations/participations_latest.csv
```

---

## Allocation Preview Outputs

Generated preview:

```text
data/matching/gg23_project_id_allocation_preview.csv
data/matching/gg23_project_id_allocation_preview.json
```

---

## Reviewed Match Summary

| Status | Count |
| --- | ---: |
| confirmed | 9 |
| new_project | 11 |
| rejected | 1 |
| total | 21 |

Interpretation:

```text
9 GG23 records reuse existing Spark project_entity_id values.
12 GG23 records require new DSPJ project_entity_id values.
```

The rejected match is:

```text
DeSci LATAM -/-> DeSci Mexico
```

Because DeSci LATAM remains an approved GG23 project, it should become a new canonical project.

---

## Project ID Allocation Rule

Draft imports do not reserve permanent project IDs.

Project IDs are assigned only after matching review.

Rules:

```text
confirmed -> reuse Spark project_entity_id
new_project -> assign next available DSPJ ID
rejected -> do not merge with rejected candidate; assign new DSPJ ID if the GG23 project is otherwise valid
provisional -> hold for review
```

Current Spark project IDs end at:

```text
DSPJ-0049
```

Therefore new GG23 project IDs are allocated as:

```text
DSPJ-0050 through DSPJ-0061
```

---

## Allocation Summary

### Reused Existing Spark Project IDs

```text
DeSci Asia -> DSPJ-0029
FunDeSci -> DSPJ-0049
MesoReefDAO -> DSPJ-0043
AsteriskDAO -> DSPJ-0045
The DeSci Journals v4 (Celo) -> DSPJ-0040
HyperDeSci Ops | Summoning $MEGAPI -> DSPJ-0021
Hyvmind -> DSPJ-0005
overlake bio -> DSPJ-0030
DeSci Round working group -> DSPJ-0027
```

### New Project IDs

```text
LunCo: Metaverse for Space Engineers -> DSPJ-0050
DeSci Youths -> DSPJ-0051
Astral -> DSPJ-0052
OpenLitterMap: Real-Time In-World Open Source Gamification System -> DSPJ-0053
?RTH - Planetary AI -> DSPJ-0054
Ideosphere -> DSPJ-0055
EcoSynthesisX -> DSPJ-0056
NetX State -> DSPJ-0057
Register deSci MAXi -> DSPJ-0058
Maxi DeSci Metaverse -> DSPJ-0059
DeSci LATAM -> DSPJ-0060
Dash Mon[k]ey -> DSPJ-0061
```

---

## Canonical Merge Actions

After preview confirmation, update:

```text
data/projects/projects_latest.csv
data/projects/projects_latest.json
data/participations/participations_latest.csv
data/participations/participations_latest.json
exports/public/projects_latest.csv
exports/public/projects_latest.json
exports/public/participations_latest.csv
exports/public/participations_latest.json
```

### Projects

For confirmed matches:

```text
Do not create duplicate project rows.
Optionally enrich existing project rows later after field-level review.
```

For new projects:

```text
Add new project rows using allocated DSPJ IDs.
Use GG23 source fields as project identity candidates.
Set classification_status = unclassified or provisional.
Set project_status = unknown.
Set match_status = confirmed.
Set confirmed_by / confirmed_at from match review.
```

### Participations

For all GG23 draft participations:

```text
Set project_entity_id = final_project_entity_id from allocation preview.
Set identity_status = confirmed.
Set cross_round_match_status = match_status from reviewed matching file.
Set matched_project_entity_id = final_project_entity_id.
```

Append the 21 GG23 participation rows to canonical participations.

Expected result:

```text
canonical projects: 49 + 12 = 61
canonical participations: 49 + 21 = 70
```

### Donations

Update GG23 draft donations:

```text
Set project_entity_id using allocation preview by source_application_id.
Keep participation_id as already assigned.
Preserve all donation event statuses and success values.
```

Donation rows remain:

```text
274
```

### Donors

GG23 donor draft remains:

```text
80 unique wallet rows
```

No cross-round donor merge is needed yet because GG23 is the first donor table.

---

## Expected Post-Merge Counts

```text
projects_latest: 61 rows
participations_latest: 70 rows
gitcoin_gg23_donations_draft: 274 rows with project_entity_id filled
gitcoin_gg23_donors_draft: 80 rows
```

---

## Review Required Before Merge

Confirm:

```text
1. Allocation preview is correct.
2. DSPJ-0050 through DSPJ-0061 assignment order is acceptable.
3. Rejected DeSci LATAM candidate should receive new ID DSPJ-0060.
4. Confirmed matches should reuse the listed Spark IDs.
```

After confirmation, perform canonical merge.

