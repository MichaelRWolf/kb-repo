# Link Cleaning Strategy (Concept)

We are **not** depending on link rewriting for core migration, but it’s useful to have
a strategy for cleaning or improving links later.

## Current State After Migration

- Original Confluence links may be:
  - broken (still pointing to Confluence URLs), or
  - preserved only as text.
- Google Docs supports:
  - hyperlinks to other docs
  - @-mentions of docs/people

## Possible Future Steps

1. **Detect Confluence URLs** inside docs.
2. **Map Confluence page IDs / titles → Drive doc IDs**:
   - using an index built from the export + the migrated docs.
3. Replace:
   - raw Confluence URLs with hyperlinks to the corresponding Google Docs.
4. Optionally:
   - add a note at the top of docs with many incoming links (“Frequently referenced from …”).

This is a non-trivial automation and may or may not be worth doing, depending on how much
the old link graph still matters once people are using search.
