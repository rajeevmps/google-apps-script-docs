# JdbcDatabaseMetaData

A JDBC database metadata object. For documentation of this class, see `java.sql.DatabaseMetaData` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html).

## Methods

### allProceduresAreCallable()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#allProceduresAreCallable()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#allProceduresAreCallable()).

**Returns:** `Boolean` — `true` if the user can call all of the procedures returned by `getProcedures(catalog, schemaPattern, procedureNamePattern)`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### allTablesAreSelectable()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#allTablesAreSelectable()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#allTablesAreSelectable()).

**Returns:** `Boolean` — `true` if the user can call all of the tables returned by `getTables(catalog, schemaPattern, tableNamePattern, types)` in a `SELECT` statement; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### autoCommitFailureClosesAllResultSets()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#autoCommitFailureClosesAllResultSets()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#autoCommitFailureClosesAllResultSets()).

**Returns:** `Boolean` — `true` if, when `autoCommit` is `true`, a SQL exception indicates that all open result sets are closed, even if holdable. Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### dataDefinitionCausesTransactionCommit()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#dataDefinitionCausesTransactionCommit()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#dataDefinitionCausesTransactionCommit()).

**Returns:** `Boolean` — `true` if a data definition statement within a transaction forces the transaction to commit; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### dataDefinitionIgnoredInTransactions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#dataDefinitionIgnoredInTransactions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#dataDefinitionIgnoredInTransactions()).

**Returns:** `Boolean` — `true` if the database ignores a data definition statement within a transaction; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### deletesAreDetected(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#deletesAreDetected(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#deletesAreDetected(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the specified result set type a visible row delete is detected by calls to `JdbcResultSet.rowDeleted()`. If `false`, the deleted rows are removed from the result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### doesMaxRowSizeIncludeBlobs()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#doesMaxRowSizeIncludeBlobs()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#doesMaxRowSizeIncludeBlobs()).

**Returns:** `Boolean` — `true` if SQL data types `LONGVARCHAR` and `LONGVARBINARY` are included in the size returned by `getMaxRowSize()`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getAttributes(catalog, schemaPattern, typeNamePattern, attributeNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getAttributes(String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getAttributes(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `typeNamePattern` (String): The user-defined type name pattern; it must match the type name as it is stored in the database.
- `attributeNamePattern` (String): The attribute name pattern; it must match the attribute name as it is declared in the database.

**Returns:** `JdbcResultSet` — A result set containing descriptions the attributes for a specified user-defined type available in the specified schema and catalog. Each row provides information about a specific attribute, ordered by `TYPE_CAT`, `TYPE_SCHEM`, `TYPE_NAME`, and `ORDINAL_POSITION`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBestRowIdentifier(catalog, schema, table, scope, nullable)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getBestRowIdentifier(String, String, String, int, boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getBestRowIdentifier(java.lang.String,%20java.lang.String,%20java.lang.String,%20int,%20boolean)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.
- `scope` (Integer): The scope of interest, using the same values as present in the `SCOPE` column description column.
- `nullable` (Boolean): If `true`, include columns that are nullable; otherwise do not.

**Returns:** `JdbcResultSet` — A result set containing the column descriptions that uniquely identify a row (one column description per row in the result set, ordered by `SCOPE`).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCatalogSeparator()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getCatalogSeparator()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getCatalogSeparator()).

**Returns:** `String` — The separator between a catalog and table name used by this database.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCatalogTerm()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getCatalogTerm()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getCatalogTerm()).

**Returns:** `String` — The database vendor's preferred term for 'catalog'.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCatalogs()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getCatalogs()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getCatalogs()).

**Returns:** `JdbcResultSet` — A result set containing the catalog names, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getClientInfoProperties()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getClientInfoProperties()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getClientInfoProperties()).

**Returns:** `JdbcResultSet` — A result set containing client info properties the driver supports, ordered by `NAME`, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnPrivileges(catalog, schema, table, columnNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getColumnPrivileges(String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getColumnPrivileges(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The name of the schema to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.
- `columnNamePattern` (String): The column name pattern to filter the search by. It must match the column name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the column privilege descriptions, one per row, ordered by `COLUMN_NAME` and `PRIVILEGE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumns(catalog, schemaPattern, tableNamePattern, columnNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getColumns(String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getColumns(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `tableNamePattern` (String): The table name pattern to filter the search by. It must match the table name as it is stored in the database.
- `columnNamePattern` (String): The column name pattern to filter the search by. It must match the column name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the column descriptions, one per row, ordered according to `TABLE_CAT`, `TABLE_SCHEM`, `TABLE_NAME`, and `ORDINAL_POSITION`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getConnection()

Returns: `JdbcConnection`

For documentation of this method, see `java.sql.DatabaseMetaData#getConnection()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getConnection()).

**Returns:** `JdbcConnection` — The connection that produced this metadata.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCrossReference(parentCatalog, parentSchema, parentTable, foreignCatalog, foreignSchema, foreignTable)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getCrossReference(String, String, String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getCrossReference(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `parentCatalog` (String): A parent catalog name as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used in the selection criteria.
- `parentSchema` (String): A parent schema name as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used in the selection criteria.
- `parentTable` (String): The name of the parent table that exports the key. It must match the table name as it is stored in the database.
- `foreignCatalog` (String): A foreign catalog name as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used in the selection criteria.
- `foreignSchema` (String): A foreign schema name as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used in the selection criteria.
- `foreignTable` (String): The name of the foreign table that exports the key. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — An result set containing the foreign key column descriptions from the specified foreign key table that reference the primary key or the columns representing a unique constraint of the parent table. One column description is provided in each row of the result set, and they are ordered by `FKTABLE_CAT`, `FKTABLE_SCHEM`, `FKTABLE_NAME`, and `KEY_SEQ`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDatabaseMajorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getDatabaseMajorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDatabaseMajorVersion()).

**Returns:** `Integer` — The major version number of the underlying database.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDatabaseMinorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getDatabaseMinorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDatabaseMinorVersion()).

**Returns:** `Integer` — The minor version number of the underlying database.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDatabaseProductName()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getDatabaseProductName()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDatabaseProductName()).

**Returns:** `String` — The name of this database product.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDatabaseProductVersion()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getDatabaseProductVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDatabaseProductVersion()).

**Returns:** `String` — The version number of this database product.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDefaultTransactionIsolation()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getDefaultTransactionIsolation()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDefaultTransactionIsolation()).

**Returns:** `Integer` — The database's default transaction isolation level, which is one of: `Jdbc.Connection.TRANSACTION_READ_UNCOMMITTED`, `Jdbc.Connection.TRANSACTION_READ_COMMITTED`, `Jdbc.Connection.TRANSACTION_REPEATABLE_READ`, `Jdbc.Connection.TRANSACTION_SERIALIZABLE`, or `Jdbc.Connection.TRANSACTION_NONE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDriverMajorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getDriverMajorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDriverMajorVersion()).

**Returns:** `Integer` — The JDBC driver's major version number.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDriverMinorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getDriverMinorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDriverMinorVersion()).

**Returns:** `Integer` — The JDBC driver's minor version number.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDriverName()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getDriverName()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDriverName()).

**Returns:** `String` — The name of this JDBC driver.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDriverVersion()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getDriverVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getDriverVersion()).

