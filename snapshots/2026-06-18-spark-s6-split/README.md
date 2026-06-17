# Snapshot — 2026-06-18 Spark S6 Split

This snapshot preserves the first Spark S6 V1.5 split into:

```text
projects
participations
funding_rounds
```

Included:

```text
data/projects/projects_latest.csv
data/projects/projects_latest.json
data/participations/participations_latest.csv
data/participations/participations_latest.json
data/funding_rounds/funding_rounds_latest.csv
data/funding_rounds/funding_rounds_latest.json
exports/public/*.csv
exports/public/*.json
docs/phase2_spark_s6_mapping_report.md
docs/phase2_spark_s6_draft_generation_report.md
docs/TODO.md
```

Not included yet:

```text
Gitcoin GG23 data
donations
donors
reviews
classification_review_queue.csv
```

Classification review is intentionally deferred until after Spark + GG23 import and matching.

