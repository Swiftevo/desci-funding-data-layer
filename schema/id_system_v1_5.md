# ID System V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

The V1.5 ID system extends the V1 identifier model without changing existing V1 IDs.

V1 already defines:

```text
DSPJ = DeSci Project
FR = Funding Round
DSPT = DeSci Participation
```

V1.5 keeps these IDs stable and activates additional prefixes for analysis tables:

```text
DSDN = DeSci Donor
DSRV = DeSci Reviewer
DSEV = DeSci Event
```

---

## Core Rule

IDs must remain:

- stable
- permanent
- non-semantic
- platform-independent
- machine-readable
- never recycled

IDs should not encode:

- category
- country
- chain
- funding result
- review decision
- current project status

---

## Project Entity ID

Purpose: permanent identity for a real DeSci project.

Format:

```text
DSPJ-0001
```

Rules:

- One real project receives one `project_entity_id`.
- The same project keeps the same ID across Spark, Gitcoin, and future rounds.
- Name changes do not change the ID.
- Platform-specific names are stored as source names or aliases.

---

## Funding Round ID

Purpose: stable identity for one funding round.

Format:

```text
FR-ART-S6
FR-GTC-GG23-DESCI
```

Recommended Gitcoin DeSci round IDs:

| funding_round_id | Round |
| --- | --- |
| FR-GTC-GR15-DESCI | Gitcoin GR15 DeSci Community Round |
| FR-GTC-BETA-DESCI | Gitcoin Beta DeSci Community Round |
| FR-GTC-GG20-DESCI | Gitcoin GG20 DeSci Community Round |
| FR-GTC-GG21-DESCI | Gitcoin GG21 DeSci Community Round |
| FR-GTC-GG23-DESCI | Gitcoin GG23 DeSci Community Round |

Rules:

- One funding event receives one `funding_round_id`.
- The ID represents the round, not the operator, result, or dataset completeness.
- Historical rounds may exist as metadata-only records before detailed backfill.

---

## Participation ID

Purpose: stable identity for one project participating in one funding round.

Format:

```text
DSPT-00001
```

Rules:

- One project in one round receives one participation ID.
- If the same project appears in five rounds, it has five participation IDs.
- Participation IDs remain stable after project matching is confirmed.
- Provisional matches should not overwrite existing IDs without human confirmation.

---

## Donor ID

Purpose: stable internal ID for a donor wallet.

Format:

```text
DSDN-000001
```

Rules:

- One wallet address should map to one donor ID.
- Wallet address remains the public analytical key.
- Donor ID is useful when joining data across multiple donation files.
- Do not infer off-chain identity from wallet address.

---

## Reviewer ID

Purpose: anonymized public ID for reviewers.

Format:

```text
GTC-GG23-RV01
```

or, if a global reviewer registry is needed later:

```text
DSRV-0001
```

Phase 1 rule:

- Use round-scoped anonymized reviewer IDs.
- Do not publish reviewer real names.

Examples:

```text
GTC-GG23-RV01
GTC-GG23-RV02
GTC-GG23-RV03
GTC-GG23-RV04
```

---

## Event ID

Purpose: stable ID for source-level events such as donations or votes.

Format:

```text
DSEV-0000001
```

Rules:

- Use one event ID per donation or vote event when creating internal event records.
- Preserve the original source event ID separately as `source_donation_id`.
- Do not replace source IDs with internal IDs; keep both.

---

## Matching Status

Project matching uses:

```text
provisional
confirmed
rejected
new_project
```

Rules:

- AI or scripts may propose `provisional` matches.
- Human confirmation is required for `confirmed`.
- Confirmed matches should include `confirmed_by` and `confirmed_at`.
- Rejected matches should preserve enough notes to avoid repeating the same false match.

