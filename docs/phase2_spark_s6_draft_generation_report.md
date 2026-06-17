# Phase 2 Spark S6 Draft Generation Report

Date: 2026-06-17  
Status: Draft tables generated for review  
Source round: `FR-ART-S6`

---

## Purpose

This report documents the first Spark S6 V1.5 table split.

Generated draft tables:

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

---

## Source

Source CSV:

```text
exports/public/desci_funding_data_layer_latest.csv
```

from the current GitHub V1 archive.

---

## Validation Summary

### Projects

| Check | Result |
| --- | ---: |
| Rows | 49 |
| Unique project_entity_id | 49 |
| Empty canonical_project_name | 0 |
| Non-empty website | 0 |

### Participations

| Check | Result |
| --- | ---: |
| Rows | 49 |
| Unique participation_id | 49 |
| Funding round IDs | FR-ART-S6 |
| Empty raw_text | 0 |
| Empty source_url | 0 |

### JSON

| File | Records |
| --- | ---: |
| projects_latest.json | 49 |
| participations_latest.json | 49 |

---

## Key Design Decision

The V1 `Link` field is an Artizen application/project page, not necessarily the project's independent website.

Therefore:

```text
projects.website = empty
participations.source_url = V1 Link
```

This avoids treating a platform application URL as a long-term project website.

---

## Default Values Applied

### Projects

```text
project_status = unknown
classification_status = provisional
match_status = confirmed
confirmed_by = existing_v1_archive
confirmed_at = 2026-06-16
```

### Participations

```text
platform = Artizen
round_family = Spark DeSci
application_status = unknown
review_status = not_collected
review_decision = unknown
match_status = confirmed
matched_project_entity_id = project_entity_id
confirmed_by = existing_v1_archive
confirmed_at = 2026-06-16
source_specific_fields_json = {}
```

---

## Raw Text Policy

`raw_text` was preserved exactly from the V1 CSV.

No summarization, cleaning, or rewriting was applied.

---

## Review Needed

Please review:

1. Whether `projects.website` should remain empty for Spark S6.
2. Whether `classification_status = provisional` is appropriate for all 49 Spark projects.
3. Whether `match_status = confirmed` is acceptable for existing V1 project IDs.
4. Whether draft tables are ready to become Phase 2 canonical outputs.