**Returns:** `String` — The version number of this JDBC driver.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getExportedKeys(catalog, schema, table)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getImportedKeys(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getExportedKeys(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — An result set containing the foreign key column descriptions for the primary key columns exported by the table. One column description is provided in each row of the result set, and they are ordered by `FKTABLE_CAT`, `FKTABLE_SCHEM`, `FKTABLE_NAME`, and `KEY_SEQ`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getExtraNameCharacters()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getExtraNameCharacters()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getExtraNameCharacters()).

**Returns:** `String` — The extra characters that are avaiable for use in unquoted identifier names in addition to a-z, A-Z, 0-9, and _.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFunctionColumns(catalog, schemaPattern, functionNamePattern, columnNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getFunctionColumns(String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getFunctionColumns(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `functionNamePattern` (String): The function pattern, which match the function name as it is stored in the database.
- `columnNamePattern` (String): The parameter name pattern, which must match the parameter or column name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the descriptions of system and user function parameters available in the given catalog. Each row contains one function description, ordered according to `FUNCTION_CAT`, `FUNCTION_SCHEM`, `FUNCTION_NAME`, and `SPECIFIC_ NAME`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFunctions(catalog, schemaPattern, functionNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getFunctions(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getFunctions(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `functionNamePattern` (String): The function pattern, which must match the function name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing descriptions of the system and user functions available in the given catalog. Each row contains one function description, ordered according to `FUNCTION_CAT`, `FUNCTION_SCHEM`, `FUNCTION_NAME`, and `SPECIFIC_ NAME`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getIdentifierQuoteString()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getIdentifierQuoteString()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getIdentifierQuoteString()).

**Returns:** `String` — The string used to quote SQL identifiers. Defaults to a space (" ") if identifier quoting isn't supported.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getImportedKeys(catalog, schema, table)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getImportedKeys(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getImportedKeys(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — An result set containing the column descriptions for the primary key columns referenced by the given table's foreign key columns (those imported by a table). One column description is provided in each row of the result set, and they are ordered by `PKTABLE_CAT`, `PKTABLE_SCHEM`, `PKTABLE_NAME`, and `KEY_SEQ`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getIndexInfo(catalog, schema, table, unique, approximate)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getIndexInfo(String, String, String, boolean, boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getIndexInfo(java.lang.String,%20java.lang.String,%20java.lang.String,%20boolean,%20boolean)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.
- `unique` (Boolean): If `true`, the method only return indices for unique values; otherwise it returns indices whether the values are unique or not.
- `approximate` (Boolean): If `true`, the result is allowed to reflect approximate or out-of-data values; otherwise result accuracy is requested.

**Returns:** `JdbcResultSet` — An result set containing the index and statistic column descriptions for the specified table. One column description is provided in each row of the result set, and they are ordered by `NON_UNIQUE`, `TYPE`, `INDEX_NAME`, and `ORDINAL_POSITION`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getJDBCMajorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getJDBCMajorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getJDBCMajorVersion()).

**Returns:** `Integer` — The major JDBC version number for this driver.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getJDBCMinorVersion()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getJDBCMinorVersion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getJDBCMinorVersion()).

**Returns:** `Integer` — The minor JDBC version number for this driver.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxBinaryLiteralLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxBinaryLiteralLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxBinaryLiteralLength()).

**Returns:** `Integer` — The maximum number of hex characters this database allows in an inline binary literal. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxCatalogNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxCatalogNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxCatalogNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a catalog name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxCharLiteralLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxCharLiteralLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxCharLiteralLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a character literal. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a column name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnsInGroupBy()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnsInGroupBy()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnsInGroupBy()).

**Returns:** `Integer` — The maximum number of columns this database allows in a `GROUP BY` clause. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnsInIndex()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnsInIndex()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnsInIndex()).

**Returns:** `Integer` — The maximum number of columns this database allows in an index. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnsInOrderBy()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnsInOrderBy()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnsInOrderBy()).

**Returns:** `Integer` — The maximum number of columns this database allows in an `ORDER BY` clause. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnsInSelect()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnsInSelect()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnsInSelect()).

