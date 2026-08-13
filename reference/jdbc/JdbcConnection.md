# JdbcConnection

A JDBC `Connection`. For documentation of this class, see `java.sql.Connection` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html).

## Methods

### clearWarnings()

Returns: `void`

For documentation of this method, see `java.sql.Connection#clearWarnings()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#clearWarnings()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### close()

Returns: `void`

Release this connection's database and all associated resources.

```javascript
const conn = Jdbc.getConnection(
    'jdbc:mysql://<host>:<port>/<instance>',
    'user',
    'password',
);
conn.close();
```

---

### commit()

Returns: `void`

Makes all pending changes permanent, releases database locks held by this `JdbcConnection`.

```javascript
const conn = Jdbc.getConnection(
    'jdbc:mysql://<host>:<port>/<instance>',
    'user',
    'password',
);
conn.setAutoCommit(false);
const stmt = conn.prepareStatement(
    'insert into person (lname,fname) values (?,?)',
);
const start = new Date();
for (let i = 0; i < 5000; i++) {
  // Objects are accessed using 1-based indexing
  stmt.setObject(1, `firstName${i}`);
  stmt.setObject(2, `lastName${i}`);
  stmt.addBatch();
}
const res = stmt.executeBatch();
conn.commit();  // When this returns, this is when changes are actually
                // committed
conn.close();
```

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### createArrayOf(typeName, elements)

Returns: `JdbcArray`

For documentation of this method, see `java.sql.Connection#createArrayOf(String, Object[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createArrayOf(java.lang.String,%20java.lang.Object[])).

**Parameters:**
- `typeName` (String): The database-specific SQL name of the array elemnents' type. Options include built-in types, user-defined types, or standard SQL types supported by the database.
- `elements` (Object[]): The elements to populate in the returned object.

**Returns:** `JdbcArray` — An array whose elements map to the specified SQL type.

---

### createBlob()

Returns: `JdbcBlob`

Constructs a `JdbcBlob` instance. See also `java.sql.Connection#createBlob()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createBlob()).

The object returned initially contains no data. You can use the `setBytes` methods of `JdbcBlob` to set the data it should contain. The blob used here is not the same as the blob created with `Utilities.newBlob(data)`. To convert between the two formats, use the defined `getBytes()` and `setBytes()` methods. Alternatively, both `JdbcBlob` and `JdbcClob` provide a `getAppsScriptBlob()` convenience method for converting to a format that can be used by Apps Script.

**Returns:** `JdbcBlob` — An empty blob object.

---

### createClob()

Returns: `JdbcClob`

For documentation of this method, see `java.sql.Connection#createClob()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createClob()).

**Returns:** `JdbcClob` — An empty clob object.

---

### createNClob()

Returns: `JdbcClob`

For documentation of this method, see `java.sql.Connection#createNClob()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createNClob()).

**Returns:** `JdbcClob` — An empty nclob object.

---

### createSQLXML()

Returns: `JdbcSQLXML`

For documentation of this method, see `java.sql.Connection#createSQLXML()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createSQLXML()).

**Returns:** `JdbcSQLXML` — An empty SQLXML object.

---

### createStatement()

Returns: `JdbcStatement`

Creates a `JdbcStatement` object for sending SQL statements to the database. See also `java.sql.Connection#createStatement()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStatement()).

```javascript
// This sample code assumes authentication is off
const conn = Jdbc.getConnection('jdbc:mysql://<host>:3306/<instance>');
const stmt = conn.createStatement();

stmt.setMaxRows(100);
const rs = stmt.execute('select * from person');

while (rs.next()) {
  // Do something
}

rs.close();
stmt.close();
conn.close();
```

**Returns:** `JdbcStatement` — A statement instance to execute queries with.

---

### createStatement(resultSetType, resultSetConcurrency)

Returns: `JdbcStatement`

Creates a `JdbcStatement` object for sending SQL statements to the database. See also `java.sql.Connection#createStatement(int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStatement(int,%20int)).

This version allows the result set type and concurrency to be overridden.

```javascript
// This sample code assumes authentication is off
// For more information about this method, see documentation here:
//  http://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStatement(int,
//  int)
const conn = Jdbc.getConnection('jdbc:mysql://<host>:3306/<instance>');
const stmt = conn.createStatement(
    Jdbc.ResultSet.TYPE_FORWARD_ONLY,
    Jdbc.ResultSet.CONCUR_READ_ONLY,
);

stmt.setMaxRows(100);
const rs = stmt.execute('select * from person');

while (rs.next()) {
  // Do something
}

rs.close();
stmt.close();
conn.close();
```

**Parameters:**
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.

**Returns:** `JdbcStatement` — A statement instance to execute queries with.

---

### createStatement(resultSetType, resultSetConcurrency, resultSetHoldability)

Returns: `JdbcStatement`

