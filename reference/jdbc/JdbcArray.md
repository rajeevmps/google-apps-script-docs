# JdbcArray

A JDBC `Array`. For documentation of this class, see `java.sql.Array` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html).

## Methods

### free()

Returns: `void`

For documentation of this method, see `java.sql.Array#free()` (http://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#free()).

---

### getArray()

Returns: `Object`

For documentation of this method, see `java.sql.Array#getArray()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getArray())

**Returns:** `Object` — An object containing the ordered elements of the SQL array value.

---

### getArray(index, count)

Returns: `Object`

For documentation of this method, see `java.sql.Array#getArray(long, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getArray(long,%20int)).

**Parameters:**
- `index` (Integer): The array index of the first element to retrieve, where the first element has an index of 1.
- `count` (Integer): The number of successive SQL array elements to retrieve.

**Returns:** `Object` — An object containing up to the specified number of consecutive SQL array elements.

---

### getBaseType()

Returns: `Integer`

For documentation of this method, see `java.sql.Array#getBaseType()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getBaseType()).

**Returns:** `Integer` — The type code (https://docs.oracle.com/javase/6/docs/api/java/sql/Types.html) for the elements in this array.

---

### getBaseTypeName()

Returns: `String`

For documentation of this method, see `java.sql.Array#getBaseTypeName()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getBaseTypeName()).

**Returns:** `String` — The database-specific name for the built-in base type or else the fully-qualified SQL type name for a base type that is a UDT.

---

### getResultSet()

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.Array#getResultSet()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getResultSet()).

**Returns:** `JdbcResultSet` — The `JdbcResultSet` containing one row for each of the elements in the array designated by this Array object, with the rows in ascending order based on the indices.

---

### getResultSet(index, count)

Returns: `JdbcResultSet`

For documentation of this method, see `java.sql.Array#getResultSet(long, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Array.html#getResultSet(long,%20int)).

**Parameters:**
- `index` (Integer): The array index of the first element to retrieve, where the first element has an index of 1.
- `count` (Integer): The number of successive SQL array elements to retrieve.

**Returns:** `JdbcResultSet` — A `JdbcResultSet` containing up to the specified number of consecutive SQL array elements.

## Properties

None.