**Returns:** `Integer` — The maximum number of columns this database allows in an `SELECT` list. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxColumnsInTable()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxColumnsInTable()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxColumnsInTable()).

**Returns:** `Integer` — The maximum number of columns this database allows in a table. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxConnections()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxConnections()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxConnections()).

**Returns:** `Integer` — The maximum number of concurrent connections to this database. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxCursorNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxCursorNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxCursorNameLength()).

**Returns:** `Integer` — The maximum number of characters that this database allows in a cursor name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxIndexLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxIndexLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxIndexLength()).

**Returns:** `Integer` — The maximum number of bytes this database allows for an index, including all its parts. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxProcedureNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxProcedureNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxProcedureNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a procedure name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxRowSize()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxRowSize()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxRowSize()).

**Returns:** `Integer` — The maximum number of bytes this database allows in a single row. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxSchemaNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxSchemaNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxSchemaNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a schema name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxStatementLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxStatementLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxStatementLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in an SQL statement. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxStatements()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxStatements()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxStatements()).

**Returns:** `Integer` — The maximum number of active statements to this database that can be open simultaneously. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxTableNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxTableNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxTableNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a table name. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxTablesInSelect()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxTablesInSelect()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxTablesInSelect()).

**Returns:** `Integer` — The maximum number of tables this database allows in a `SELECT` statement. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMaxUserNameLength()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getMaxUserNameLength()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getMaxUserNameLength()).

**Returns:** `Integer` — The maximum number of characters this database allows in a username. A response of 0 indicates there is no known limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getNumericFunctions()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getNumericFunctions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getNumericFunctions()).