Creates a `JdbcStatement` object for sending SQL statements to the database. See also `java.sql.Connection#createStatement(int, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStatement(int,%20int,%20int)).

This version allows the result set type, concurrency and holdability to be overridden.

```javascript
// This sample code assumes authentication is off
// For more information about this method, see documentation here:
//  http://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStatement(int,
//  int)
const conn = Jdbc.getConnection('jdbc:mysql://<host>:3306/<instance>');
const stmt = conn.createStatement(
    Jdbc.ResultSet.TYPE_FORWARD_ONLY,
    Jdbc.ResultSet.CONCUR_READ_ONLY,
    Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT,
);

stmt.setMaxRows(100);
const rs = stmt.execute('select * from person');

while (rs.next()) {
  // Do something
}

rs.close();
stmt.close();
conn.close();
```

**Parameters:**
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.
- `resultSetHoldability` (Integer): A holdability setting; either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Returns:** `JdbcStatement` — A statement instance to execute queries with.

---

### createStruct(typeName, attributes)

Returns: `JdbcStruct`

For documentation of this method, see `java.sql.Connection#createStruct(String, Object[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#createStruct(java.lang.String,%20java.lang.Object[])).

**Parameters:**
- `typeName` (String): The database-specific SQL name of the array elemnents' type. Options include built-in types, user-defined types, or standard SQL types supported by the database.
- `attributes` (Object[]): The attributes that populate the returned object.

**Returns:** `JdbcStruct` — A structure object that maps to the given SQL type and is populated with the given attributes.

---

### getAutoCommit()

Returns: `Boolean`

For documentation of this method, see `java.sql.Connection#getAutoCommit()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getAutoCommit()).

**Returns:** `Boolean` — `true` if the connection's auto-commit mode is enabled; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCatalog()

Returns: `String`

or documentation of this method, see `java.sql.Connection#getCatalog()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getCatalog()).

**Returns:** `String` — The current catalog name or `null` if no name has been set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getHoldability()

Returns: `Integer`

For documentation of this method, see `java.sql.Connection#getHoldability()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getHoldability()).

**Returns:** `Integer` — The holdability setting of the connection; either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

---

### getMetaData()

Returns: `JdbcDatabaseMetaData`

For documentation of this method, see `java.sql.Connection#getMetaData()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getMetaData()).

**Returns:** `JdbcDatabaseMetaData` — The metadata of the database this connection connects to.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTransactionIsolation()

Returns: `Integer`

For documentation of this method, see `java.sql.Connection#getTransactionIsolation()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getTransactionIsolation()).

**Returns:** `Integer` — The current transaction level, which is one of: `Jdbc.Connection.TRANSACTION_READ_UNCOMMITTED`, `Jdbc.Connection.TRANSACTION_READ_COMMITTED`, `Jdbc.Connection.TRANSACTION_REPEATABLE_READ`, `Jdbc.Connection.TRANSACTION_SERIALIZABLE`, or `Jdbc.Connection.TRANSACTION_NONE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getWarnings()

Returns: `String[]`

For documentation of this method, see `java.sql.Connection#getWarnings()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#getWarnings()).

**Returns:** `String[]` — An array of warning strings.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isClosed()

Returns: `Boolean`

For documentation of this method, see `java.sql.Connection#isClosed()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#isClosed()).

**Returns:** `Boolean` — `true` if the connection is closed; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isReadOnly()

Returns: `Boolean`

For documentation of this method, see `java.sql.Connection#isReadOnly()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#isReadOnly()).

**Returns:** `Boolean` — `true` if the connection is read-only; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isValid(timeout)

Returns: `Boolean`

For documentation of this method, see `java.sql.Connection#isValid(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#isValid(int)).

**Parameters:**
- `timeout` (Integer): The time in seconds to wait for the validation operation to complete. A value of 0 indicates no timeout is applied.

**Returns:** `Boolean` — `true` if the connection is valid; `false` otherwise. Also returns `false` if the timeout period expires before the operation completes.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### nativeSQL(sql)

Returns: `String`

For documentation of this method, see `java.sql.Connection#nativeSQL(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#nativeSQL(java.lang.String)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' placeholders.

**Returns:** `String` — The native form of the provided statement.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### prepareCall(sql)

Returns: `JdbcCallableStatement`

For documentation of this method, see `java.sql.Connection#prepareCall(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareCall(java.lang.String)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' placeholders, typically provided using JDBC call escape syntax.

**Returns:** `JdbcCallableStatement` — A callable statement containing the pre-compiled SQL statement.

---

### prepareCall(sql, resultSetType, resultSetConcurrency)

Returns: `JdbcCallableStatement`

For documentation of this method, see `java.sql.Connection#prepareCall(String, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareCall(java.lang.String,%20int,%20int)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' placeholders, typically provided using JDBC call escape syntax.
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.

**Returns:** `JdbcCallableStatement` — A callable statement containing the pre-compiled SQL statement that produces result sets with the provided type and concurrency.

---

### prepareCall(sql, resultSetType, resultSetConcurrency, resultSetHoldability)

Returns: `JdbcCallableStatement`

For documentation of this method, see `java.sql.Connection#prepareCall(String, int, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareCall(java.lang.String,%20int,%20int,%20int)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' placeholders, typically provided using JDBC call escape syntax.
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.
- `resultSetHoldability` (Integer): A holdability setting; either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Returns:** `JdbcCallableStatement` — A callable statement containing the pre-compiled SQL statement that produces result sets with the provided type, concurrency.

