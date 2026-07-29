# DBMS_VECTOR_DATABASE PL/SQL

When ORDS is unavailable, prefer `DBMS_VECTOR_DATABASE` through the user's
existing approved PL/SQL client connection. VecDB requires Oracle AI Database
26ai+ at database version `23.26.3` or later. ORDS is not required for this
PL/SQL route.

Do not request a REST URL, and do not provision or create a database, ORDS,
schema, user, or credentials. Ask only for the existing approved connection
target and authentication method appropriate to the PL/SQL client.

## Discover first

Use read-only `DBMS_VECTOR_DATABASE` discovery before any mutation: database
summary, `LIST_MODELS`, `LIST_VECTOR_TABLES`, and `DESCRIBE_VECTOR_TABLE` for
the relevant table. Treat returned JSON/CLOB responses according to the
documented package contract.

```sql
declare
  l_response clob;
begin
  l_response := dbms_vector_database.list_vector_tables();
  dbms_output.put_line(dbms_lob.substr(l_response, 4000, 1));
end;
/
```

Use the documented package operations for table/data lifecycle, `SEARCH`,
`RERANK`, models, and indexes. Do not mix Python SDK method names into PL/SQL
examples. Ask for explicit confirmation before drop/delete, model load/drop,
bulk loading, or index create/rebuild/drop.

## Oracle Version Notes (19c vs 26ai)

Oracle Database 19c does not support `DBMS_VECTOR_DATABASE` VecDB workflows.
Use Oracle AI Database 26ai+ at database version `23.26.3` or later. ORDS is
not required for this approved PL/SQL route.

## Sources

- Oracle Vector Database PLSQL API reference for DBMS_VECTOR_DATABASE: https://docs.oracle.com/en/database/oracle/oracle-database/26/arpls/