**Returns:** `String` — The comma-separated list of math functions available with this database. These are the Open/Open CLI math function names used in the JDBC function escape clause.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getPrimaryKeys(catalog, schema, table)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getPrimaryKeys(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getPrimaryKeys(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — An result set containing the column descriptions for the primary key columns, one per row, ordered by `COLUMN_NAME`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getProcedureColumns(catalog, schemaPattern, procedureNamePattern, columnNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getProcedureColumns(String, String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getProcedureColumns(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `procedureNamePattern` (String): The procedure name pattern to filter the search by. It must match the procedure name as it is stored in the database.
- `columnNamePattern` (String): The column name pattern to filter the search by. It must match the column name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the procedure and column descriptions, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getProcedureTerm()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getProcedureTerm()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getProcedureTerm()).

**Returns:** `String` — The database vendor's preferred term for 'procedure'.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getProcedures(catalog, schemaPattern, procedureNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getProcedures(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getProcedures(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `procedureNamePattern` (String): The procedure name pattern to filter the search by. It must match the procedure name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the procedure descriptions, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getResultSetHoldability()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getResultSetHoldability()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getResultSetHoldability()).

**Returns:** `Integer` — The database default holdability; one of `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRowIdLifetime()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getRowIdLifetime()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getRowIdLifetime()).

**Returns:** `Integer` — The status indicatig the lifetime of a `ROWID`, which is one of `Jdbc.RowIdLifetime.ROWID_UNSUPPORTED`, `Jdbc.RowIdLifetime.ROWID_VALID_OTHER`, `Jdbc.RowIdLifetime.ROWID_VALID_SESSION`, `Jdbc.RowIdLifetime.ROWID_VALID_TRANSACTION`, or `Jdbc.RowIdLifetime.ROWID_VALID_FOREVER`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSQLKeywords()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getSQLKeywords()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSQLKeywords()).

**Returns:** `String` — The comma-separated list of all this database's SQL keywords that aren't also SQL:2003 keywords.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSQLStateType()

Returns: `Integer`

For documentation of this method, see `java.sql.DatabaseMetaData#getSQLStateType()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSQLStateType()).

**Returns:** `Integer` — The type of `SQLSTATE`, which is either `sqlStateXOpen` or `sqlStateSQL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSchemaTerm()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getSchemaTerm()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSchemaTerm()).

**Returns:** `String` — The database vendor's preferred term for 'schema'.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSchemas()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getSchemas()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSchemas()).

**Returns:** `JdbcResultSet` — A result set containing the schema descriptions, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSchemas(catalog, schemaPattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getSchemas()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSchemas()).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.

**Returns:** `JdbcResultSet` — A result set containing scheme descriptions available in this database, ordered by `TABLE_CATALOG` and `TABLE_SCHEM`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSearchStringEscape()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getSearchStringEscape()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSearchStringEscape()).

**Returns:** `String` — The string that is used to escape wildcard characters such as '_' or '%'.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getStringFunctions()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getStringFunctions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getStringFunctions()).

**Returns:** `String` — The comma-separated list of string functions available with this database. These are the Open Group CLI string function names used in the JDBC function escape clause.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSuperTables(catalog, schemaPattern, tableNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getSuperTables(String, String,String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSuperTables(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used in the selection criteria.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema.
- `tableNamePattern` (String): The table name pattern; may be a fully qualified name.

**Returns:** `JdbcResultSet` — A result set containing descriptions of the table hierarchies defined in a particular schema in this database. Each row provides information about a specific table type. Tables without supers aren't listed.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSuperTypes(catalog, schemaPattern, typeNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getSuperTypes(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSuperTypes(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used in the selection criteria.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema.
- `typeNamePattern` (String): The user-defined type name pattern; may be a fully qualified name.

**Returns:** `JdbcResultSet` — A result set containing descriptions of the user-defined type hierarchies defined in a particular schema in this database. Each row provides information about a specific user-defined type. Types without supers aren't listed.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSystemFunctions()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getSystemFunctions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getSystemFunctions()).

**Returns:** `String` — The comma-separated list of system functions available with this database. These are the Open Group CLI system function names used in the JDBC function escape clause.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTablePrivileges(catalog, schemaPattern, tableNamePattern)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getTablePrivileges(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getTablePrivileges(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `tableNamePattern` (String): The table name pattern to filter the search by. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — A result set containing the table privilege descriptions, one per row, ordered by `TABLE_CAT`, `TABLE_SCHEM`, `TABLE_NAME`, and `PRIVILEGE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTableTypes()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getTableTypes()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getTableTypes()).

**Returns:** `JdbcResultSet` — A result set containing the table types, one per row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTables(catalog, schemaPattern, tableNamePattern, types)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getTables(String, String, String, String[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getTables(java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String[])).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `tableNamePattern` (String): The table name pattern to filter the search by. It must match the table name as it is stored in the database.
- `types` (String[]): A list of table types to return, each of which must be on the list that `getTableTypes()` returns. Passing `null` indictates that all table types are returned.

**Returns:** `JdbcResultSet` — A result set containing the table descriptions, one per row, ordered according to `TABLE_TYPE`, `TABLE_CAT`, `TABLE_SCHEM`, and `TABLE_NAME`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTimeDateFunctions()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getTimeDateFunctions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getTimeDateFunctions()).

**Returns:** `String` — The comma-separated list of time and date functions available with this database.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTypeInfo()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getTypeInfo()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getTypeInfo()).

**Returns:** `JdbcResultSet` — An result set containing the descriptions of data types supported by this database. One SQL type description is provided in each row of the result set, and they are ordered by `DATA_TYPE` and then by how closely the data type maps to the corresponding JDBC SQL type.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getUDTs(catalog, schemaPattern, typeNamePattern, types)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getUDTs(String, String, String, int[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getUDTs(java.lang.String,%20java.lang.String,%20java.lang.String,%20int[])).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schemaPattern` (String): The schema name pattern to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `typeNamePattern` (String): The type name pattern to filter the search by; may be a fully qualified name.
- `types` (Integer[]): A list of user-defined types (`JAVA_OBJECT`, `STRUCT`, or `DISTINCT`) to include. Passing `null` indictates that all types are returned.

**Returns:** `JdbcResultSet` — A result set containing the user-defined type (UDT) descriptions, one per row, ordered according to `DATA_TYPE`, `TYPE_CAT`, `TYPE_SCHEM`, and `TYPE_NAME`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getURL()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getURL()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getURL()).

**Returns:** `String` — The URL for this database management system, or `null` if isn't generated.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getUserName()

Returns: `String`

For documentation of this method, see `java.sql.DatabaseMetaData#getUserName()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getUserName()).

**Returns:** `String` — The username as known to this database.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getVersionColumns(catalog, schema, table)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.DatabaseMetaData#getVersionColumns(String, String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#getVersionColumns(java.lang.String,%20java.lang.String,%20java.lang.String)).

**Parameters:**
- `catalog` (String): The catalog name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a catalog. Passing `null` incidates the catalog name isn't used to narrow the search.
- `schema` (String): The schema name to filter the search by, as it appears in the database. Passing an empty string retrieves those procedures without a schema. Passing `null` incidates the schema name isn't used to narrow the search.
- `table` (String): The table name. It must match the table name as it is stored in the database.

**Returns:** `JdbcResultSet` — An unordered result set containing the column descriptions that are updated when any value in a row is updated (one column description per row in the result set).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### insertsAreDetected(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#insertsAreDetected(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#insertsAreDetected(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the specified result set type a visible row insert is detected by calls to `JdbcResultSet.rowInserted()`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isCatalogAtStart()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#isCatalogAtStart()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#isCatalogAtStart()).

**Returns:** `Boolean` — `true` if a catalog appears at the start of a fully-qualified table name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isReadOnly()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#isReadOnly()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#isReadOnly()).

**Returns:** `Boolean` — `true` if the database is read-only; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### locatorsUpdateCopy()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#locatorsUpdateCopy()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#locatorsUpdateCopy()).

**Returns:** `Boolean` — `true` if updates made to a Large Object (LOB) are made to a copy of th LOB; `false` if updates are made directly to the LOB.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nullPlusNonNullIsNull()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#nullPlusNonNullIsNull()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#nullPlusNonNullIsNull()).

**Returns:** `Boolean` — `true` if concatenations of `NULL` and non-`NULL` values result in a `NULL`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nullsAreSortedAtEnd()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#nullsAreSortedAtEnd()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#nullsAreSortedAtEnd()).

**Returns:** `Boolean` — `true` if `NULL` values are sorted to the end regardless of sort order (ascending or descending). Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nullsAreSortedAtStart()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#nullsAreSortedAtStart()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#nullsAreSortedAtStart()).

**Returns:** `Boolean` — `true` if `NULL` values are sorted to the start regardless of sort order (ascending or descending). Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nullsAreSortedHigh()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#nullsAreSortedHigh()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#nullsAreSortedHigh()).

**Returns:** `Boolean` — `true` if the `NULL` values are sorted high, meaning they are considered to have a value higher than others in the domain when sorting. Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nullsAreSortedLow()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#nullsAreSortedLow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#nullsAreSortedLow()).

**Returns:** `Boolean` — `true` if the `NULL` values are sorted low, meaning they are considered to have a value lower than others in the domain when sorting. Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### othersDeletesAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#othersDeletesAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#othersDeletesAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the deletes made by others are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### othersInsertsAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#othersInsertsAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#othersInsertsAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the inserts made by others are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### othersUpdatesAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#othersUpdatesAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#othersUpdatesAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the updates made by others are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### ownDeletesAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#ownDeletesAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#ownDeletesAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the set's own deletes are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### ownInsertsAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#ownInsertsAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#ownInsertsAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the set's own inserts are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### ownUpdatesAreVisible(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#ownUpdatesAreVisible(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#ownUpdatesAreVisible(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the given result set type the set's own updates are visible; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesLowerCaseIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesLowerCaseIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesLowerCaseIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case unquoted SQL identifiers as case-insensitive and stores them in lowercase; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesLowerCaseQuotedIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesLowerCaseQuotedIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesLowerCaseQuotedIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case quoted SQL identifiers as case-insensitive and stores them in lowercase; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesMixedCaseIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesMixedCaseIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesMixedCaseIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case unquoted SQL identifiers as case-insensitive and stores them in mixed case; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesMixedCaseQuotedIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesMixedCaseQuotedIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesMixedCaseQuotedIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case quoted SQL identifiers as case-insensitive and stores them in mixed case; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesUpperCaseIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesUpperCaseIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesUpperCaseIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case unquoted SQL identifiers as case-insensitive and stores them in uppercase; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### storesUpperCaseQuotedIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#storesUpperCaseQuotedIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#storesUpperCaseQuotedIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case quoted SQL identifiers as case-insensitive and stores them in uppercase; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsANSI92EntryLevelSQL()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsANSI92EntryLevelSQL()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsANSI92EntryLevelSQL()).

**Returns:** `Boolean` — `true` if this database supports the ANSI92 entry level SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsANSI92FullSQL()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsANSI92FullSQL()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsANSI92FullSQL()).

**Returns:** `Boolean` — `true` if this database supports the ANSI92 full level SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsANSI92IntermediateSQL()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsANSI92IntermediateSQL()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsANSI92IntermediateSQL()).

**Returns:** `Boolean` — `true` if this database supports the ANSI92 intermediate level SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsAlterTableWithAddColumn()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsAlterTableWithAddColumn()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsAlterTableWithAddColumn()).

