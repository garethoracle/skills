# VecDB Indexes and Jobs

VecDB manages indexes by default. Use this reference only when the user
intentionally needs manual index configuration, delayed indexing, tuning,
rebuild/drop work, or asynchronous job inspection. VecDB requires Oracle AI
Database 26ai+ at database version `23.26.3` or later.

First inspect the vector table, its index state, and existing jobs. Prefer
automatic/default indexing unless there is a stated need to override it. Index
creation, rebuild, drop, and bulk-load follow-up can be costly or long-running:
explain the impact and ask for explicit confirmation before acting.

Use the public documented methods `create_index()`, `list_index_jobs()`,
`describe_index_job()`, `get_index_job_log()`, `rebuild_index()`,
`describe_index()`, and `drop_index()` to manage index state and jobs. Do not
treat job submission as completion; re-read status and diagnose the log when
necessary. Never rebuild or drop an index that may be shared without explicit
user intent and ownership.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB index management. Use Oracle AI
Database 26ai+ at database version `23.26.3` or later. This SDK workflow also
requires ORDS `26.2.2` or later.

## Sources

- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
