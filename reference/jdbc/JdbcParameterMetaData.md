# JdbcParameterMetaData

A JDBC `ParameterMetaData`. For documentation of this class, see `java.sql.ParameterMetaData` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html).

## Methods

### getParameterClassName(param)

Returns: `String`

For documentation of this method, see `java.sql.ParameterMetaData#getParameterClassName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getParameterClassName(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `String` — The fully-qualified Java class name that is used by the `JdbcPreparedStatement.setObject(index, x)` methods.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getParameterCount()

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#getParameterCount()` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getParameterCount()).

**Returns:** `Integer` — The number of parameters for which this metadata contains information.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getParameterMode(param)

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#getParameterMode(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getParameterMode(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Integer` — The designated parameter's mode, which is one of `Jdbc.ParameterMetaData.parameterModeIn`, `Jdbc.ParameterMetaData.parameterModeOut`, `Jdbc.ParameterMetaData.parameterModeInOut`, or `Jdbc.ParameterMetaData.parameterModeUnknown`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getParameterType(param)

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#getParameterType(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getParameterType(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Integer` — The designated parameter's SQL type (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html).

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getParameterTypeName(param)

Returns: `String`

For documentation of this method, see `java.sql.ParameterMetaData#getParameterTypeName(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getParameterTypeName(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `String` — The designated parameter's database-specific type name. This is a fully-qualified type name if the parameter is a user-defined type.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getPrecision(param)

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#getPrecision(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getPrecision(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Integer` — The maximum column size for the given parameter. For numeric data, this is the maximum precision. For character data, this is the length in characters. For datetime data, this is the length in characters of the string representation (assuming the maximum allowed precision of the fractional seconds component). For binary data, this is the length in bytes. For the `ROWID` datatype, this is the length in bytes. Returns 0 for types where the column size is not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getScale(param)

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#getScale(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#getScale(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Integer` — The designated parameter's number of digits to right of the decimal point. Returns 0 for data types where the scale is not applicable.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isNullable(param)

Returns: `Integer`

For documentation of this method, see `java.sql.ParameterMetaData#isNullable(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#isNullable(int)).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Integer` — The nullability status of the given parameter; one of `Jdbc.ParameterMetaData.parameterNoNulls`, `Jdbc.ParameterMetaData.parameterNullable`, or `Jdbc.ParameterMetaData.parameterNullableUnknown`.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### isSigned(param)

Returns: `Boolean`

For documentation of this method, see `java.sql.ParameterMetaData#isSigned(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/ParameterMetaData.html#isSigned(int))).

**Parameters:**
- `param` (Integer): The index of the parameter to examine. The first parameter has an index of 1.

**Returns:** `Boolean` — `true` if the specified parameter can accept signed number values; `false` otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

## Properties

None.