**Returns:** `Boolean` — `true` if the database supports `ALTER TABLE` with add column; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsAlterTableWithDropColumn()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsAlterTableWithDropColumn()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsAlterTableWithDropColumn()).

**Returns:** `Boolean` — `true` if the database supports `ALTER TABLE` with drop column; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsBatchUpdates()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsBatchUpdates()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsBatchUpdates()).

**Returns:** `Boolean` — `true` if the database supports batch updates; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCatalogsInDataManipulation()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCatalogsInDataManipulation()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCatalogsInDataManipulation()).

**Returns:** `Boolean` — `true` if a data manipulation statement can include a catalog name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCatalogsInIndexDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCatalogsInIndexDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCatalogsInIndexDefinitions()).

**Returns:** `Boolean` — `true` if an index definition statement can include a catalog name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCatalogsInPrivilegeDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCatalogsInPrivilegeDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCatalogsInPrivilegeDefinitions()).

**Returns:** `Boolean` — `true` if a privilege definition statement can include a catalog name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCatalogsInProcedureCalls()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCatalogsInProcedureCalls()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCatalogsInProcedureCalls()).

**Returns:** `Boolean` — `true` if a procedure call statement can include a catalog name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCatalogsInTableDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCatalogsInTableDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCatalogsInTableDefinitions()).

