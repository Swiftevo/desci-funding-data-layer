# Data Layer

This folder contains the structured data exports for the DeSci Funding Data Layer.

---

# Structure

## csv/

Human-readable and spreadsheet-compatible exports.

Used for:

* Notion imports
* manual review
* archival preservation

---

## json/

Machine-readable structured exports.

Used for:

* AI systems
* APIs
* automation
* retrieval pipelines
* future embeddings

---

# Current Dataset

## Artizen Season 6 — Spark DeSci Round

* 49 projects
* structured metadata
* participation IDs
* raw proposal preservation
* category classification system

---

# Notes

CSV exports are designed to be:

* UTF-8 BOM compatible
* RFC4180 compliant
* Excel-safe
* Notion-safe

Raw proposal text is preserved without summarization inside the `raw_text` field.
