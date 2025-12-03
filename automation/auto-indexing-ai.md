# Auto-Indexing for AI (Concept)

This file sketches how an AI-first indexing layer might work later.

## Goal

Allow AI tools to:

- answer questions over the migrated docs
- suggest related documents
- generate draft articles from multiple sources

## Basic Steps

1. **Chunk the corpus** into pieces:
   - entire docs or smaller sections (see [auto-chunking-algorithm.md](automation/auto-chunking-algorithm.md)).
2. **Embed** each chunk:
   - use a sentence/paragraph-level embedding model.
3. Store:
   - the text
   - embeddings
   - document metadata (title, path, tags, etc.)
4. Build queries that:
   - embed the user’s question
   - retrieve top-N most relevant chunks
5. Use an LLM to:
   - synthesize answers
   - reference source docs as needed
   - propose related topics or missing docs.

All of this can be layered **on top of** the migrated Google Docs, without changing the docs themselves.
