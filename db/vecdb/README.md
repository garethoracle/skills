# Oracle VecDB Skill

This package guides safe work against an existing Oracle VecDB deployment.
VecDB requires Oracle AI Database 26ai+ with database version `23.26.3` or
later. SDK/REST through ORDS requires ORDS `26.2.2` or later.

- `SKILL.md` — entry-point routing and connection/safety rules.
- `sdk-setup.md` — default Python SDK -> ORDS -> database route.
- `rest-api.md` — direct REST for explicit HTTP or non-Python needs.
- `dbms-vector-database.md` — preferred `DBMS_VECTOR_DATABASE` route without ORDS.
- `tables-and-data.md` — vector tables, ingestion, and load jobs.
- `model-management.md` — model discovery and intentional lifecycle work.
- `search-and-rerank.md` — query shapes, filters, and reranking.
- `indexes-and-jobs.md` — deliberate index work and job inspection.
- `prompts/` — standalone Copy Prompt instructions for three solution types.
- `agents/openai.yaml` — skill UI metadata.

Do not provision or create a database, ORDS, schema, user, or credentials.
Use an existing connection target, placeholders only, and read-only discovery
before mutations.
