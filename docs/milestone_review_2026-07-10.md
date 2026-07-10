# Milestone Review - 2026-07-10

## Current Milestones

### Milestone 1 - V1.5 Foundation

Status:

```text
completed and merged
```

Delivered:

```text
schema_v1_5
entity table docs
donation/review/public-private policies
repo folder structure
round metadata for Spark S6 and five Gitcoin DeSci rounds
funding_rounds_latest
initial V1.5 snapshot
```

### Milestone 2 - Spark S6 Split

Status:

```text
completed and merged
```

Delivered:

```text
49 Spark projects
49 Spark participations
projects_latest
participations_latest
public exports
Spark split snapshot
```

### Milestone 3 - GG23 Source Inspection and Mapping Plan

Status:

```text
completed and merged
```

Delivered:

```text
GG23 source inspection report
GG23 mapping plan
project diary
```

Key decision:

```text
Preserve all GG23 donation rows, including blank status and success = FALSE rows.
```

### Milestone 4 - GG23 Draft Import

Status:

```text
completed locally
```

Delivered:

```text
21 GG23 draft participations
274 GG23 donation events
80 GG23 donor wallet rows
```

### Milestone 5 - Spark/GG23 Matching and Canonical Merge

Status:

```text
completed locally, PR #4 created
```

Delivered:

```text
match candidates
ID allocation preview
canonical merge plan
canonical merge report
2026-07-10 GG23 merge snapshot
```

Merge result:

```text
projects_latest: 61
participations_latest: 70
```

## Current Data Shape

```text
Projects: 61
Participations: 70
Funding rounds: 6
Spark S6 participations: 49
Gitcoin GG23 participations: 21
GG23 donation events: 274
GG23 donor wallets: 80
```

## Important Compression of Decisions

The important decisions are now:

```text
Project identity is canonical at the DSPJ layer.
Participation records represent project-round history.
GG23 did not reserve DSPJ IDs until matching was reviewed.
Confirmed GG23/Spark matches reuse Spark DSPJ IDs.
New GG23 projects received DSPJ-0050 through DSPJ-0061.
LunCo is a new project but related to LORS.
DeSci LATAM is independent from DeSci Mexico.
GG23 donation status and success fields are preserved.
```

Older implementation teaching details are less important than these operating rules.

## Next Recommended Milestone

After PR #4 is merged:

```text
Generate classification_review_queue.csv
```

Then decide:

```text
whether to backfill GG21 next
whether to add project_relationships
whether to promote GG23 donors into donors_latest now or wait for multi-round donor data
```