**Returns:** `Boolean` — `true` if a table definition statement can include a catalog name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsColumnAliasing()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsColumnAliasing()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsColumnAliasing()).

**Returns:** `Boolean` — `true` if the database supports column aliasing; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsConvert()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsConvert()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsConvert()).

**Returns:** `Boolean` — `true` if this database supports the JDBC scalar function `CONVERT` for the conversion of one JDBC type (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html) to another; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsConvert(fromType, toType)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsConvert(int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsConvert(int,%20int)).

**Parameters:**
- `fromType` (Integer): The type (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html) to convert from.
- `toType` (Integer): The type (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html) to convert to.

**Returns:** `Boolean` — `true` if this database supports the JDBC scalar function `CONVERT` for the conversion of the specified JDBC types; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCoreSQLGrammar()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCoreSQLGrammar()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCoreSQLGrammar()).

**Returns:** `Boolean` — `true` if this database supports the ODBC Core SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsCorrelatedSubqueries()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsCorrelatedSubqueries()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsCorrelatedSubqueries()).

**Returns:** `Boolean` — `true` if this database supports correlated subqueries; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsDataDefinitionAndDataManipulationTransactions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsDataDefinitionAndDataManipulationTransactions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsDataDefinitionAndDataManipulationTransactions()).

**Returns:** `Boolean` — `true` if this database supports both data definition and data manipulation statements within a transaction; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsDataManipulationTransactionsOnly()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsDataManipulationTransactionsOnly()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsDataManipulationTransactionsOnly()).

**Returns:** `Boolean` — `true` if this database supports data manipulation statements within a transaction; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsDifferentTableCorrelationNames()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsDifferentTableCorrelationNames()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsDifferentTableCorrelationNames()).

**Returns:** `Boolean` — `true` if table correlation names are supported and are restricted to be different frm the names of the tables in the database; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsExpressionsInOrderBy()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsExpressionsInOrderBy()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsExpressionsInOrderBy()).

**Returns:** `Boolean` — `true` if this database supports expressions in `ORDER BY` lists; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsExtendedSQLGrammar()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsExtendedSQLGrammar()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsExtendedSQLGrammar()).

**Returns:** `Boolean` — `true` if this database supports the ODBC Extended SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsFullOuterJoins()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsFullOuterJoins()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsFullOuterJoins()).

**Returns:** `Boolean` — `true` if this database supports full nested outer joins; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsGetGeneratedKeys()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsGetGeneratedKeys()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsGetGeneratedKeys()).

**Returns:** `Boolean` — `true` if auto-generated keys can be retrieved after a statement is executed; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsGroupBy()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsGroupBy()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsGroupBy()).

