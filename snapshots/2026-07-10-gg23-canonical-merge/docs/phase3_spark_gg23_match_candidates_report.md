# Phase 3 Spark/GG23 Match Candidates Report

Date: 2026-06-25  
Status: Draft match candidates generated for human review

---

## Purpose

Generate candidate matches between:

```text
Spark S6 projects
Gitcoin GG23 draft participations
```

This report does not confirm any match.

All suggested overlaps remain:

```text
match_status = provisional
```

until human review.

---

## Generated Files

```text
data/matching/spark_gg23_match_candidates.csv
data/matching/spark_gg23_match_candidates.json
```

---

## Summary

| Check | Result |
| --- | ---: |
| GG23 applications reviewed | 21 |
| Provisional match candidates | 8 |
| New project candidates | 13 |
| Unique GG23 application IDs | 21 |

---

## Provisional Match Candidates

These require human review.

| GG23 Application ID | GG23 Project | Spark Candidate ID | Spark Candidate | Confidence | Basis |
| --- | --- | --- | --- | ---: | --- |
| 1 | DeSci Asia | DSPJ-0029 | DeSci Asia | 0.99 | manual_seed_exact_name |
| 3 | FunDeSci (DeSci Fundraising platfrom) | DSPJ-0049 | FunDeSci | 0.95 | manual_seed_name_contains |
| 8 | AsteriskDAO | DSPJ-0045 | Asterisk Women Health | 0.62 | manual_review_name_prefix |
| 9 | The DeSci Journals v4 (Celo) | DSPJ-0040 | DeSci Reviews | 0.78 | manual_seed_project_alias |
| 15 | Hyvmind | DSPJ-0005 | hyvmind | 0.99 | manual_seed_case_normalized_name |
| 18 | overlake bio | DSPJ-0030 | Overlake Bio | 0.90 | manual_seed_name_contains |
| 26 | DeSci Round working group | DSPJ-0027 | Spark DeSci | 0.65 | manual_review_round_operator_overlap |
| 29 | DeSci LATAM | DSPJ-0047 | DeSci Mexico | 0.42 | manual_review_regional_ecosystem_overlap |

Note:

```text
Low-confidence candidates are included to support human review.
They should not be treated as confirmed matches.
```

---

## New Project Candidates

These did not receive a strong Spark S6 candidate from the current matching pass.

```text
LunCo: Metaverse for Space Engineers
DeSci Youths
MesoReefDAO - Regenerating Reef Conservation with DeSci Web3 tools
Astral
HyperDeSci Ops | Summoning $MEGAPI
OpenLitterMap: Real-Time In-World Open Source Gamification System
?RTH - Planetary AI
Ideosphere
EcoSynthesisX
NetX State
Register deSci MAXi
Maxi DeSci Metaverse
Dash Mon[k]ey
```

Important:

```text
new_project here means "no strong Spark candidate found yet".
It does not assign a permanent DSPJ ID.
```

---

## Matching Method

Candidate generation used:

```text
normalized name similarity
token overlap
name contains matching
manual review seeds for obvious or important cases
```

Manual review seeds were used for:

```text
DeSci Asia
FunDeSci
The DeSci Journals v4
Hyvmind
overlake bio
AsteriskDAO
DeSci Round working group
DeSci LATAM
```

---

## Required Human Actions

For each provisional candidate, choose one:

```text
confirmed
rejected
keep provisional
```

For each new project candidate, choose one:

```text
new_project
provisional match to an existing Spark project
needs more source review
```

Only after human review should canonical merge proceed.

---

## Next Step

Review:

```text
data/matching/spark_gg23_match_candidates.csv
```

Then update:

```text
match_status
confirmed_by
confirmed_at
match_notes
```

After confirmation, canonical merge can:

```text
reuse existing DSPJ IDs for confirmed matches
assign new DSPJ IDs only to confirmed new projects
```

