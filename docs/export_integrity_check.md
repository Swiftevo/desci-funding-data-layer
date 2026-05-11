Before every snapshot/export:

1. Check row count matches expected project count.
2. Check project_entity_id uniqueness.
3. Check participation_id uniqueness.
4. Check raw_text is not empty.
5. Check max raw_text length.
6. Check whether raw_text still contains:
    Do not require a universal section format.
    For Artizen, verify [WHAT], [IMPACT], [PROGRESS], [WHY].
    For other sources, preserve and validate the original source structure.
7. Check CSV can be re-imported without row break.
8. Keep original production CSV as fallback.
