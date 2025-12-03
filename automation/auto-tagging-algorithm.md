# Auto-Tagging Algorithm (Concept)

This is a future, nice-to-have automation, not required for the migration.

## Goal

Assign helpful tags or keywords to docs without manual curation, to support:

- better search
- better AI clustering
- easier discovery for humans

## Basic Approach

For each doc:

1. Extract text (title + body).
2. Run a keyword/phrase extraction process (could be:
   - simple TF/IDF
   - LLM-assisted summarization
   - a mix of both).
3. Filter for:
   - relevance (remove stopwords, boilerplate)
   - limited number of tags (e.g. 3–10 per doc)
4. Store tags:
   - inside the doc (e.g. a “Tags:” line at the top or bottom), or
   - in an external index (database, YAML, etc.).

This can be done after migration, in batches, focusing on the most important spaces first.
