# VecDB Search and Reranking

Use `query()` for documented text, dense-vector, or record-ID retrieval.
VecDB requires Oracle AI Database 26ai+ at database version `23.26.3` or later.
Select the query shape that matches the table: text needs integrated embeddings;
vector search needs a compatible vector; record-ID search finds similar records.

Ask for only needed outputs such as title, content snippet, metadata, and
similarity/distance. Apply documented metadata filters and a bounded `top_k`.
Do not copy filter syntax from another vector database. Use advanced options
only when the user needs a recall, latency, or distance-metric adjustment.

Rerank only after initial retrieval and only when discovery confirms a
documented reranking model. Preserve the mapping from reranked items to
retrieved metadata. Retrieval itself is read-only; changing tables, models, or
indexes requires the relevant confirmation in the linked reference.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB search or reranking. Use Oracle AI
Database 26ai+ at database version `23.26.3` or later. This SDK workflow also
requires ORDS `26.2.2` or later.

## Sources

- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
