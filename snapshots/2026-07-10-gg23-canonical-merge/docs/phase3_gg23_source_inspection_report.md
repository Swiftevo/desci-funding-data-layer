# Phase 3 Gitcoin GG23 Source Inspection Report

Date: 2026-06-18  
Status: Source inspection only  
Round: `FR-GTC-GG23-DESCI`

---

## Purpose

Inspect the Gitcoin GG23 DeSci Community Round source files before generating V1.5 tables.

No formal V1.5 Gitcoin tables have been generated yet.

---

## Source Files

Local source files inspected:

```text
C:\Users\User\Desktop\gitcoin grant 23 desci community round project information.txt
C:\Users\User\Desktop\gitcoin grant 23 desci community round small donation.txt
```

Both files are tab-separated text files.

---

## Project Information File

### Summary

| Check | Result |
| --- | ---: |
| Rows | 21 |
| Columns | 20 |
| Unique `id` values | 21 |
| Unique `projectId` values | 21 |
| Status values | Approved |
| Empty title | 0 |
| Empty project description | 0 |

### Columns

```text
id
projectId
status
title
payoutAddress
signature
website
projectTwitter
projectGithub
userGithub
Funding Sources and Total prior funding for project in USD
Team Size
Profiles or socials of other main team members publicly associated with project
How old is the project? (Months)
Describe your project in a few paragraphs (ideally including a problem statement, solution, roadmap, and timeline for implementation)
How does your project support the mission or goals of DeSci?
Describe how funds from the grants program will be used for your project.
If you participated in past grant rounds (i.e. DeSci GR15/ Beta/GG 20DeSci round/GG21 DeSci round) using a different project payout wallet address, please share it here.
If this project participated in past DeSci grant rounds, please share any new updates or milestones since the last round.
Is there any other information you would like to share about your project, previous work, other project affiliations, or potential conflicts of interest? (or anything not covered elsewhere in this application that you feel is relevant to share)
```

### Public / Private Notes

This project information file does not include:

```text
Email Address
Telegram username
reviewer real names
```

This makes it suitable for public archive mapping, subject to normal review.

---

## Donation File

### Summary

| Check | Result |
| --- | ---: |
| Rows | 274 |
| Columns | 16 |
| Unique donation IDs | 274 |
| Unique projectId values | 21 |
| Unique applicationId values | 21 |
| Unique voters | 80 |
| Unique grantAddress values | 19 |
| roundId values | 28 |

### Columns

```text
id
projectId
applicationId
roundId
token
voter
grantAddress
amount
amountUSD
coefficient
status
last_score_timestamp
type
success
rawScore
threshold
```

### Status Distribution

```text
DONE: 238
blank: 36
```

### Success Distribution

```text
TRUE: 147
FALSE: 91
blank: 36
```

### Type Distribution

```text
ThresholdScoreCheck: 238
blank: 36
```

### Amount Summary

```text
total donation events: 274
total amountUSD: 801.8001
DONE amountUSD: 630.2020
blank-status amountUSD: 171.5982
```

Important:

```text
The filename includes "small donation". Confirm whether this file represents all GG23 donation events or only a filtered subset before treating amountUSD as final round totals.
```

---

## Join Integrity

### Project ID Join

Donation `projectId` values match project information `projectId` values.

| Check | Result |
| --- | ---: |
| Donation projectIds missing from project file | 0 |
| Project file projectIds without donations | 0 |

### Application ID Join

Donation `applicationId` values match project information `id` values.

| Check | Result |
| --- | ---: |
| Donation applicationIds missing from project file | 0 |
| Project information ids without donations | 0 |

### Address Join

Donation `grantAddress` values match project information `payoutAddress` values.

| Check | Result |
| --- | ---: |
| Unique payoutAddress values | 19 |
| Unique grantAddress values | 19 |
| grantAddress not found in payoutAddress | 0 |
| payoutAddress not found in grantAddress | 0 |

---

## Duplicate Address Note

There are 21 approved projects but only 19 unique payout/grant addresses.

One payout address appears across three project records:

```text
0x9b9dbC177fbE6A32bBc92A44B04B5d6711e151de
```

Associated application IDs and titles:

```text
9  - The DeSci Journals v4 (Celo)
23 - Register deSci MAXi
25 - Maxi DeSci Metaverse
```

Interpretation:

```text
This is not automatically an error.
It should be preserved because it may be useful for project identity, payout linkage, and future anti-sybil or ecosystem graph analysis.
```

---

## Proposed Mapping Direction

### Project Information

Map to:

```text
data/projects/
data/participations/
```

Likely mapping:

| Source Field | Target |
| --- | --- |
| id | source_application_id |
| projectId | source_project_id |
| status | application_status / source_status |
| title | source_project_name and candidate canonical_project_name |
| payoutAddress | payout_address |
| website | website candidate |
| projectTwitter | project_twitter |
| projectGithub | project_github |
| userGithub | user_github |
| application question fields | raw_text and source_specific_fields_json |

### Donations

Map to:

```text
data/donations/
data/donors/
```

Likely mapping:

| Source Field | Target |
| --- | --- |
| id | source_donation_id |
| projectId | source_project_id |
| applicationId | source_application_id |
| roundId | round_source_id |
| token | token_address |
| voter | donor_wallet |
| grantAddress | grant_address |
| amount | amount_raw |
| amountUSD | amount_usd |
| coefficient | coefficient |
| status | status |
| last_score_timestamp | last_score_timestamp |
| type | score_type |
| success | success |
| rawScore | raw_score |
| threshold | threshold |

---

## Next Step

Before generating V1.5 Gitcoin GG23 tables, confirm:

1. Whether the donation file is complete or only a small-donation subset.
2. Whether `status = blank` donation rows should be preserved in public donations.
3. Whether `success = FALSE` rows should be preserved in public donations.
4. Whether the three projects sharing one payout address are expected.

After confirmation, generate a Gitcoin GG23 mapping report.

