# Auto-Chunking Algorithm (Concept)

This algorithm is **optional** and intended for a later refinement pass.

## Goal

Turn larger Google Docs (converted from Confluence pages) into multiple, smaller,
section-level docs **without manual editing**.

## Inputs

- A Google Doc with headings (`H1`, `H2`, etc.).
- A decision on which heading levels define chunks (e.g. `H1` and `H2`).

## Basic Algorithm

For each selected document:

1. Read the document structure:
   - parse headings and their ranges.
2. For each top-level heading (e.g. `H1` or `H2`):
   - extract that heading and its content until the next heading of the same level.
   - create a new Google Doc with:
     - title: `Original Title — Section Heading`
     - body: the extracted section content.
3. Optionally, add a short note in each section doc:
   - “Source: [link to original doc]”
4. Leave the original doc untouched as a “full” reference.

## Result

- A set of smaller, more focused docs suitable for:
  - human navigation
  - AI embedding and retrieval
- A preserved original doc that still contains the whole page for context.

Implementation details (API, tooling) are intentionally deferred.
