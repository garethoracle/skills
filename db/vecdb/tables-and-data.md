# VecDB Tables and Data

Use this reference for vector-table definition, annotations, inline data,
listing, deletion, and bulk-load jobs. Start with `list_vector_tables()` and
`describe_vector_table(table_name="<existing-table>")`. VecDB requires Oracle
AI Database 26ai+ at database version `23.26.3` or later.

## Table choices

Use integrated embeddings only after `list_models()` confirms a suitable loaded
model; configure the documented embedding parameters and upsert metadata that
contains the chosen text field. Use bring-your-own vectors only when the
application already supplies vectors with the correct dimensions. Use neutral,
clearly owned names such as `demo_documents` for examples.

Use public `create_vector_table()`, `update_vector_table_annotation()`,
`upsert_vectors()`, `list_vectors()`, `delete_vectors()`, and
`drop_vector_table()` only with their current documented arguments. Inspect
the table before changing it. Ask for explicit confirmation before delete or
drop, and never clean up a table the workflow does not own.

## Ingestion and jobs

Use small inline upserts for representative demo data. For a large staged
dataset, first ensure the target vector table already exists, then use the
documented `load_vectors()` bulk-load operation with a CSV file that is already
available at an approved object-storage URL. This is not a local-file loader.
Use only the user's existing object-storage location and credential
configuration when required; do not provision storage or create credentials.
Inspect `list_vector_load_jobs()`, `describe_vector_load_job()`, and
`get_vector_load_job_log()` afterward. Bulk load is costly or long-running: ask
for confirmation before starting it. Do not include real storage URLs,
credentials, or customer data in examples.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB tables or ingestion. Use Oracle AI
Database 26ai+ at database version `23.26.3` or later. This SDK workflow also
requires ORDS `26.2.2` or later.

## Sources

- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
