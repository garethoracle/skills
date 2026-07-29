# VecDB Python SDK Setup

Use this route when ORDS is available and the user is building a Python
application. The default path is **Python SDK → ORDS → database**. Oracle
VecDB requires Oracle AI Database 26ai+ at database version `23.26.3` or
later, and SDK access requires ORDS `26.2.2` or later.

## Install and connect

Install the public package exactly as follows:

```bash
python -m pip install oracle-vecdb
```

Start from an existing endpoint. Do not provision or create a database, ORDS,
schema, user, or credentials. Keep credentials in the local environment or a
secret manager, never in source or chat. Use only placeholders in examples.

```python
import os
from oracle_vecdb import Configuration, OracleVecDB

config = Configuration(
    rest_url=os.environ["VECDB_REST_URL"],  # https://<host>:<port>/ords/<schema>/_/db-api/stable/vecdb/
    username=os.environ.get("VECDB_USERNAME"),
    password=os.environ.get("VECDB_PASSWORD"),
)
vecdb = OracleVecDB(config)
```

When the existing environment uses bearer authentication, use its documented
`access_token` configuration with `VECDB_ACCESS_TOKEN` or `<bearer-token>`;
do not request a password as well. TLS verification stays enabled by default.
Use a configured custom CA when required; disabling verification is only a
temporary disposable-test exception.

## Discover before changes

```python
summary = vecdb.describe_vector_database()
models = vecdb.list_models()
tables = vecdb.list_vector_tables()
table = vecdb.describe_vector_table(table_name="<existing-table>")
```

Read `tables-and-data.md` for table/ingestion work, `search-and-rerank.md` for
retrieval, `model-management.md` for models, and `indexes-and-jobs.md` for
intentional index or job operations. Ask before any destructive, costly, or
long-running operation.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB. Use Oracle AI Database 26ai+ at
database version `23.26.3` or later. This SDK route also requires ORDS
`26.2.2` or later; use the approved `DBMS_VECTOR_DATABASE` PL/SQL route when
ORDS is unavailable or below that version.

## Sources

- Oracle Vector Database Python SDK API reference: https://docs.oracle.com/en/cloud/paas/autonomous-vector-database/vcapi/index.html
- Oracle VecDB PyPI package: https://pypi.org/project/oracle-vecdb/