**Returns:** `Boolean` — `true` if this database supports some form of `GROUP BY` clause; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsGroupByBeyondSelect()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsGroupByBeyondSelect()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsGroupByBeyondSelect()).

**Returns:** `Boolean` — `true` if this database supports using columns that aren't in the `SELECT` statement in a `GROUP BY` clause, provided that all the columns in the `SELECT` statement are included in the `GROUP BY` clause. Returns `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsGroupByUnrelated()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsGroupByUnrelated()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsGroupByUnrelated()).

**Returns:** `Boolean` — `true` if this database supports using a column that isn't in the `SELECT` statement in a `GROUP BY` clause; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsIntegrityEnhancementFacility()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsIntegrityEnhancementFacility()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsIntegrityEnhancementFacility()).

**Returns:** `Boolean` — `true` if this database supports the SQL Integrity Enhancement Facility; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsLikeEscapeClause()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsLikeEscapeClause()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsLikeEscapeClause()).

**Returns:** `Boolean` — `true` if this database supports specifying a `LIKE` escape clause; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsLimitedOuterJoins()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsLimitedOuterJoins()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsLimitedOuterJoins()).

**Returns:** `Boolean` — `true` if this database provides limited support for outer joins; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMinimumSQLGrammar()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMinimumSQLGrammar()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMinimumSQLGrammar()).

**Returns:** `Boolean` — `true` if this database supports the ODBC Minimum SQL grammar; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMixedCaseIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMixedCaseIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMixedCaseIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case unquoted SQL identifiers as case-sensitive and as a result stores them in mixed case; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMixedCaseQuotedIdentifiers()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMixedCaseQuotedIdentifiers()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMixedCaseQuotedIdentifiers()).

**Returns:** `Boolean` — `true` if the database treats mixed case quoted SQL identifiers as case-sensitive and as a result stores them in mixed case; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMultipleOpenResults()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMultipleOpenResults()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMultipleOpenResults()).

**Returns:** `Boolean` — `true` if a callable statement can return multiple result sets simultenously; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMultipleResultSets()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMultipleResultSets()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMultipleResultSets()).

**Returns:** `Boolean` — `true` if this database supports getting multiple result sets from a single execution call; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsMultipleTransactions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsMultipleTransactions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsMultipleTransactions()).

**Returns:** `Boolean` — `true` if this database supports having multiple transactions on different connections open at once; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsNamedParameters()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsNamedParameters()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsNamedParameters()).

**Returns:** `Boolean` — `true` if the database supports named parameters to callable statements; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsNonNullableColumns()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsNonNullableColumns()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsNonNullableColumns()).

**Returns:** `Boolean` — `true` if columns in this database may be defined as non-nullable; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOpenCursorsAcrossCommit()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOpenCursorsAcrossCommit()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOpenCursorsAcrossCommit()).

**Returns:** `Boolean` — `true` if this database supports keeping cursors always open across commits; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOpenCursorsAcrossRollback()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOpenCursorsAcrossRollback()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOpenCursorsAcrossRollback()).

**Returns:** `Boolean` — `true` if this database supports keeping cursors always open across rollbacks; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOpenStatementsAcrossCommit()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOpenStatementsAcrossCommit()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOpenStatementsAcrossCommit()).

**Returns:** `Boolean` — `true` if this database supports keeping statements always open across commits; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOpenStatementsAcrossRollback()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOpenStatementsAcrossRollback()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOpenStatementsAcrossRollback()).

**Returns:** `Boolean` — `true` if this database supports keeping statements always open across rollbacks; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOrderByUnrelated()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOrderByUnrelated()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOrderByUnrelated()).

**Returns:** `Boolean` — `true` if this database supports using a column that isn't in the `SELECT` statement in an `ORDER BY` clause; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsOuterJoins()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsOuterJoins()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsOuterJoins()).

**Returns:** `Boolean` — `true` if this database supports some form of outer join; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsPositionedDelete()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsPositionedDelete()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsPositionedDelete()).

**Returns:** `Boolean` — `true` if this database supports positioned `DELETE` statements; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsPositionedUpdate()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsPositionedUpdate()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsPositionedUpdate()).

