# DeSci Funding Data Layer

Open data infrastructure for decentralized science funding rounds, projects, and ecosystem research.

## Overview

This repository serves as a canonical archive and structured data layer for DeSci (Decentralized Science) funding ecosystems.

The project currently focuses on:

* Funding round project databases
* Structured project metadata
* Raw proposal preservation
* Participation tracking
* DeSci ecosystem mapping
* Open and machine-readable data formats

## Current Coverage

### Artizen Season 6 — Spark DeSci Round
https://artizen.fund/index/mf/spark-desci-fund-for-radical-researchers?season=6&scroll=no

* 49 DeSci projects
* Structured metadata
* Raw application archives
* Project classification system
* Stable ID system

## Architecture

The database uses a three-layer identity structure:

### Project Entity ID

Permanent project identity.

Example:
DSPJ-0001

### Funding Round ID

Funding round identity.

Example:
FR-ART-S6

### Participation ID

Unique participation instance per project per round.

Example:
DSPT-00001

## Repository Structure

```text
/schema
/data
/rounds
/snapshots
/exports
/docs
```

## Schema Status

Current version:
V1 Schema Freeze

The V1 schema focuses on:

* Stability
* Preservation
* Future interoperability
* AI-readable structure
* Cross-round compatibility

## Long-Term Goals

Future expansion may include:

* Additional funding rounds
* Cross-platform integrations
* Ecosystem analytics
* AI agents and retrieval systems
* Public APIs
* Knowledge graph infrastructure

## Notes

Notion is used as the human-facing management layer.

GitHub acts as the canonical archive and source-of-truth layer for structured exports and schema preservation.
