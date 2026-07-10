# Project Alignment - 2026-07-10

## Purpose

This note aligns three layers of the DeSci Funding Data Layer work:

```text
conversation memory
repository files
current data state
```

It is intended as a compact handoff document for continuing the GG23 import and the next historical Gitcoin backfill without reopening every previous discussion.

## Current Operating Model

The project uses the V1.5 project-centric model:

```text
Projects = ecosystem identity
Funding Rounds = funding context
Participations = project-round history
Donations = funding event graph
Donors = wallet identity graph
Reviews = evaluation history
```

The first three tables are the canonical core:

```text
data/projects/
data/funding_rounds/
data/participations/
```

Donations, donors, reviews, matching outputs, and snapshots support analysis and auditability.

## Confirmed Data State

As of this checkpoint:

```text
projects_latest: 61
participations_latest: 70
funding_rounds_latest: 6
GG23 donation events: 274
GG23 donor wallets: 80
```

Detailed participation coverage:

```text
Spark S6: 49 participations
Gitcoin GG23: 21 participations
```

Round metadata exists for:

```text
FR-ART-S6
FR-GTC-GR15-DESCI
FR-GTC-BETA-DESCI
FR-GTC-GG20-DESCI
FR-GTC-GG21-DESCI
FR-GTC-GG23-DESCI
```

Detailed imported rounds:

```text
FR-ART-S6
FR-GTC-GG23-DESCI
```

Historical Gitcoin rounds still need detailed backfill:

```text
GG21
GG20
Beta
GR15
```

## Conversation Decisions To Preserve

Public archive excludes:

```text
email
telegram username
reviewer real names
private notes
```

Public archive includes:

```text
payout address
grant address
donor wallet
donation event status
anonymized reviewer scores
raw public application text
```

Draft imports must not reserve permanent `DSPJ` project IDs.

Permanent `project_entity_id` values are assigned only after matching review:

```text
confirmed match -> reuse existing DSPJ ID
new project -> assign next available DSPJ ID
rejected candidate -> do not merge with rejected candidate
provisional -> hold for human review
```

For GG23, the reviewed result was:

```text
9 confirmed Spark/GG23 matches
12 new canonical projects
new IDs DSPJ-0050 through DSPJ-0061
```

Special relationship:

```text
LunCo is a new canonical project.
LORS is one of LunCo's projects.
Spark S6 participation was LORS directly, not LunCo directly.
Do not merge LunCo and LORS into one DSPJ ID.
Preserve the relationship in notes or a future project_relationships table.
```

Rejected match:

```text
DeSci LATAM is independent from DeSci Mexico.
DeSci LATAM receives its own canonical ID.
```

Donation preservation rule:

```text
Do not filter failed, blank-status, or low-score donation events.
Preserve status, success, rawScore, threshold, coefficient, score type, and timestamp.
```

This prevents future analysis from treating every donation row as successful.

## File Map

Canonical current tables:

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

GG23 supporting tables:

```text
data/participations/gitcoin_gg23_participations_draft.csv
data/donations/gitcoin_gg23_donations_draft.csv
data/donors/gitcoin_gg23_donors_draft.csv
data/matching/spark_gg23_match_candidates.csv
data/matching/gg23_project_id_allocation_preview.csv
```

Current key docs:

```text
README.md
docs/TODO.md
docs/milestone_review_2026-07-10.md
docs/diary_2026-07-10.md
docs/phase3_gg23_canonical_merge_report.md
docs/phase3_gg23_canonical_merge_plan.md
```

Latest snapshot:

```text
snapshots/2026-07-10-gg23-canonical-merge/
```

## Donor Layer Alignment

Current donor status:

```text
data/donors/gitcoin_gg23_donors_draft.csv exists.
data/donors/gitcoin_gg23_donors_draft.json exists.
data/donors/donors_latest.csv does not exist yet.
data/donors/donors_latest.json does not exist yet.
```

Interpretation:

```text
The project has a GG23 round-specific donor table.
The project does not yet have a cross-round canonical donor identity table.
```

Recommended stance:

```text
Keep GG23 donor data round-specific for now.
Promote to donors_latest after at least one additional Gitcoin round is backfilled,
unless donor analysis becomes the immediate priority.
```

## Review And Worktree Alignment

Important local workflow note:

```text
C:\Users\User\Documents\DeSci Database
```

is currently a data working folder with an unusual local git state. It shows many files as untracked and no local commits on `master`.

The clean PR worktree for PR #5 is:

```text
C:\Users\User\Documents\DeSci Database\.codex-worktrees\docs-progress-review
```

PR #5:

```text
https://github.com/Swiftevo/desci-funding-data-layer/pull/5
status: open draft
branch: docs-progress-review
purpose: documentation and alignment update after GG23 merge
```

Future PR work should use a clean worktree or clean clone based on `origin/main`, not the untracked root workspace directly.

## Current Milestones

Completed and merged:

```text
V1.5 foundation
Spark S6 split
GG23 source inspection and mapping docs
GG23 canonical merge
```

Completed locally / in PR:

```text
README current-state refresh
TODO refresh
2026-07-10 diary
2026-07-10 milestone review
this alignment note
```

## Next Decision Points

Recommended next sequence:

```text
1. Merge PR #5 after review.
2. Generate classification_review_queue.csv.
3. Human-review provisional / unclassified project classifications.
4. Decide whether to add project_relationships for LunCo -> LORS and future parent-child/project-family cases.
5. Choose next Gitcoin historical backfill round, likely GG21.
6. Revisit donors_latest after another Gitcoin round creates real cross-round donor identity value.
```

## Compact Memory For Future Agents

If another agent continues this work, start from these assumptions:

```text
GitHub is the canonical public archive.
Notion is the human-facing CMS layer.
Projects are the stable ecosystem identity layer.
Participations are round-specific.
GG23 has already been matched against Spark S6.
Do not reassign DSPJ IDs without checking the allocation preview.
Do not collapse LunCo and LORS into one project.
Do not remove failed or blank-status GG23 donation rows.
Do not publish email, Telegram usernames, reviewer real names, or private notes.
Donors are currently GG23-only draft, not canonical cross-round identities.
```
