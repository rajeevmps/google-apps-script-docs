# JdbcResultSet

A JDBC `ResultSet`. For documentation of this class, see `java.sql.ResultSet` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html).

## Methods

### absolute(row)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#absolute(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#absolute(int)).

**Parameters:**
- `row` (Integer): The number of the row to which the cursor moves to. A positive number indicates the row number counting from the start of the result set, while a negative number indicates the counting from the end of the result set.

**Returns:** `Boolean` — `true` if the cursor is moved to a position in this result set; `false` if the cursor is before the first row or after the last row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### afterLast()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#afterLast()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#afterLast()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### beforeFirst()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#beforeFirst()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#beforeFirst()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### cancelRowUpdates()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#cancelRowUpdates()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#cancelRowUpdates()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### clearWarnings()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#clearWarnings()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#clearWarnings()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### close()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#close()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#close()).

---

### deleteRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#deleteRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#deleteRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### findColumn(columnLabel)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#findColumn(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#findColumn(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Integer` — The column index of the specified column.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### first()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#first()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#first()).

**Returns:** `Boolean` — `true` if the cursor is on a valid row; `false` if there are no rows in the result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getArray(columnIndex)

Returns: `JdbcArray|null`

For documentation of this method, see `java.sql.ResultSet#getArray(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getArray(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcArray|null` — The value of the designated column in the current row of this result set as an array.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getArray(columnLabel)

Returns: `JdbcArray|null`

For documentation of this method, see `java.sql.ResultSet#getArray(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getArray(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcArray|null` — The value of the designated column in the current row of this result set as an array.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBigDecimal(columnIndex)

Returns: `BigNumber|null`

For documentation of this method, see `java.sql.ResultSet#getBigDecimal(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBigDecimal(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `BigNumber|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBigDecimal(columnLabel)

Returns: `BigNumber|null`

For documentation of this method, see `java.sql.ResultSet#getBigDecimal(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBigDecimal(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `BigNumber|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBlob(columnIndex)

Returns: `JdbcBlob|null`

For documentation of this method, see `java.sql.ResultSet#getBlob(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBlob(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcBlob|null` — The value of the designated column in the current row of this result set as a blob.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBlob(columnLabel)

Returns: `JdbcBlob|null`

For documentation of this method, see `java.sql.ResultSet#getBlob(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBlob(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcBlob|null` — The value of the designated column in the current row of this result set as a blob.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBoolean(columnIndex)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#getBoolean(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBoolean(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — The column value; `false` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBoolean(columnLabel)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#getBoolean(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBoolean(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Boolean` — The column value; `false` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getByte(columnIndex)

Returns: `Byte`

For documentation of this method, see `java.sql.ResultSet#getByte(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getByte(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Byte` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getByte(columnLabel)

Returns: `Byte`

For documentation of this method, see `java.sql.ResultSet#getByte(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getByte(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Byte` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBytes(columnIndex)

Returns: `Byte[]`

For documentation of this method, see `java.sql.ResultSet#getBytes(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBytes(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Byte[]` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getBytes(columnLabel)

Returns: `Byte[]`

For documentation of this method, see `java.sql.ResultSet#getBytes(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getBytes(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Byte[]` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getClob(columnIndex)

Returns: `JdbcClob|null`

For documentation of this method, see `java.sql.ResultSet#getClob(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getClob(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcClob|null` — The value of the designated column in the current row of this result set as a clob.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getClob(columnLabel)

Returns: `JdbcClob|null`

For documentation of this method, see `java.sql.ResultSet#getClob(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getClob(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcClob|null` — The value of the designated column in the current row of this result set as a clob.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getConcurrency()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getConcurrency()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getConcurrency()).

**Returns:** `Integer` — The concurrency type, which is either `Jdbc.ResultSet.CONCUR_READ_ONLY` or `Jdbc.ResultSet.CONCUR_UPDATABLE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getCursorName()

Returns: `String`

For documentation of this method, see `java.sql.ResultSet#getCursorName()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getCursorName()).

**Returns:** `String` — The SQL name for this result set's cursor.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDate(columnIndex)

Returns: `JdbcDate|null`

For documentation of this method, see `java.sql.ResultSet#getDate(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDate(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcDate|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDate(columnIndex, timeZone)

Returns: `JdbcDate|null`

For documentation of this method, see `java.sql.ResultSet#getDate(int, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDate(int,%20java.util.Calendar)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcDate|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDate(columnLabel)

Returns: `JdbcDate|null`

