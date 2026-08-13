# JdbcResultSetMetaData

A JDBC `ResultSetMetaData`. For documentation of this class, see `java.sql.ResultSetMetaData` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html).

## Methods

### getCatalogName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getCatalogName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getCatalogName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The catalog name for the table in the designated column, or an empty string if not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnClassName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnClassName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnClassName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The fully-qualified name of the class of the designated column's values.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnCount()

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnCount()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnCount()).

**Returns:** `Integer` — The number of columns in this result set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnDisplaySize(column)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnDisplaySize(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnDisplaySize(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The maximum number of characters allowed as the width of the designated columns.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnLabel(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnLabel(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnLabel(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The designated column's suggested title, usually specifed by a SQL `AS` clause. Returns the same as `getColumnName(column)` if an `AS` is not specified.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The designated column's name.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnType(column)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnType(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnType(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The SQL type (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html) of the designated column.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getColumnTypeName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getColumnTypeName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getColumnTypeName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The designated column's database-specific type name. Returns the fully-qualifed type name if this is a user-defined type.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getPrecision(column)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#getPrecision(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getPrecision(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The maximum column size for the given column. For numeric data, this is the maximum precision. For character data, this is the length in characters. For datetime data, this is the length in characters of the string representation (assuming the maximum allowed precision of the fractional seconds component). For binary data, this is the length in bytes. For the `ROWID` datatype, this is the length in bytes. Returns 0 for types where the column size is not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getScale(column)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#getScale(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getScale(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The designated columns's number of digits to right of the decimal point. Returns 0 for data types where the scale is not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getSchemaName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getSchemaName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getSchemaName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The table schema of the designated column.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getTableName(column)

Returns: `String`

For documentation of this method, see `java.sql.ResultSetMetaData#getTableName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#getTableName(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `String` — The table name of the designated column, or an empty string if not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isAutoIncrement(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isAutoIncrement(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isAutoIncrement(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if the specified column is automatically numbered; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isCaseSensitive(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isCaseSensitive(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isCaseSensitive(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if the specified column is case-sensitive; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isCurrency(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isCurrency(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isCurrency(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if the specified column is a cash value; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isDefinitelyWritable(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isDefinitelyWritable(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isDefinitelyWritable(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if writes to the designated column definitely succeed; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isNullable(column)

Returns: `Integer`

For documentation of this method, see `java.sql.ResultSetMetaData#isNullable(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isNullable(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Integer` — The nullability status of the specified column, which is `Jdbc.ResultSetMetaData.columnNoNulls`, `Jdbc.ResultSetMetaData.columnNullable`, or `Jdbc.ResultSetMetaData.columnNullableUnknown`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isReadOnly(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isReadOnly(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isReadOnly(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if the designated column is definitely non-writable; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isSearchable(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isSearchable(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isSearchable(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if a where clause can use the specified column; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isSigned(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isSigned(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isSigned(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if the values in the specified column are signed numbers; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isWritable(column)

Returns: `Boolean`

For documentation of this method, see `java.sql.ResultSetMetaData#isWritable(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ResultSetMetaData.html#isWritable(int)).

**Parameters:**
- `column` (Integer): The index of the column to examine (the first column is 1, the second is 2, and so on).

**Returns:** `Boolean` — `true` if it is possible to write to the designated column; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

## Properties

None.
