# DeSci Funding Data Layer

Open data infrastructure for decentralized science funding rounds, projects, participations, donations, donors, reviews, and ecosystem research.

## Current Status

V1.5 project-centric model is active.

Current canonical coverage:

```text
Projects: 61
Participations: 70
Funding rounds: 6
```

Current detailed participation coverage:

```text
Spark S6 participations: 49
Gitcoin GG23 participations: 21
```

Gitcoin GG23 analysis tables:

```text
Donation events: 274
Donor wallets: 80
```

## Architecture

The V1.5 data layer uses:

```text
Projects = ecosystem identity
Funding Rounds = funding context
Participations = project-round history
Donations = funding event graph
Donors = wallet identity graph
Reviews = evaluation history
```

The first three tables form the primary project-centric archive:

```text
data/projects/
data/funding_rounds/
data/participations/
```

Analysis tables currently include:

```text
data/donations/
data/donors/
data/matching/
```

## Current Round Coverage

Round metadata exists for:

```text
FR-ART-S6
FR-GTC-GR15-DESCI
FR-GTC-BETA-DESCI
FR-GTC-GG20-DESCI
FR-GTC-GG21-DESCI
FR-GTC-GG23-DESCI
```

Detailed canonical project/participation data currently includes:

```text
FR-ART-S6
FR-GTC-GG23-DESCI
```

Historical Gitcoin rounds are metadata-only until future backfill:

```text
FR-GTC-GR15-DESCI
FR-GTC-BETA-DESCI
FR-GTC-GG20-DESCI
FR-GTC-GG21-DESCI
```

## Canonical Data

Canonical latest tables:

```text
data/projects/projects_latest.csv
data/projects/projects_latest.json
data/funding_rounds/funding_rounds_latest.csv
data/funding_rounds/funding_rounds_latest.json
data/participations/participations_latest.csv
data/participations/participations_latest.json
```

Public exports:

```text
exports/public/projects_latest.csv
exports/public/projects_latest.json
exports/public/funding_rounds_latest.csv
exports/public/funding_rounds_latest.json
exports/public/participations_latest.csv
exports/public/participations_latest.json
```

GG23 draft / analysis tables:

```text
data/participations/gitcoin_gg23_participations_draft.csv
data/donations/gitcoin_gg23_donations_draft.csv
data/donors/gitcoin_gg23_donors_draft.csv
data/matching/spark_gg23_match_candidates.csv
data/matching/gg23_project_id_allocation_preview.csv
```

## Donor Data

GG23 donor data exists as a draft analysis table:

```text
data/donors/gitcoin_gg23_donors_draft.csv
data/donors/gitcoin_gg23_donors_draft.json
```

This is not yet a cross-round canonical `donors_latest` table.

Current donor scope:

```text
Gitcoin GG23 only
80 unique wallet addresses
274 donation events summarized across donor rows
```

Future work should decide when to promote donor data into:

```text
data/donors/donors_latest.csv
data/donors/donors_latest.json
```

after additional Gitcoin rounds are backfilled.

## Preservation Rules

Raw application text is preserved.

Donation event status is preserved, including:

```text
status = blank
success = FALSE
rawScore
threshold
coefficient
score_type
last_score_timestamp
```

This prevents future analysis from treating all donation events as successful.

Public archive excludes:

```text
Email Address
Telegram username
reviewer real names
private notes
```

## Latest Snapshot

Latest local checkpoint:

```text
snapshots/2026-07-10-gg23-canonical-merge/
```

