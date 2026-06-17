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

