# AI-First Future Architecture (Short Sketch)

This is **not** required for today’s migration, but describes where we want the content
to plausibly go later.

## Target Model

- **Storage layer:** Google Docs files in reasonably sized "topic docs".
- **Indexing layer:** embedding / vector index over the docs (or over sub-doc chunks).
- **Knowledge layer:** LLM-based services that:
  - answer questions over the corpus
  - propose related docs / concepts
  - generate draft articles from multiple notes
  - highlight gaps or contradictions

## Implications for Today

To keep migration simple **and** future-compatible, we:

- keep one topic per doc where feasible (when we eventually split/merge)
- avoid extremely deep folder trees
- give docs clear, semantic titles (good for search today, embeddings tomorrow)
- avoid over-engineering navigation; assume **search + semantics** win long-term
