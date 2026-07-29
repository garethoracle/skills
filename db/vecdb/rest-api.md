# VecDB REST API

Use direct REST only for an explicit HTTP, curl, OpenAPI-style, or non-Python
need. Otherwise, when ORDS is available, prefer **Python SDK -> ORDS ->
database**. REST requires Oracle AI Database 26ai+ at database version
`23.26.3` or later and ORDS `26.2.2` or later.

## Existing endpoint and authentication

Use the existing VecDB ORDS base URL, with public-safe placeholders only:

```text
https://<host>:<port>/ords/<schema>/_/db-api/stable/vecdb/
```

Use the target's existing basic or bearer authentication mechanism. Do not
provision or create a database, ORDS, schema, user, or credentials; never put
secrets in files, logs, or responses.

## Read-only discovery and query shape

Inspect summary, models, vector tables, and the target table before mutation.
Use documented camelCase REST request fields. For example, a text retrieval
body uses `queryBy`, `topK`, `outputSelector`, and documented filters:

```json
{
  "queryBy": {"text": "example query"},
  "topK": 5,
  "filters": {"category": {"$eq": "example"}},
  "outputSelector": ["title", "content"],
  "includeVectors": false
}
```

Ask for explicit confirmation before delete/drop, model lifecycle, bulk load,
or manual index work. Use only documented endpoint paths and request bodies;
refer to the current public REST API reference for the narrow operation.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support VecDB REST workflows. Use Oracle AI
Database 26ai+ at database version `23.26.3` or later, with ORDS `26.2.2` or
later. Use the approved `DBMS_VECTOR_DATABASE` PL/SQL route when ORDS is
unavailable or below that version.

## Sources

- Oracle Vector Database REST API reference: https://docs.oracle.com/en/database/oracle/oracle-rest-data-services/26.2/orrst
