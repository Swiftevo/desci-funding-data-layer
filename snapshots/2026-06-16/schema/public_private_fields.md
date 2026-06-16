# Public and Private Field Policy V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

The DeSci Funding Data Layer is intended to be a public, machine-readable GitHub archive.

Because source datasets can contain personal contact information and private reviewer identity, V1.5 defines explicit public/private field rules.

---

## Public Archive Includes

The public archive may include:

```text
project name
website
project Twitter
project GitHub
user GitHub
payout address
donor wallet
grant address
application raw text
donation amount
anonymized reviewer score
funding result
source project ID
source application ID
round metadata
```

These fields are included because they support:

- project identity tracking
- ecosystem analysis
- funding graph analysis
- anti-sybil research
- AI retrieval
- public archival durability

---

## Public Archive Excludes

The public archive must exclude:

```text
Email Address
Telegram username
reviewer real names
private notes
private reviewer comments
internal conflict discussions
```

These fields may exist in private working files, but they must not be published in the canonical public GitHub export.

---

## Reviewer Identity

Reviewer real names are not public.

Use anonymized IDs such as:

```text
GTC-GG23-RV01
GTC-GG23-RV02
GTC-GG23-RV03
GTC-GG23-RV04
```

---

## Contact Fields

The following source fields are treated as private contact fields:

```text
Email Address
Telegram username
```

They should be excluded from:

- public CSV exports
- public JSON exports
- public snapshots
- public GitHub documentation examples

---

## Wallet and Address Fields

The following fields may be public:

```text
payout address
donor wallet
grant address
```

Reason:

- Gitcoin funding analysis requires wallet-level donor data.
- Payout and grant addresses help identify projects across rounds.
- Wallet-level data supports future anti-sybil and funding graph analysis.

Do not infer off-chain personal identity from wallet addresses unless explicitly present in a public source.

---

## Raw Application Text

Raw application text is public unless it contains private contact fields or other sensitive material that must be redacted.

Source-aware raw text should preserve the original structure of each platform.

For Gitcoin GG23, recommended sections include:

```text
[PROJECT DESCRIPTION]
[DESCI MISSION ALIGNMENT]
[USE OF FUNDS]
[PAST ROUND WALLET]
[NEW UPDATES]
[OTHER INFORMATION]
[DIVERSITY QUESTION]
```

For Spark / Artizen, preserve the existing structure:

```text
[WHAT]
[IMPACT]
[PROGRESS]
[WHY]
```

