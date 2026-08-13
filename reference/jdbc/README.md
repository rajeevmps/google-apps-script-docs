# JDBC Service Reference

Offline reference documentation for the Google Apps Script JDBC service, mirroring https://developers.google.com/apps-script/reference/jdbc/. The JDBC service allows scripts to connect to Google Cloud SQL, MySQL, Microsoft SQL Server, Oracle, and PostgreSQL databases.

## Classes

- [Jdbc](./Jdbc.md) — Top-level namespace for opening database connections (`getConnection`, `getCloudSqlConnection`) and constructing `Date`/`Time`/`Timestamp` values.
- [JdbcArray](./JdbcArray.md) — Represents a JDBC `Array`; retrieves the elements of a SQL array value.
- [JdbcBlob](./JdbcBlob.md) — Represents a JDBC `Blob`; reads and writes binary large object data.
- [JdbcCallableStatement](./JdbcCallableStatement.md) — Represents a JDBC `CallableStatement`; executes SQL stored procedures and retrieves output parameters.
- [JdbcClob](./JdbcClob.md) — Represents a JDBC `Clob`; reads and writes character large object data.
- [JdbcConnection](./JdbcConnection.md) — Represents a JDBC `Connection`; manages the connection lifecycle, transactions, and creation of statements.
- [JdbcDatabaseMetaData](./JdbcDatabaseMetaData.md) — Represents a JDBC `DatabaseMetaData`; provides metadata about the connected database and its capabilities.
- [JdbcDate](./JdbcDate.md) — Represents a JDBC `Date` value.
- [JdbcParameterMetaData](./JdbcParameterMetaData.md) — Represents a JDBC `ParameterMetaData`; provides metadata about the parameters of a prepared statement.
- [JdbcPreparedStatement](./JdbcPreparedStatement.md) — Represents a JDBC `PreparedStatement`; executes precompiled parameterized SQL statements.
- [JdbcRef](./JdbcRef.md) — Represents a JDBC `Ref`; a reference to a SQL structured type value.
- [JdbcResultSet](./JdbcResultSet.md) — Represents a JDBC `ResultSet`; the set of results returned by a database query, with cursor navigation and column accessors.
- [JdbcResultSetMetaData](./JdbcResultSetMetaData.md) — Represents a JDBC `ResultSetMetaData`; provides metadata about the columns in a `JdbcResultSet`.
- [JdbcRowId](./JdbcRowId.md) — Represents a JDBC `RowId`; the address of a row in a database table.
- [JdbcSQLXML](./JdbcSQLXML.md) — Represents a JDBC `SQLXML`; reads and writes SQL `XML` values.
- [JdbcSavepoint](./JdbcSavepoint.md) — Represents a JDBC `Savepoint`; a point within the current transaction that can be rolled back to.
- [JdbcStatement](./JdbcStatement.md) — Represents a JDBC `Statement`; executes static (non-parameterized) SQL statements.
- [JdbcStruct](./JdbcStruct.md) — Represents a JDBC `Struct`; the mapping of a SQL structured type value.
- [JdbcTime](./JdbcTime.md) — Represents a JDBC `Time` value.
- [JdbcTimestamp](./JdbcTimestamp.md) — Represents a JDBC `Timestamp` value.