**Returns:** `Boolean` — `true` if this database supports positioned `UPDATE` statements; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsResultSetConcurrency(type, concurrency)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsResultSetConcurrency(int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsResultSetConcurrency(int,%20int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.
- `concurrency` (Integer): The concurrency type, which is either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.

**Returns:** `Boolean` — `true` if this database supports the specified result set and concurrency type combination; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsResultSetHoldability(holdability)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsResultSetHoldability(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsResultSetHoldability(int)).

**Parameters:**
- `holdability` (Integer): A holdability constant to check; one of `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Returns:** `Boolean` — `true` if the database the specified holdability; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsResultSetType(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsResultSetType(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsResultSetType(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if this database supports the specified result set type; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSavepoints()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSavepoints()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSavepoints()).

**Returns:** `Boolean` — `true` if the database supports savepoints; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSchemasInDataManipulation()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSchemasInDataManipulation()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSchemasInDataManipulation()).

**Returns:** `Boolean` — `true` if a data manipulation statement can include a schema name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSchemasInIndexDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSchemasInIndexDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSchemasInIndexDefinitions()).

**Returns:** `Boolean` — `true` if an index definition statement can include a schema name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSchemasInPrivilegeDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSchemasInPrivilegeDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSchemasInPrivilegeDefinitions()).

**Returns:** `Boolean` — `true` if an privilege definition statement can include a schema name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSchemasInProcedureCalls()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSchemasInProcedureCalls()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSchemasInProcedureCalls()).

**Returns:** `Boolean` — `true` if a procedure call statement can include a schema name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSchemasInTableDefinitions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSchemasInTableDefinitions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSchemasInTableDefinitions()).

**Returns:** `Boolean` — `true` if a table definition statement can include a schema name; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSelectForUpdate()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSelectForUpdate()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSelectForUpdate()).

**Returns:** `Boolean` — `true` if this database supports `SELECT FOR UPDATE` statements; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsStatementPooling()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsStatementPooling()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsStatementPooling()).

**Returns:** `Boolean` — `true` if the database supports statement pooling; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsStoredFunctionsUsingCallSyntax()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsStoredFunctionsUsingCallSyntax()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsStoredFunctionsUsingCallSyntax()).

**Returns:** `Boolean` — `true` if the database supports invoking user-defined or vendor functions using the stored procedure escape syntax; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsStoredProcedures()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsStoredProcedures()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsStoredProcedures()).

**Returns:** `Boolean` — `true` if this database supports stored procedure calls that used the stored procedure escape syntax; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSubqueriesInComparisons()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSubqueriesInComparisons()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSubqueriesInComparisons()).

**Returns:** `Boolean` — `true` if this database supports subqueries in comparison expressions; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSubqueriesInExists()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSubqueriesInExists()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSubqueriesInExists()).

**Returns:** `Boolean` — `true` if this database supports subqueries in `EXISTS` expressions; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSubqueriesInIns()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSubqueriesInIns()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSubqueriesInIns()).

**Returns:** `Boolean` — `true` if this database supports subqueries in `IN` expressions; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsSubqueriesInQuantifieds()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsSubqueriesInQuantifieds()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsSubqueriesInQuantifieds()).

**Returns:** `Boolean` — `true` if this database supports subqueries in quantified expressions; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsTableCorrelationNames()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsTableCorrelationNames()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsTableCorrelationNames()).

**Returns:** `Boolean` — `true` if this database supports table corelation names; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsTransactionIsolationLevel(level)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsTransactionIsolationLevel(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsTransactionIsolationLevel(int)).

**Parameters:**
- `level` (Integer): The transaction isolation level to determine the support of. This must be one of `Jdbc.Connection.TRANSACTION_READ_UNCOMMITTED`, `Jdbc.Connection.TRANSACTION_READ_COMMITTED`, `Jdbc.Connection.TRANSACTION_REPEATABLE_READ`, `Jdbc.Connection.TRANSACTION_SERIALIZABLE`, or `Jdbc.Connection.TRANSACTION_NONE`.

**Returns:** `Boolean` — `true` if this database supports the given transaction isolation level; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsTransactions()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsTransactions()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsTransactions()).

**Returns:** `Boolean` — `true` if this database supports transactions; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsUnion()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsUnion()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsUnion()).

**Returns:** `Boolean` — `true` if this database supports SQL `UNION`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### supportsUnionAll()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#supportsUnionAll()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#supportsUnionAll()).

**Returns:** `Boolean` — `true` if this database supports SQL `UNION ALL`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updatesAreDetected(type)

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#updatesAreDetected(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#updatesAreDetected(int)).

**Parameters:**
- `type` (Integer): The result set type, which is `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Returns:** `Boolean` — `true` if for the specified result set type a visible row update is detected by calls to `JdbcResultSet.rowUpdated()`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### usesLocalFilePerTable()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#usesLocalFilePerTable()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#usesLocalFilePerTable()).

**Returns:** `Boolean` — `true` if the database stores each table in a separate local file; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### usesLocalFiles()

Returns: `Boolean`

For documentation of this method, see `java.sql.DatabaseMetaData#usesLocalFiles()` (https://docs.oracle.com/javase/6/docs/api/java/sql/DatabaseMetaData.html#usesLocalFiles()).

**Returns:** `Boolean` — `true` if the database stores tables in a local file; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

## Properties

None.
