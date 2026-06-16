# Snapshot — 2026-06-16

This snapshot preserves the first V1.5 checkpoint before project-level data import.

Included:

```text
schema/
rounds/*/round_info.json
data/funding_rounds/funding_rounds_latest.csv
data/funding_rounds/funding_rounds_latest.json
exports/public/funding_rounds_latest.csv
exports/public/funding_rounds_latest.json
```

Not included yet:

```text
projects
participations
donations
donors
reviews
```

Those tables will be generated after Spark S6 split and Gitcoin GG23 import.