---

### prepareStatement(sql)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement.

---

### prepareStatement(sql, autoGeneratedKeys)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String,%20int)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.
- `autoGeneratedKeys` (Integer): A flag that indicates whether auto-generated keys are returned; either `Jdbc.Statement.RETURN_GENERATED_KEYS` or `Jdbc.Statement.NO_GENERATED_KEYS`.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement, possibly capable of returning auto-generated keys.

---

### prepareStatement(sql, resultSetType, resultSetConcurrency)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String,%20int,%20int)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement that produces result sets with the provided type and concurrency.

---

### prepareStatement(sql, resultSetType, resultSetConcurrency, resultSetHoldability)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String, int, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String,%20int,%20int,%20int)).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.
- `resultSetType` (Integer): A result set type; one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_SENSITIVE`.
- `resultSetConcurrency` (Integer): A concurrency type; either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.
- `resultSetHoldability` (Integer): A holdability setting; either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement that produces result sets with the provided type, concurrency, and holdability.

---

### prepareStatementByIndex(sql, indices)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String, int[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String,%20int[])).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.
- `indices` (Integer[]): The column indices of columns that are returned from the inserted row or rows.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement, capable of returning auto-generated keys specified by the provided column indices.

---

### prepareStatementByName(sql, columnNames)

Returns: `JdbcPreparedStatement`

For documentation of this method, see `java.sql.Connection#prepareStatement(String, String[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#prepareStatement(java.lang.String,%20java.lang.String[])).

**Parameters:**
- `sql` (String): An SQL statement that may contain one more more '?' IN parameter placeholders.
- `columnNames` (String[]): The column names that specify which columns the method should return from the inserted row or rows.

**Returns:** `JdbcPreparedStatement` — A prepared statement containing the pre-compiled SQL statement, capable of returning auto-generated keys specified by the provided column names.

---

### releaseSavepoint(savepoint)

Returns: `void`

For documentation of this method, see `java.sql.Connection#releaseSavepoint(Savepoint)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#releaseSavepoint(java.sql.Savepoint)).

**Parameters:**
- `savepoint` (JdbcSavepoint): The save point to remove.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### rollback()

Returns: `void`

For documentation of this method, see `java.sql.Connection#rollback()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#rollback()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### rollback(savepoint)

Returns: `void`

For documentation of this method, see `java.sql.Connection#rollback(Savepoint)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#rollback(java.sql.Savepoint)).

**Parameters:**
- `savepoint` (JdbcSavepoint): The save point to rollback to.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setAutoCommit(autoCommit)

Returns: `void`

For documentation of this method, see `java.sql.Connection#setAutoCommit(boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setAutoCommit(boolean)).

**Parameters:**
- `autoCommit` (Boolean): If `true`, auto-commit mode is enabled; `false` disables.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setCatalog(catalog)

Returns: `void`

For documentation of this method, see `java.sql.Connection#setCatalog(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setCatalog(java.lang.String)).

**Parameters:**
- `catalog` (String): The name of a catalog (the subspace in the connection's database) in which to work.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setHoldability(holdability)

Returns: `void`

For documentation of this method, see `java.sql.Connection#setHoldability(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setHoldability(int)).

**Parameters:**
- `holdability` (Integer): The default holdability of `JdbcResultSet` objects created with this connection; either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

---

### setReadOnly(readOnly)

Returns: `void`

For documentation of this method, see `java.sql.Connection#setReadOnly(boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setReadOnly(boolean)).

**Parameters:**
- `readOnly` (Boolean): If `true`, read-only mode is enabled; `false` disables.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setSavepoint()

Returns: `JdbcSavepoint`

For documentation of this method, see `java.sql.Connection#setSavepoint()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setSavepoint()).

**Returns:** `JdbcSavepoint` — The new unnamed save point.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setSavepoint(name)

Returns: `JdbcSavepoint`

For documentation of this method, see `java.sql.Connection#setSavepoint(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setSavepoint(java.lang.String)).

**Parameters:**
- `name` (String): The name of the created save point.

**Returns:** `JdbcSavepoint` — The new named save point.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setTransactionIsolation(level)

Returns: `void`

For documentation of this method, see `java.sql.Connection#setTransactionIsolation(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Connection.html#setTransactionIsolation(int)).

**Parameters:**
- `level` (Integer): The transaction level to set, which is one of: `Jdbc.Connection.TRANSACTION_READ_UNCOMMITTED`, `Jdbc.Connection.TRANSACTION_READ_COMMITTED`, `Jdbc.Connection.TRANSACTION_REPEATABLE_READ`, `Jdbc.Connection.TRANSACTION_SERIALIZABLE`, or `Jdbc.Connection.TRANSACTION_NONE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

## Properties

None.
