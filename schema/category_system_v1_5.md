# Category System V1.5

Version: V1.5  
Status: Draft for implementation

---

## Overview

V1.5 continues to use the V1 category system as the canonical classification layer.

The main V1 category layers remain:

```text
Project Type
Domain
Function
```

These categories support cross-round comparison across Spark, Gitcoin, and future funding sources.

---

## Canonical Category Source

The canonical category source remains:

```text
schema/category_system.md
```

V1.5 does not redefine the category list. It defines how categories should be applied in a multi-round model.

---

## Where Categories Belong

### Project-Level Categories

Long-term classification belongs in `projects`:

```text
project_type
domain
function
```

Use project-level categories when they describe what the project fundamentally is across rounds.

Example:

```text
Project: DeSci Asia
Project Type: Community
Domain: Education
Function: Community Building, Education
```

### Participation-Level Categories

Round-specific classifications may be stored in `participations` when needed:

```text
source_specific_fields_json
round_specific_project_type
round_specific_domain
round_specific_function
```

Use participation-level categories when a platform or round has its own tagging system or when the project presents a different focus in a specific round.

---

## Classification Status

Use `classification_status` to avoid forcing premature certainty:

```text
unclassified
provisional
confirmed
```

Rules:

- `unclassified`: no category assigned yet.
- `provisional`: initial AI or human suggestion, not final.
- `confirmed`: reviewed and accepted by a human curator.

---

## Round-Specific Extensions

Round-specific category extensions are allowed, but they should not casually change the canonical category system.

If a source platform has a category not present in V1:

1. Preserve the original value in source-specific fields.
2. Map it to the closest V1 category when possible.
3. If no suitable V1 value exists, document the proposed extension.

Recommended fields:

```text
source_category_raw
canonical_category_mapped
classification_status
classification_notes
```

---

## Extension Review Rule

New canonical category values should only be added when:

- multiple projects require the value
- no existing category is sufficient
- the category improves cross-round analysis
- the change is documented in schema notes

---

## AI Classification Rule

AI may assist with classification, but AI-generated categories should begin as:

```text
classification_status = provisional
```

Human review is required before:

```text
classification_status = confirmed
```

---

## Preservation Rule

Never delete source-native category or tag values.

If a platform provides a tag that does not match the canonical system, preserve it in:

```text
source_specific_fields_json
```

or in a source-specific raw field.