For documentation of this method, see `java.sql.ResultSet#getDate(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDate(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcDate|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDate(columnLabel, timeZone)

Returns: `JdbcDate|null`

For documentation of this method, see `java.sql.ResultSet#getDate(String, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDate(java.lang.String,%20java.util.Calendar)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcDate|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDouble(columnIndex)

Returns: `Number`

For documentation of this method, see `java.sql.ResultSet#getDouble(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDouble(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Number` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getDouble(columnLabel)

Returns: `Number`

For documentation of this method, see `java.sql.ResultSet#getDouble(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getDouble(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Number` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFetchDirection()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getFetchDirection()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getFetchDirection()).

**Returns:** `Integer` — The specified direction to set, which is either `Jdbc.ResultSet.FETCH_FORWARD` or `Jdbc.ResultSet.FETCH_REVERSE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFetchSize()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getFetchSize()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getFetchSize()).

**Returns:** `Integer` — The current fetch size for this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFloat(columnIndex)

Returns: `Number`

For documentation of this method, see `java.sql.ResultSet#getFloat(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getFloat(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Number` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getFloat(columnLabel)

Returns: `Number`

For documentation of this method, see `java.sql.ResultSet#getFloat(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getFloat(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Number` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getHoldability()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getHoldability()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getHoldability()).

