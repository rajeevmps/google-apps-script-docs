# Jdbc

The JDBC service allows scripts to connect to Google Cloud SQL (https://developers.google.com/cloud-sql), MySQL, Microsoft SQL Server, Oracle, and PostgreSQL databases. For more information, see the guide to JDBC (https://developers.google.com/apps-script/guides/jdbc).

## Methods

### getCloudSqlConnection(url)

Returns: `JdbcConnection`

Attempts to establish a connection to the given Google Cloud SQL URL.

**Parameters:**
- `url` (String): A database URL of the form `jdbc:google:mysql://subname`.

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/sqlservice`

---

### getCloudSqlConnection(url, info)

Returns: `JdbcConnection`

Attempts to establish a connection to the given Google Cloud SQL URL.

**Parameters:**
- `url` (String): A database URL of the form `jdbc:google:mysql://subname`.
- `info` (Object): Optional JavaScript object specifying advanced parameters as defined below.
- `connectTimeoutSeconds` (Integer): connection timeout in seconds
- `database` (String): the database to connect to
- `instance` (String): the name of a Google SQL Service instance
- `password` (String): the user's password
- `queryTimeoutSeconds` (Integer): query timeout in seconds
- `user` (String): the username to pass to the database

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/sqlservice`

---

### getCloudSqlConnection(url, userName, password)

Returns: `JdbcConnection`

Attempts to establish a connection to the given Google Cloud SQL URL.

**Parameters:**
- `url` (String): A database URL of the form `jdbc:google:mysql://subname`.
- `userName` (String): The username to pass to the database.
- `password` (String): The user's password.

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/sqlservice`

---

### getConnection(url)

Returns: `JdbcConnection`

Attempts to establish a connection to the given database URL.

```javascript
const conn = Jdbc.getConnection(
    'jdbc:mysql://yoursqlserver.example.com:3306/database_name',
);
```

**Parameters:**
- `url` (String): A database URL of the form `jdbc:subprotocol:subname`.

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getConnection(url, info)

Returns: `JdbcConnection`

Attempts to establish a connection to the given database URL.

```javascript
const conn = Jdbc.getConnection(
    'jdbc:mysql://yoursqlserver.example.com:3306/database_name',
    {user: 'username', password: 'password'},
);
```

**Parameters:**
- `url` (String): A database URL of the form `jdbc:subprotocol:subname`.
- `info` (Object): Optional JavaScript object specifying advanced parameters as defined below.
- `databaseName` (String): the database to connect to
- `password` (String): the user's password
- `useJDBCCompliantTimeZoneShift` (Boolean): whether or not the connection should comply with JDBC rules when converting time zones. The default is `false`.
- `user` (String): the username to pass to the database
- `_serverSslCertificate` (String): the server's SSL certificate
- `_clientSslCertificate` (String): the client's SSL certificate
- `_clientSslKey` (String): the client's SSL key

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### getConnection(url, userName, password)

Returns: `JdbcConnection`

Attempts to establish a connection to the given database using a username and password.

```javascript
const conn = Jdbc.getConnection(
    'jdbc:mysql://yoursqlserver.example.com:3306/database_name',
    'username',
    'password',
);
```

**Parameters:**
- `url` (String): A database URL of the form `jdbc:subprotocol:subname`.
- `userName` (String): The username to pass to the database.
- `password` (String): The user's password.

**Returns:** `JdbcConnection` — A JdbcConnection object.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/script.external_request`

---

### newDate(milliseconds)

Returns: `JdbcDate`

Create a date from milliseconds since epoch.

**Parameters:**
- `milliseconds` (Integer): Milliseconds since epoch.

**Returns:** `JdbcDate` — A JdbcDate object.

---

### newTime(milliseconds)

Returns: `JdbcTime`

Create a time from milliseconds since epoch.

**Parameters:**
- `milliseconds` (Integer): Milliseconds since epoch.

**Returns:** `JdbcTime` — A JdbcTime object.

---

### newTimestamp(milliseconds)

Returns: `JdbcTimestamp`

Create a timestamp from milliseconds since epoch.

**Parameters:**
- `milliseconds` (Integer): Milliseconds since epoch.

**Returns:** `JdbcTimestamp` — A JdbcTimestamp object.

---

### parseDate(date)

Returns: `JdbcDate`

Create a date by parsing the SQL date string.

**Parameters:**
- `date` (String): A string containing a SQL date string.

**Returns:** `JdbcDate` — A JdbcDate object.

---

### parseTime(time)

Returns: `JdbcTime`

Create a time by parsing the SQL time string.

**Parameters:**
- `time` (String): A string containing a SQL time string.

**Returns:** `JdbcTime` — A JdbcTime object.

---

### parseTimestamp(timestamp)

Returns: `JdbcTimestamp`

Create a timestamp by parsing the SQL timestamp string.

**Parameters:**
- `timestamp` (String): A string containing a SQL timestamp string.

**Returns:** `JdbcTimestamp` — A JdbcTimestamp object.

## Properties

None.
