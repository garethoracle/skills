---
name: vecdb
description: Build, explain, troubleshoot, and evolve applications against an existing Oracle VecDB deployment using the public Python SDK, direct REST or non-Python needs, or DBMS_VECTOR_DATABASE PL/SQL when ORDS is unavailable; covers version checks, safe connection handling, models, tables, ingestion, search, reranking, indexes, and jobs.
---

# Oracle VecDB

Use this skill for an existing Oracle VecDB deployment only. VecDB requires
**Oracle AI Database 26ai+** at database version **23.26.3 or later**.
SDK and REST access through ORDS also requires **ORDS 26.2.2 or later**.
Do not present VecDB as supported on an older database.

## Start every live task

1. Determine whether ORDS is available and confirm the database version.
2. With ORDS, confirm ORDS 26.2.2 or later and collect an existing REST URL
   plus either username/password or the environment's bearer/API token. Do
   not ask the user to paste a secret in chat; use placeholders and local
   environment or secret-manager configuration.
3. Without ORDS, collect only the existing approved database connection
   details and authentication method needed by the user's PL/SQL client.
4. Never provision or create a database, ORDS deployment, schema, user, or
   credentials. Inspect summary, models, tables, and the relevant table before
   mutations.

## Route the request

| Situation                                                                         | Route                                                              | Read                                          |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------ | --------------------------------------------- |
| ORDS is available; application is Python                                          | Default: **Python SDK → ORDS → database**                          | `sdk-setup.md`, then the narrow workflow file |
| User explicitly needs HTTP, curl, OpenAPI-style, Go, or another non-Python client | Direct REST through ORDS; this is an explicit HTTP/non-Python path | `rest-api.md`                                 |
| ORDS is unavailable                                                               | Preferred route: `DBMS_VECTOR_DATABASE` PL/SQL                     | `dbms-vector-database.md`                     |
| Table definition, inline data, or bulk-load jobs                                  | Table/data lifecycle                                               | `tables-and-data.md`                          |
| Embedding or reranking model lifecycle                                            | Discover, load, describe, or drop models                           | `model-management.md`                         |
| Text, vector, or record-ID search; filters; reranking                             | Retrieval behavior                                                 | `search-and-rerank.md`                        |
| Intentional index configuration or asynchronous jobs                              | Indexes and job status/logs                                        | `indexes-and-jobs.md`                         |

## Safety boundary

Use read-only discovery first. Ask for explicit confirmation before dropping or
deleting resources, loading or dropping models, bulk ingestion, and creating,
rebuilding, or dropping indexes. Only offer cleanup for clearly named demo
resources owned by the workflow. Keep endpoints, credentials, customer data,
and storage locations out of source, logs, and final responses.

## First-response checklist for common situations

Keep the first response short, but make these decisions explicit before giving
an execution script:

| User situation                                                    | Required response                                                                                                                                                                                            |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| No connection details                                             | Ask **whether ORDS is available**. State `23.26.3` and ORDS `26.2.2`; with ORDS ask for the existing REST URL and local auth mechanism, and without ORDS ask only for the approved PL/SQL connection target. |
| Supported ORDS Python request                                     | Say **Python SDK → ORDS → database** and include `python -m pip install oracle-vecdb`. State that summary, models, tables, and table description are read-only discovery.                                    |
| Explicit HTTP/non-Python request                                  | Say `REST`, show `https://<host>:<port>/ords/<schema>/_/db-api/stable/vecdb/`, and use documented camelCase fields such as `queryBy`, `topK`, and `outputSelector`.                                          |
| ORDS is unavailable                                               | Say **ORDS is unavailable** and choose `DBMS_VECTOR_DATABASE`; do not require a REST URL or suggest ORDS setup.                                                                                              |
| Database below `23.26.3`                                          | Say VecDB is unsupported and stop; do not offer a VecDB workaround.                                                                                                                                          |
| ORDS below `26.2.2`                                               | Say SDK/REST is unsupported through that ORDS. Offer only `DBMS_VECTOR_DATABASE` if an approved existing database connection is available; do not continue with SDK instructions.                            |
| Bearer/API-token environment                                      | Accept the bearer token through `VECDB_ACCESS_TOKEN` or `<bearer-token>`; do not require a password or request a real token.                                                                                 |
| Drop, delete, bulk load, model lifecycle, or manual index request | Call it destructive, costly, or long-running. Ask for confirmation, then perform read-only discovery: list/describe the target and inspect relevant models/jobs before mutation.                             |

## Public SDK inventory

Use public `OracleVecDB` methods only. The supported method families include
`describe_vector_database()`, `list_models()`, `load_model()`,
`describe_model()`, `drop_model()`, `list_vector_tables()`,
`describe_vector_table()`, `create_vector_table()`,
`update_vector_table_annotation()`, `drop_vector_table()`,
`generate_embedding()`, `upsert_vectors()`, `list_vectors()`,
`delete_vectors()`, `load_vectors()`, `list_vector_load_jobs()`,
`describe_vector_load_job()`, `get_vector_load_job_log()`, `query()`,
`rerank()`, `create_index()`, `list_index_jobs()`,
`describe_index_job()`, `get_index_job_log()`, `rebuild_index()`,
`describe_index()`, and `drop_index()`. Consult the linked API guide for
current arguments, request/response shapes, and version-sensitive behavior;
do not infer or invent parameters.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB; do not offer a 19c fallback for
these workflows. Use Oracle AI Database 26ai+ at database version `23.26.3`
or later. Python SDK and direct REST access also require ORDS `26.2.2` or
later; without a supported ORDS deployment, use the approved
`DBMS_VECTOR_DATABASE` PL/SQL route instead.

## Sources

- Oracle Vector Database PLSQL API reference for DBMS_VECTOR_DATABASE: https://docs.oracle.com/en/database/oracle/oracle-database/26/arpls/
- Oracle Vector Database REST API reference: https://docs.oracle.com/en/database/oracle/oracle-rest-data-services/26.2/orrst
- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