**Returns:** `Integer` — The holdability of this result set, which is either `Jdbc.ResultSet.HOLD_CURSORS_OVER_COMMIT` or `Jdbc.ResultSet.CLOSE_CURSORS_AT_COMMIT`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getInt(columnIndex)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getInt(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getInt(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getInt(columnLabel)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getInt(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getInt(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getLong(columnIndex)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getLong(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getLong(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getLong(columnLabel)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getLong(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getLong(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getMetaData()

Returns: `JdbcResultSetMetaData`

For documentation of this method, see `java.sql.ResultSet#getMetaData()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getMetaData()).

**Returns:** `JdbcResultSetMetaData` — The number, types, and properties of this result set's columns.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getNClob(columnIndex)

Returns: `JdbcClob|null`

For documentation of this method, see `java.sql.ResultSet#getNClob(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getNClob(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcClob|null` — The column value of the current row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getNClob(columnLabel)

Returns: `JdbcClob|null`

For documentation of this method, see `java.sql.ResultSet#getNClob(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getNClob(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcClob|null` — The column value of the current row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getNString(columnIndex)

Returns: `String|null`

For documentation of this method, see `java.sql.ResultSet#getNString(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getNString(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `String|null` — The column value of the current row; `null` if the value is SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getNString(columnLabel)

Returns: `String|null`

For documentation of this method, see `java.sql.ResultSet#getNString(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getNString(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `String|null` — The column value of the current row; `null` if the value is SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getObject(columnIndex)

Returns: `Object`

For documentation of this method, see `java.sql.ResultSet#getObject(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getObject(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `Object` — The value of the designated column in the current row of this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getObject(columnLabel)

Returns: `Object`

For documentation of this method, see `java.sql.ResultSet#getObject(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getObject(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Object` — The value of the designated column in the current row of this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRef(columnIndex)

Returns: `JdbcRef|null`

For documentation of this method, see `java.sql.ResultSet#getRef(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getRef(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcRef|null` — The value of the designated column in the current row of this result set as a reference.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRef(columnLabel)

Returns: `JdbcRef|null`

For documentation of this method, see `java.sql.ResultSet#getRef(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getRef(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcRef|null` — The value of the designated column in the current row of this result set as a reference.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRow()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getRow()).

**Returns:** `Integer` — The current row number, or 0 if there is no current row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRowId(columnIndex)

Returns: `JdbcRowId|null`

For documentation of this method, see `java.sql.ResultSet#getRowId(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getRowId(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcRowId|null` — The column row ID value; `null` if the value is SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRowId(columnLabel)

Returns: `JdbcRowId|null`

For documentation of this method, see `java.sql.ResultSet#getRowId(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getRowId(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcRowId|null` — The column row ID value; `null` if the value is SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRows(queryString)

Returns: `Object[][]`

Returns all the rows from this `ResultSet` object.

The `queryString` consists of comma-separated calls to getter methods of this `JdbcResultSet`, for example: `"getString(1), getDouble('price'), getDate(3, 'UTC')"`. Supported methods include `getString`, `getInt`, `getDouble`, `getDate`, etc. Arguments can be integer column indices (1-based) or single/double quoted string column labels.

Usage: For example, to read column 1 from result set, instead of iterating using `next()`, use `getRows`, shown in the following examples.

The following example uses `next()`:

```text only
while (rs.next()) {
  Logger.log(rs.getString(1));
}
```

Use `getRows()` for better performance, in the following way:

```transact-sql
var rows = rs.getRows("getString(1)");
for (var i = 0; i < rows.length; i++) {
  Logger.log(rows[i][0]);
}
```

Note: For large results, you can use `getRows(queryString, batchSize)` for pagination.

**Parameters:**
- `queryString` (String): The SQL query string used to generate this result set.

**Returns:** `Object[][]` — The current rows from this `ResultSet` object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getRows(queryString, batchSize)

Returns: `Object[][]`

Returns up to `batchSize` rows from this `ResultSet` object. Consecutively calling this method starts iteration from where it left in previous iteration.

Usage:

```transact-sql
var rows;
do {
  rows = rs.getRows("getString(1)", 100);
  for (var i = 0; i < rows.length; i++) {
    Logger.log(rows[i][0]);
  }
} while(rows.length > 0);
```

**Parameters:**
- `queryString` (String): The SQL query string used to generate this result set.
- `batchSize` (Integer): The maximum number of rows to return in single call.

**Returns:** `Object[][]` — The current rows from this `ResultSet` object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSQLXML(columnIndex)

Returns: `JdbcSQLXML|null`

For documentation of this method, see `java.sql.ResultSet#getSQLXML(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getSQLXML(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcSQLXML|null` — The column value of the current row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSQLXML(columnLabel)

Returns: `JdbcSQLXML|null`

For documentation of this method, see `java.sql.ResultSet#getSQLXML(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getSQLXML(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcSQLXML|null` — The column value of the current row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getShort(columnIndex)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getShort(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getShort(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getShort(columnLabel)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getShort(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getShort(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `Integer` — The column value; 0 if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getStatement()

Returns: `JdbcStatement|null`

For documentation of this method, see `java.sql.ResultSet#getStatement()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getStatement()).

**Returns:** `JdbcStatement|null` — The statement that produced this result set, or `null` if the result set was produced some other way.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getString(columnIndex)

Returns: `String|null`

For documentation of this method, see `java.sql.ResultSet#getString(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getString(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `String|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getString(columnLabel)

Returns: `String|null`

For documentation of this method, see `java.sql.ResultSet#getString(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getString(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `String|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTime(columnIndex)

Returns: `JdbcTime|null`

For documentation of this method, see `java.sql.ResultSet#getTime(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTime(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcTime|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTime(columnIndex, timeZone)

Returns: `JdbcTime|null`

For documentation of this method, see `java.sql.ResultSet#getTime(int, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTime(int,%20java.util.Calendar)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcTime|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTime(columnLabel)

Returns: `JdbcTime|null`

For documentation of this method, see `java.sql.ResultSet#getTime(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTime(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcTime|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTime(columnLabel, timeZone)

Returns: `JdbcTime|null`

For documentation of this method, see `java.sql.ResultSet#getTime(String, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTime(java.lang.String,%20java.util.Calendar)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcTime|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTimestamp(columnIndex)

Returns: `JdbcTimestamp|null`

For documentation of this method, see `java.sql.ResultSet#getTimestamp(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTimestamp(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).

**Returns:** `JdbcTimestamp|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTimestamp(columnIndex, timeZone)

Returns: `JdbcTimestamp|null`

For documentation of this method, see `java.sql.ResultSet#getTimestamp(int, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTimestamp(int,%20java.util.Calendar)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve (the first column is 1, the second is 2, and so on).
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcTimestamp|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTimestamp(columnLabel)

Returns: `JdbcTimestamp|null`

For documentation of this method, see `java.sql.ResultSet#getTimestamp(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTimestamp(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `JdbcTimestamp|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTimestamp(columnLabel, timeZone)

Returns: `JdbcTimestamp|null`

For documentation of this method, see `java.sql.ResultSet#getTimestamp(String, Calendar)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getTimestamp(java.lang.String,%20java.util.Calendar)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `timeZone` (String): A time zone string used to construct java.lang.Calendar (https://docs.oracle.com/javase/6/docs/api/java/util/Calendar.html) instance, which in turn is used to build the date. Several formats of time zone strings are recognized: short IDs (such as `PST`, `EST`, and `GMT`), long IDs (such as `US/Pacific` and `America/Los_Angeles`), and offsets (such as `GMT+6:30`).

**Returns:** `JdbcTimestamp|null` — The column value; `null` if the value was SQL `NULL`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getType()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSet#getType()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getType()).

**Returns:** `Integer` — The type of this result set, which is one of `Jdbc.ResultSet.TYPE_FORWARD_ONLY`, `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`, or `Jdbc.ResultSet.TYPE_SCROLL_INSENSITIVE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getURL(columnIndex)

Returns: `String`

For documentation of this method, see `java.sql.ResultSet#getURL(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getURL(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to retrieve the data from (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The URL value of the designated column in the current row of this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getURL(columnLabel)

Returns: `String`

For documentation of this method, see `java.sql.ResultSet#getURL(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#getURL(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Returns:** `String` — The URL value of the designated column in the current row of this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getWarnings()

Returns: `String[]`

Returns the current set of warnings reported by the driver.

**Returns:** `String[]` — The current set of warnings.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### insertRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#insertRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#insertRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isAfterLast()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#isAfterLast()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#isAfterLast()).

**Returns:** `Boolean` — `true` if the cursor is after the last row; `false` if it is in any other position or if the result set contains no rows.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isBeforeFirst()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#isBeforeFirst()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#isBeforeFirst()).

**Returns:** `Boolean` — `true` if the cursor is before the first row; `false` if it is in any other position or if the result set contains no rows.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isClosed()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#isClosed()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#isClosed()).

**Returns:** `Boolean` — `true` if this result set is closed; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isFirst()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#isFirst()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#isFirst()).

**Returns:** `Boolean` — `true` if the cursor is on the first row; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isLast()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#isLast()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#isLast()).

**Returns:** `Boolean` — `true` if the cursor is on the last row; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### last()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#first()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#last()).

**Returns:** `Boolean` — `true` if the cursor is on a valid row; `false` if there are no rows in the result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### moveToCurrentRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#moveToCurrentRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#moveToCurrentRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### moveToInsertRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#moveToInsertRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#moveToInsertRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### next()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#next()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#next()).

**Returns:** `Boolean` — `true` if the new current row is valid; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### previous()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#previous()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#previous()).

**Returns:** `Boolean` — `true` if the cursor is on a valid row; `false` if the cursor is positioned before the first row.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### refreshRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#refreshRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#refreshRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### relative(rows)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#relative(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#relative(int)).

**Parameters:**
- `rows` (Integer): The number row steps to move the cursor. A positive number moves the cursor forward, while a negative number moves the cursor backward.

**Returns:** `Boolean` — `true` if the cursor is on a row; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### rowDeleted()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#rowDeleted()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#rowDeleted()).

**Returns:** `Boolean` — `true` if the current row was visibly deleted; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### rowInserted()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#rowInserted()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#rowInserted()).

**Returns:** `Boolean` — `true` if the current row was visibly inserted; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### rowUpdated()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#rowUpdated()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#rowUpdated()).

**Returns:** `Boolean` — `true` if the current row was visibly updated; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setFetchDirection(direction)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#setFetchDirection(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#setFetchDirection(int)).

**Parameters:**
- `direction` (Integer): The specified direction to set, which is either `Jdbc.ResultSet.FETCH_FORWARD` or `Jdbc.ResultSet.FETCH_REVERSE`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### setFetchSize(rows)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#setFetchSize(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#setFetchSize(int)).

**Parameters:**
- `rows` (Integer): The number of rows to fetch.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateArray(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateArray(int, Array)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateArray(int,%20java.sql.Array)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcArray): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateArray(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateArray(String, Array)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateArray(java.lang.String,%20java.sql.Array)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcArray): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBigDecimal(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBigDecimal(int, BigDecimal)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBigDecimal(int,%20java.math.BigDecimal)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (BigNumber): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBigDecimal(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBigDecimal(String, BigDecimal)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBigDecimal(java.lang.String,%20java.math.BigDecimal)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (BigNumber): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBlob(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBlob(int, Blob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBlob(int,%20java.sql.Blob)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcBlob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBlob(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRef(String, Blob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBlob(java.lang.String,%20java.sql.Blob)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcBlob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBoolean(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBoolean(int, boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBoolean(int,%20boolean)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Boolean): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBoolean(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBoolean(String, boolean)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBoolean(java.lang.String,%20boolean)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Boolean): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateByte(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateByte(int, byte)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateByte(int,%20byte)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Byte): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateByte(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateByte(String, byte)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateByte(java.lang.String,%20byte)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Byte): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBytes(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBytes(int, byte[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBytes(int,%20byte[])).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Byte[]): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateBytes(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateBytes(String, byte[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateBytes(java.lang.String,%20byte[])).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Byte[]): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateClob(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateClob(int, Clob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateClob(int,%20java.sql.Clob)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcClob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateClob(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateClob(String, Clob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateClob(java.lang.String,%20java.sql.Clob)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcClob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateDate(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateDate(int, Date)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateDate(int,%20java.sql.Date)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcDate): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateDate(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateDate(String, Date)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateDate(java.lang.String,%20java.sql.Date)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcDate): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateDouble(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateDouble(int, double)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateDouble(int,%20double)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Number): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateDouble(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateDouble(String, double)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateDouble(java.lang.String,%20double)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Number): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateFloat(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateFloat(int, float)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateFloat(int,%20float)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Number): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateFloat(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateFloat(String, float)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateFloat(java.lang.String,%20float)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Number): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateInt(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateInt(int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateInt(int,%20int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateInt(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateInt(String, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateInt(java.lang.String,%20int)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateLong(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateLong(int, long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateLong(int,%20long)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateLong(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateLong(String, long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateLong(java.lang.String,%20long)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNClob(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNClob(int, NClob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNClob(int,%20java.sql.NClob)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcClob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNClob(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNClob(String, NClob)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNClob(java.lang.String,%20java.sql.NClob)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcClob): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNString(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNString(int, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNString(int,%20java.lang.String)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (String): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNString(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNString(String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNString(java.lang.String,%20java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (String): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNull(columnIndex)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNull(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNull(int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateNull(columnLabel)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateNull(String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateNull(java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateObject(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateObject(int, Object)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateObject(int,%20java.lang.Object)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Object): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateObject(columnIndex, x, scaleOrLength)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateObject(int, Object, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateObject(int,%20java.lang.Object,%20int)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Object): The new column value.
- `scaleOrLength` (Integer): The number of digits after the decimal for `BigDecimal` types, or the length of data for `InputStream` or `Reader` types. Ignored for all other types.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateObject(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateObject(String, Object)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateObject(java.lang.String,%20java.lang.Object)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Object): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateObject(columnLabel, x, scaleOrLength)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateObject(String, Object, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateObject(java.lang.String,%20java.lang.Object,%20int)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Object): The new column value.
- `scaleOrLength` (Integer): The number of digits after the decimal for `BigDecimal` types, or the length of data for `InputStream` or `Reader` types. Ignored for all other types.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateRef(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRef(int, Ref)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateRef(int,%20java.sql.Ref)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcRef): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateRef(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRef(String, Ref)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateRef(java.lang.String,%20java.sql.Ref)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcRef): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateRow()

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRow()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateRow()).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateRowId(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRowId(int, RowId)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateRowId(int,%20java.sql.RowId)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcRowId): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateRowId(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateRowId(String, RowId)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateRowId(java.lang.String,%20java.sql.RowId)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcRowId): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateSQLXML(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateSQLXML(int, SQLXML)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateSQLXML(int,%20java.sql.SQLXML)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcSQLXML): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateSQLXML(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateSQLXML(String, SQLXML)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateSQLXML(java.lang.String,%20java.sql.SQLXML)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcSQLXML): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateShort(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateShort(int, short)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateShort(int,%20short)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateShort(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateShort(String, short)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateShort(java.lang.String,%20short)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (Integer): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateString(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateString(int, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateString(int,%20java.lang.String)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (String): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateString(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateString(String, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateString(java.lang.String,%20java.lang.String)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (String): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateTime(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateTime(int, Time)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateTime(int,%20java.sql.Time)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcTime): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateTime(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateTime(String, Time)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateTime(java.lang.String,%20java.sql.Time)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcTime): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateTimestamp(columnIndex, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateTimestamp(int, Timestamp)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateTimestamp(int,%20java.sql.Timestamp)).

**Parameters:**
- `columnIndex` (Integer): The index of the column to update (the first column is 1, the second is 2, and so on).
- `x` (JdbcTimestamp): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### updateTimestamp(columnLabel, x)

Returns: `void`

For documentation of this method, see `java.sql.ResultSet#updateTimestamp(String, Timestamp)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#updateTimestamp(java.lang.String,%20java.sql.Timestamp)).

**Parameters:**
- `columnLabel` (String): The label for the column, specified with the SQL AS clause. If the AS clause wasn't specified, then the label is the name of the column.
- `x` (JdbcTimestamp): The new column value.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### wasNull()

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSet#wasNull()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSet.html#wasNull()).

**Returns:** `Boolean` — `true` if the last column read was SQL `NULL`; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

## Properties

None.
