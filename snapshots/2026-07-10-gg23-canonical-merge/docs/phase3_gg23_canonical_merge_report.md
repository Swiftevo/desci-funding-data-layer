# Phase 3 GG23 Canonical Merge Report

Date: 2026-07-10  
Status: Canonical merge completed locally for review

---

## Summary

Gitcoin GG23 draft records have been merged into the V1.5 canonical project and participation tables.

The merge followed:

```text
data/matching/spark_gg23_match_candidates.csv
data/matching/gg23_project_id_allocation_preview.csv
docs/phase3_gg23_canonical_merge_plan.md
```

---

## Project Merge Result

Before merge:

```text
projects_latest: 49
```

After merge:

```text
projects_latest: 61
```

New project IDs assigned:

```text
DSPJ-0050
DSPJ-0051
DSPJ-0052
DSPJ-0053
DSPJ-0054
DSPJ-0055
DSPJ-0056
DSPJ-0057
DSPJ-0058
DSPJ-0059
DSPJ-0060
DSPJ-0061
```

Confirmed Spark matches reused existing `DSPJ` IDs.

---

## Participation Merge Result

Before merge:

```text
participations_latest: 49
```

After merge:

```text
participations_latest: 70
```

Breakdown:

```text
Spark S6 participations: 49
Gitcoin GG23 participations: 21
```

Validation:

```text
unique participation_id: 70
empty project_entity_id: 0
empty raw_text: 0
```

---

## Donation Update Result

GG23 donation draft rows:

```text
274
```

All donation rows now have `project_entity_id` filled from the reviewed allocation preview.

Preserved donation status fields:

```text
status = DONE: 238
status = blank: 36
success = FALSE: 91
```

No donation event was filtered out.

---

## Public Exports Updated

Updated:

```text
exports/public/projects_latest.csv
exports/public/projects_latest.json
exports/public/participations_latest.csv
exports/public/participations_latest.json
```

---

## Notes

LunCo remains a new canonical project:

```text
DSPJ-0050
```

Its relationship to LORS is preserved in matching and allocation notes:

```text
LORS is one of LunCo projects; Spark participation was LORS directly, not LunCo directly.
```

DeSci LATAM remains a new canonical project:

```text
DSPJ-0060
```

because the proposed match to DeSci Mexico was rejected by human review.

