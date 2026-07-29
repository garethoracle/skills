# VecDB Model Management

Use model lifecycle operations only when the user asks to discover, load,
describe, or drop a model, or needs documented embedding or reranking support.
VecDB requires Oracle AI Database 26ai+ at database version `23.26.3` or later.

Use `list_models()`, `load_model()`, `describe_model(model_name="<model-name>")`,
and `drop_model(model_name="<model-name>")` for the documented model lifecycle.
Start with `list_models()` and describe the relevant loaded model before using
or changing it.
Use integrated embeddings for table ingestion when a suitable model is already
loaded; use the documented `generate_embedding()` and `rerank()` operations
only when the application actually needs standalone inference. Do not hard-code
a model name before discovery.

Loading and dropping models can be costly or destructive. Ask for explicit
confirmation and verify dependencies before either action. Do not put model
sources, storage URLs, credentials, or private data in committed material.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB model management. Use Oracle AI
Database 26ai+ at database version `23.26.3` or later. This SDK workflow also
requires ORDS `26.2.2` or later.

## Sources

- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
