# Google Docs Atomic Chunking Pipeline (Optional, Later)

This pipeline is **not** required for first-pass migration. It is a follow-up step
to move from "1 doc per Confluence page" toward smaller, "atomic" topic notes.

## Goals

- Create smaller, concept-sized docs (atomic notes) from larger Google Docs.
- Keep the process **mechanical**:
  - split by headings
  - apply predictable naming rules
- Do not delete or destroy the original docs.

## High-Level Flow

```text
Google Doc (converted from Confluence page)
    ↓ (analyze headings)
Section-level docs per H1/H2
    ↓
Original doc retained as reference
```

## Rules of Thumb

- Use **H1 / H2** boundaries to define chunks.
- Each section becomes a new doc named:

  `Original Title — Section Heading`

  Example:

  - `API Guide`
  - `API Guide — Overview`
  - `API Guide — Authentication`
  - `API Guide — Errors`

- Keep links or context (e.g. a short “Source: Original Doc” note) if desired.

## Why Later, Not Now

- Migration needs to be **fast and low-friction**.
- Chunking introduces another layer of complexity.
- Doing it mechanically but separately gives us:
  - a working, navigable corpus now
  - the option to refine structure when we have time or better tools.
