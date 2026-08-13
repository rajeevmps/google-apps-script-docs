# JdbcTime

A JDBC `Time`. For documentation of this class, see `java.sql.Time` (https://docs.oracle.com/javase/6/docs/api/java/sql/Time.html).

## Methods

### after(when)

Returns: `Boolean`

For documentation of this method, see `java.sql.Date#after(Date)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#after(java.util.Date)).

**Parameters:**
- `when` (JdbcTime): A time to compare to.

**Returns:** `Boolean` — `true` if and only if this time is strictly later than the time specified as a parameter; `false` otherwise.

---

### before(when)

Returns: `Boolean`

For documentation of this method, see `java.sql.Date#before(Date)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#before(java.util.Date)).

**Parameters:**
- `when` (JdbcTime): A time to compare to.

**Returns:** `Boolean` — `true` if and only if this time is strictly earlier than the time specified as a parameter; `false` otherwise.

---

### getHours()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getHours()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getHours()).

**Returns:** `Integer` — The hour represented by this object; the value is a number (0 through 23) representing the hour within the day that contains or begins with the instant in time represented by this object, as interpreted in the local time zone.

---

### getMinutes()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getMinutes()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getMinutes()).

**Returns:** `Integer` — The minutes past the hour represented by this object, as interpreted in the local time zone. The value is a number between 0 through 59 inclusive.

---

### getSeconds()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getSeconds()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getSeconds()).

**Returns:** `Integer` — The seconds past the minute represented by this object, as interpreted in the local time zone. The value is a number between 0 through 61 inclusive, whiere 60 and 61 are only possible for machines that take leap seconds into account.

---

### getTime()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getTime()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getTime()).

**Returns:** `Integer` — The number of milliseconds since January 1, 1970, 00:00:00 GMT represented by this time object.

---

### setHours(hours)

Returns: `void`

For documentation of this method, see `java.sql.Date#setHours(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setHours(int)).

**Parameters:**
- `hours` (Integer): The hour to set; this object is updated to represent a point in time within the specified hour of the day, with the year, month, date, minute, and second the same as before, as interpreted in the local time zone.

---

### setMinutes(minutes)

Returns: `void`

For documentation of this method, see `java.sql.Date#setMinutes(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setMinutes(int)).

**Parameters:**
- `minutes` (Integer): The minutes to set; this object is updated to represent a point in time within the specified minute of the hour, with the year, month, date, hour, and second the same as before, as interpreted in the local time zone.

---

### setSeconds(seconds)

Returns: `void`

For documentation of this method, see `java.sql.Date#setSeconds(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setSeconds(int)).

**Parameters:**
- `seconds` (Integer): The seconds to set; this object is updated to represent a point in time within the specified second of the minute, with the year, month, date, hour, and minute the same as before, as interpreted in the local time zone.

---

### setTime(milliseconds)

Returns: `void`

For documentation of this method, see `java.sql.Time#setTime(long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Time.html#setTime(long)).

**Parameters:**
- `milliseconds` (Integer): The time value to set. The value is milliseconds since January 1, 1970, 00:00:00 GMT, while a negative number is milliseconds before that time.

## Properties

None.
