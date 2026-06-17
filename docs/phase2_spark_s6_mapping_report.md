# Phase 2 Spark S6 Mapping Report

Date: 2026-06-16  
Status: Draft for review  
Source round: `FR-ART-S6`

---

## Purpose

This report analyzes the existing Spark S6 V1 CSV before splitting it into the V1.5 tables:

```text
projects
funding_rounds
participations
```

No project-level V1.5 tables have been generated yet.

---

## Source Files Reviewed

The current GitHub V1 source files are:

```text
exports/public/desci_funding_data_layer_latest.csv
data/csv/DeSci_PreNotion_Production_V1.csv
```

Both files expose the same V1 column structure for Spark S6.

---

## Integrity Summary

| Check | Result |
| --- | ---: |
| Rows | 49 |
| Columns | 40 |
| Unique project_entity_id | 49 |
| Unique participation_id | 49 |
| Funding round IDs | FR-ART-S6 |
| Empty project names | 0 |
| Empty raw_text fields | 0 |

Conclusion:

```text
The Spark S6 V1 CSV is suitable for V1.5 splitting.
```

---

## V1 Column Inventory

```text
project_entity_id
funding_round_id
participation_id
Project name
Link
Round
Season
Status
Region
Project type
Domain
Function
Category
Problem type
Solution type
Target user
Tags
What are you making
Impact
Progress
Why you
raw_text
Summary (AI)
DeSci alignment
Evidence level
Narrative clarity
Risk flag
Fundability score
Impact score
Execution score
raised_amount_usd
requested_amount_usd
matching_amount_usd
donor_count
vote_count
funding_rank
GitHub path
Obsidian path
Created
Last edited
```

---

## Empty Field Summary

Fields fully populated:

```text
project_entity_id
funding_round_id
participation_id
Project name
Link
Round
Season
What are you making
Impact
Progress
Why you
raw_text
Created
Last edited
```

Mostly populated:

```text
Project type: 46 / 49
Domain: 46 / 49
Function: 46 / 49
```

Currently empty:

```text
Status
Region
Category
Problem type
Solution type
Target user
Tags
Summary (AI)
DeSci alignment
Evidence level
Narrative clarity
Risk flag
Fundability score
Impact score
Execution score
raised_amount_usd
requested_amount_usd
matching_amount_usd
donor_count
vote_count
funding_rank
GitHub path
Obsidian path
```

Interpretation:

```text
The V1 CSV already contains complete identity and application preservation fields.
Funding, review, AI summary, and advanced classification fields are placeholders.
```

---

## Proposed V1 to V1.5 Mapping

### Projects Table

These fields should move into `data/projects/projects_latest.csv` and `.json`:

| V1 Field | V1.5 Field |
| --- | --- |
| project_entity_id | project_entity_id |
| Project name | canonical_project_name |
| Link | website / source_url candidate |
| Project type | project_type |
| Domain | domain |
| Function | function |
| Region | region |
| Created | created_at_source |
| Last edited | last_edited_source |

Recommended default fields:

```text
aliases = empty
project_status = unknown
classification_status = provisional
match_status = confirmed
confirmed_by = existing_v1_archive
confirmed_at = 2026-06-16
notes = Imported from Spark S6 V1 archive.
```

Rationale:

```text
Spark V1 already assigned stable project_entity_id values.
For the initial split, these can be treated as confirmed project records within the existing V1 archive.
```

---

### Funding Rounds Table

Spark S6 is already represented in:

```text
data/funding_rounds/funding_rounds_latest.csv
data/funding_rounds/funding_rounds_latest.json
```

No new funding round row is needed.

---

### Participations Table

These fields should move into `data/participations/participations_latest.csv` and `.json`:

| V1 Field | V1.5 Field |
| --- | --- |
| participation_id | participation_id |
| project_entity_id | project_entity_id |
| funding_round_id | funding_round_id |
| Round | round_family / source_round_name |
| Season | round_number / source_season |
| Project name | source_project_name |
| Link | source_url |
| Status | source_status / application_status |
| What are you making | what_are_you_making |
| Impact | impact |
| Progress | progress |
| Why you | why_you |
| raw_text | raw_text |
| Summary (AI) | application_summary |
| raised_amount_usd | raised_amount_usd |
| requested_amount_usd | requested_amount_usd |
| matching_amount_usd | matching_amount_usd |
| donor_count | donor_count |
| vote_count | vote_count |
| funding_rank | funding_rank |
| GitHub path | github_path |
| Obsidian path | obsidian_path |
| Created | created_at_source |
| Last edited | last_edited_source |

Recommended default fields:

```text
platform = Artizen
round_family = Spark DeSci
application_status = unknown
review_status = not_collected
review_decision = unknown
match_status = confirmed
source_specific_fields_json = preserve empty or source-only fields
```

---

## Classification Notes

Current populated classification fields:

```text
Project type
Domain
Function
```

All populated `Project type` and `Domain` values fit the existing V1 category system.

The `Function` field contains several round-specific extensions not currently listed in `schema/category_system.md`:

```text
Data Processing
Data Storage
Infrastructure
Matching
Onboarding
Restoration
```

Recommendation:

```text
Preserve these source values during the split.
Set classification_status = provisional.
Do not change the canonical category system yet.
```

Future review can decide whether to:

```text
map them to existing canonical values
keep them as source-specific functions
promote some of them into canonical V1.5 category extensions
```

---

## Raw Text Preservation

`raw_text` is fully populated for all 49 records.

Spark / Artizen raw text uses this structure:

```text
[WHAT]
[IMPACT]
[PROGRESS]
[WHY]
```

Recommendation:

```text
Preserve raw_text exactly in participations.
Do not summarize, clean, or rewrite it during the split.
```

---

## Phase 2 Next Step

If this mapping report is confirmed, the next step is:

```text
Generate draft Spark S6 V1.5 projects and participations tables.
```

Expected outputs:

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

These should be generated as draft outputs first, then reviewed before committing.

