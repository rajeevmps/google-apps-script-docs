# JdbcTimestamp

A JDBC `Timestamp`. For documentation of this class, see `java.sql.Timestamp` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html).

## Methods

### after(when)

Returns: `Boolean`

For documentation of this method, see `java.sql.Timestamp#after(Timestamp)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#after(java.sql.Timestamp)).

**Parameters:**
- `when` (JdbcTimestamp): A timestamp to compare to.

**Returns:** `Boolean` — `true` if and only if this timestampe is strictly later than the timestamp specified as a parameter; `false` otherwise.

---

### before(when)

Returns: `Boolean`

For documentation of this method, see `java.sql.Timestamp#before(Timestamp)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#before(java.sql.Timestamp)).

**Parameters:**
- `when` (JdbcTimestamp): A timestamp to compare to.

**Returns:** `Boolean` — `true` if and only if this timestamp is strictly earlier than the timestamp specified as a parameter; `false` otherwise.

---

### getDate()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getDate()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getDate()).

**Returns:** `Integer` — The day of the month represented by this timestamp. The value returned is between 1 and 31 representing the day of the month that contains or begins with the instant in time represented by this timestamp, as interpreted in the local time zone.

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

### getMonth()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getMonth()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getMonth()).

**Returns:** `Integer` — The month that contains or begins with the instant in time represented by this timestamp. The value returned is between 0 and 11, with the value 0 representing January.

---

### getNanos()

Returns: `Integer`

For documentation of this method, see `java.sql.Timestamp#getNanos()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#getNanos()).

**Returns:** `Integer` — This timestamp's fractional seconds value (nanoseconds).

---

### getSeconds()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getSeconds()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getSeconds()).

**Returns:** `Integer` — The seconds past the minute represented by this object, as interpreted in the local time zone. The value is a number between 0 through 61 inclusive, whiere 60 and 61 are only possible for machines that take leap seconds into account.

---

### getTime()

Returns: `Integer`

For documentation of this method, see `java.sql.Timestamp#getTime()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#getTime()).

**Returns:** `Integer` — The number of milliseconds since January 1, 1970, 00:00:00 GMT represented by this time object.

---

### getYear()

Returns: `Integer`

For documentation of this method, see `java.sql.Date#getYear()` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#getYear()).

**Returns:** `Integer` — A value that is the result of subtracting 1900 from the year that contains or begins with the instant in time represented by this timestampe, as interpreted in the local time zone.

---

### setDate(date)

Returns: `void`

For documentation of this method, see `java.sql.Date#setDate(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setDate(int)).

**Parameters:**
- `date` (Integer): The day of month to set. This timestamp is updated to represent a point in time within the specified day of month, with the year, month, hour, minute, and second the same as before, as interpreted in the local time zone. If the date was April 30, for example, and the date is set to 31, then it is treated as if it were on May 1, because April has only 30 days.

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

### setMonth(month)

Returns: `void`

For documentation of this method, see `java.sql.Date#setMonth(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setMonth(int)).

**Parameters:**
- `month` (Integer): The month to set. This timestamp is updated to represent a point in time within the specified month, with the year, date, hour, minute, and second the same as before, as interpreted in the local time zone. If the date was October 31, for example, and the month is set to June, then the new date is treated as if it were on July 1, because June has only 30 days.

---

### setNanos(nanoseconds)

Returns: `void`

For documentation of this method, see `java.sql.Timestamp#setNanos(int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#setNanos(int)).

**Parameters:**
- `nanoseconds` (Integer): The new fractional seconds value.

---

### setSeconds(seconds)

Returns: `void`

For documentation of this method, see `java.sql.Date#setSeconds(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setSeconds(int)).

**Parameters:**
- `seconds` (Integer): The seconds to set; this object is updated to represent a point in time within the specified second of the minute, with the year, month, date, hour, and minute the same as before, as interpreted in the local time zone.

---

### setTime(milliseconds)

Returns: `void`

For documentation of this method, see `java.sql.Timestamp#setTime(long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Timestamp.html#setTime(long)).

**Parameters:**
- `milliseconds` (Integer): The time value to set. The value is milliseconds since January 1, 1970, 00:00:00 GMT.

---

### setYear(year)

Returns: `void`

For documentation of this method, see `java.sql.Date#setYear(int)` (https://docs.oracle.com/javase/6/docs/api/java/util/Date.html#setYear(int)).

**Parameters:**
- `year` (Integer): The year value to set; the timestamp's year is set to this value plus 1900. This timestamp is updated to represent a point in time within the specified year, with the month, date, hour, minute, and second the same as before, as interpreted in the local time zone. If the date was February 29, for example, and the year is set to a non-leap year, then the new date is treated as if it were on March 1.

## Properties

None.
