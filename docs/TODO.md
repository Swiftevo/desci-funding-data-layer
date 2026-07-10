# TODO

## Phase 2 Classification Review

Do not manually review all provisional classifications immediately.

Classification review should happen after:

```text
Spark S6 import
Gitcoin GG23 import
Spark/GG23 project matching
```

After matching, generate:

```text
classification_review_queue.csv
```

Prioritize review for:

```text
1. Projects overlapping between Spark S6 and Gitcoin GG23
2. Projects with non-canonical Function values
3. Projects with missing Project type / Domain / Function
4. Projects with uncertain AI or mapping results
5. High-signal ecosystem projects
```

Goal:

```text
Review the most important records first instead of manually reviewing every provisional classification upfront.
```

## Project ID Allocation Rule

Draft imports must not reserve permanent `project_entity_id` values.

For Gitcoin GG23:

```text
project_entity_id remains empty during draft import
identity_status = pending_match
cross_round_match_status = pending_match
```

Only after Spark/GG23 matching review:

```text
confirmed match -> reuse existing Spark DSPJ ID
confirmed new_project -> assign next available DSPJ ID
provisional -> do not assign permanent DSPJ ID yet
rejected -> do not merge with rejected candidate
```

Reason:

```text
This prevents draft GG23 records from occupying DSPJ IDs before we know whether they already exist in Spark.
Future Spark new projects should receive IDs after all previously confirmed canonical new projects.
```
