# Properties Service

The [Properties service](https://developers.google.com/apps-script/reference/properties) stores data in
key-value pairs scoped to one script, one user of a script, or one document in
which a [add-on](https://developers.google.com/workspace/add-ons/overview) is used.
It's typically used to store developer configuration or user preferences.
Properties are never shared between scripts.

To view the daily quotas and storage limits for the Properties service, see
[Quotas for Google Services](https://developers.google.com/apps-script/guides/services/quotas).

## Comparison of property stores

The
[`PropertiesService`](https://developers.google.com/apps-script/reference/properties/properties-service)
global object offers three methods, each of which returns a similar
[`Properties`](https://developers.google.com/apps-script/reference/properties/properties)
object but with different access rights, as shown in the following table:

|   | Script Properties | User Properties | Document Properties |
|---|---|---|---|
| Method to access | `https://developers.google.com/apps-script/reference/properties/properties-service#getScriptProperties()` | `https://developers.google.com/apps-script/reference/properties/properties-service#getUserProperties()` | `https://developers.google.com/apps-script/reference/properties/properties-service#getDocumentProperties()` |
| Data shared among | All users of a script, add-on, or web app | The current user of a script, add-on, or web app | All users of an add-on in the open document |
| Typically used for | App-wide configuration data, like the username and password for the developer's external database | User-specific settings, like metric or imperial units | Document-specific data, like the source URL for an embedded chart |

## Data format

The Properties service stores all data as strings in key-value pairs. Data types
that are not already strings are automatically converted to strings, including
methods contained within saved objects.

## Save data

To save a single value, call the method [`Properties.setProperty(key,
value)`](https://developers.google.com/apps-script/reference/properties/properties#setProperty(String,String))
of the appropriate store, as shown in the following example:
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Set a property in each of the three property stores.
  const scriptProperties = PropertiesService.getScriptProperties();
  const userProperties = PropertiesService.getUserProperties();
  const documentProperties = PropertiesService.getDocumentProperties();

  scriptProperties.setProperty("SERVER_URL", "http://www.example.com/");
  userProperties.setProperty("DISPLAY_UNITS", "metric");
  documentProperties.setProperty(
    "SOURCE_DATA_ID",
    "1j3GgabZvXUF177W0Zs_2v--H6SPCQb4pmZ6HsTZYT5k",
  );
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

To save data in bulk, pass a map of key-value pairs to
[`Properties.setProperties(properties)`](https://developers.google.com/apps-script/reference/properties/properties#setProperties(Object)).
Each key-value pair of the object in the parameter is stored as a separate
property:
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Set multiple script properties in one call.
  const scriptProperties = PropertiesService.getScriptProperties();
  scriptProperties.setProperties({
    cow: "moo",
    sheep: "baa",
    chicken: "cluck",
  });
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

## Read data

To retrieve a single value that you have previously saved, call
[`Properties.getProperty`](https://developers.google.com/apps-script/reference/properties/properties#getProperty(String)):
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Get the value for the user property 'DISPLAY_UNITS'.
  const userProperties = PropertiesService.getUserProperties();
  const units = userProperties.getProperty("DISPLAY_UNITS");
  console.log("values of units %s", units);
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

To retrieve all values in the current property store, call
[`Properties.getProperties`](https://developers.google.com/apps-script/reference/properties/properties#getProperties()):
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Get multiple script properties in one call, then log them all.
  const scriptProperties = PropertiesService.getScriptProperties();
  const data = scriptProperties.getProperties();
  for (const key in data) {
    console.log("Key: %s, Value: %s", key, data[key]);
  }
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

## Modify data

The methods `getProperty` and `getProperties` return a copy of the stored
data, not a live view, so changing the returned object doesn't update the value
in the property store. To update the data in the store, save it again:
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Change the unit type in the user property 'DISPLAY_UNITS'.
  const userProperties = PropertiesService.getUserProperties();
  let units = userProperties.getProperty("DISPLAY_UNITS");
  units = "imperial"; // Only changes local value, not stored value.
  userProperties.setProperty("DISPLAY_UNITS", units); // Updates stored value.
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

## Delete data

To delete a single value, call
[`Properties.deleteProperty`](https://developers.google.com/apps-script/reference/properties/properties#deleteProperty(String)):
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Delete the user property 'DISPLAY_UNITS'.
  const userProperties = PropertiesService.getUserProperties();
  userProperties.deleteProperty("DISPLAY_UNITS");
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

To delete all properties in the current store, call
[`Properties.deleteAllProperties`](https://developers.google.com/apps-script/reference/properties/properties#deleteAllProperties()):
service/propertyService.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/propertyService.gs)

```javascript
try {
  // Get user properties in the current script.
  const userProperties = PropertiesService.getUserProperties();
  // Delete all user properties in the current script.
  userProperties.deleteAllProperties();
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with error %s", err.message);
}
```

## Manage script properties manually

Manually add up to fifty custom properties, as strings in key-value pairs, from
the project settings page. To add more than fifty properties, add them
programmatically using the methods described in the preceding section in
[Save data](https://developers.google.com/apps-script/guides/properties#save_data). When you set script properties from the project
settings page, don't reference script variables.

### Add script properties

1. Open your Google Apps Script project.
2. At the left, click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).
3. To add the first property, under **Script Properties** click **Add script property**.
4. To add second and subsequent properties, under **Script Properties** click **Edit script properties** \> **Add script property**.
5. For **Property**, enter the key name.
6. For **Value**, enter the value for the key.
7. (Optional) To add more properties, click **Add script property**.
8. Click **Save script properties**.

### Edit script properties

1. Open your Apps Script project.
2. At the left, click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).
3. Under **Script Properties** , click **Edit script properties**.
4. Make changes to the key name and key value for each property you want to change.
5. Click **Save script properties**.

### Delete script properties

1. Open your Apps Script project.
2. At the left, click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).
3. Under **Script Properties** , click **Edit script properties**.
4. Next to the property that you want to delete, click **Remove** .
5. Click **Save script properties**.


Versions 1.0 and 1.1 of the TLS security protocol are disabled. To
establish connections, use TLS 1.2 or higher.

Google Apps Script can connect to external databases through the
[JDBC service](https://developers.google.com/apps-script/reference/jdbc), a wrapper around the standard
[Java Database Connectivity technology](http://www.oracle.com/technetwork/java/javase/jdbc/index.html).
The JDBC service supports Google Cloud SQL for MySQL, MySQL, Microsoft SQL
Server, Oracle and PostgreSQL databases.

If your spreadsheet is growing too large or you're experiencing timeout issues with complex calculations, moving your data to an external database can significantly improve performance and reliability.

To update an external database with JDBC, your script must open a connection
to the database and then make changes by sending SQL statements.

## Google Cloud SQL databases

[Google Cloud SQL](https://developers.google.com/sql) lets you create relational
databases that live in Google's cloud. Cloud SQL might incur charges based on
your usage.

Create a Google Cloud SQL instance by following the steps listed in the
[Cloud SQL quickstart](https://developers.google.com/sql/docs/quickstart).

### Create Google Cloud SQL connections

There are two ways of establishing a connection with a Google Cloud SQL
database using Apps Script's [JDBC service](https://developers.google.com/apps-script/reference/jdbc):

- (Recommended) Connecting using [Jdbc.getCloudSqlConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getcloudsqlconnectionurl)
- Connecting using [Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl)

Both are valid, but the second method requires you to authorize a set of IP
ranges for access to your database.

#### Use [Jdbc.getCloudSqlConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getcloudsqlconnectionurl) (recommended)

This method creates a connection to a Google Cloud SQL MySQL instance using the
[Jdbc.getCloudSqlConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getcloudsqlconnectionurl)
method. The database URL has the form of `jdbc:google:mysql://subname`, where
`subname` is the MySQL **Instance Connection Name** listed on the Cloud SQL
instance **Overview** page in the [Google Cloud console](https://console.cloud.google.com/).

To connect to Cloud SQL SQL Server, see
[Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl).

#### Use [Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl)

In order to use this method, you must authorize certain
[Classless Inter-Domain Routing (CIDR)](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
IP address ranges so that Apps Script's servers can connect to
your database. Before running your script, complete the following steps:

1. In your Google Cloud SQL instance,
   [authorize the IP ranges](https://cloud.google.com/sql/docs/mysql/configure-ip#add),
   one at at time from this [data source](https://www.gstatic.com/ipranges/goog_ipv4_only.txt).

2. Copy the URL that was assigned to your database; it should have the
   form `jdbc:mysql:subname`.

Once you've authorized these IP ranges, create connections to your Google Cloud
SQL instance using one of the
[Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl)
methods and the URL you copied earlier.

## Other databases

If you already have your own MySQL, Microsoft SQL Server, Oracle or PostgreSQL
database, connect to it through Apps Script's JDBC service.

### Create other database connections

In order to create a database connection using the Apps Script
[JDBC service](https://developers.google.com/apps-script/reference/jdbc), in your database settings
you must authorize IP ranges from [this data source](https://www.gstatic.com/ipranges/goog.json).

The JDBC service can only connect to ports 1025 or later. Ensure your
database is not serving off a lower port.

Once these allowlists are in place, create a connection to the database
using one of the
[Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl)
methods and your database's URL.

## Sample code

The following sample code assumes you are connecting to a Google Cloud SQL
database, and creates database connections using the
[Jdbc.getCloudSqlConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getcloudsqlconnectionurl)
method. For other databases you must use the
[Jdbc.getConnection](https://developers.google.com/apps-script/reference/jdbc/jdbc#getconnectionurl)
method to create database connections.

For more information on the JDBC methods, see the
[Java documentation for JDBC](http://docs.oracle.com/javase/7/docs/api/java/sql/package-summary.html).

### Create a database, user, and table

Most developers use the
[MySQL command-line tool](http://dev.mysql.com/doc/refman/5.5/en/mysql.html) to
create databases, users, and tables. However, it's possible to do the same
thing in Apps Script, as shown in the following example. Create at
least one other user so that your script doesn't always have to connect to the
database as `root`.
service/jdbc.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/jdbc.gs)

```javascript
/**
 * Create a new database within a Cloud SQL instance.
 */
function createDatabase() {
  try {
    const conn = Jdbc.getCloudSqlConnection(instanceUrl, root, rootPwd);
    conn.createStatement().execute(`CREATE DATABASE ${db}`);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}

/**
 * Create a new user for your database with full privileges.
 */
function createUser() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, root, rootPwd);

    const stmt = conn.prepareStatement("CREATE USER ? IDENTIFIED BY ?");
    stmt.setString(1, user);
    stmt.setString(2, userPwd);
    stmt.execute();

    conn.createStatement().execute(`GRANT ALL ON \`%\`.* TO ${user}`);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}

/**
 * Create a new table in the database.
 */
function createTable() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);
    conn
      .createStatement()
      .execute(
        "CREATE TABLE entries " +
          "(guestName VARCHAR(255), content VARCHAR(255), " +
          "entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));",
      );
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}
```

### Write to the database

The following examples demonstrate how to write a single record to the database
as well as a batch of 500 records. Batching is vital for bulk operations.

Parameterized statements are used, in which the variables are denoted by `?`. To
prevent [SQL injection attacks](https://en.wikipedia.org/wiki/SQL_injection),
use parameterized statements to escape all user-supplied data.
service/jdbc.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/jdbc.gs)

```javascript
/**
 * Write one row of data to a table.
 */
function writeOneRecord() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);

    const stmt = conn.prepareStatement(
      "INSERT INTO entries " + "(guestName, content) values (?, ?)",
    );
    stmt.setString(1, "First Guest");
    stmt.setString(2, "Hello, world");
    stmt.execute();
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}

/**
 * Write 500 rows of data to a table in a single batch.
 */
function writeManyRecords() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);
    conn.setAutoCommit(false);

    const start = new Date();
    const stmt = conn.prepareStatement(
      "INSERT INTO entries " + "(guestName, content) values (?, ?)",
    );
    for (let i = 0; i < 500; i++) {
      stmt.setString(1, `Name ${i}`);
      stmt.setString(2, `Hello, world ${i}`);
      stmt.addBatch();
    }

    const batch = stmt.executeBatch();
    conn.commit();
    conn.close();

    const end = new Date();
    console.log("Time elapsed: %sms for %s rows.", end - start, batch.length);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}

/**
 * Write 500 rows of data to a table in a single batch.
 * Recommended for faster writes
 */
function writeManyRecordsUsingExecuteBatch() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);
    conn.setAutoCommit(false);

    const start = new Date();
    const stmt = conn.prepareStatement(
      "INSERT INTO entries " + "(guestName, content) values (?, ?)",
    );
    const params = [];
    for (let i = 0; i < 500; i++) {
      params.push([`Name ${i}`, `Hello, world ${i}`]);
    }

    const batch = stmt.executeBatch(params);
    conn.commit();
    conn.close();

    const end = new Date();
    console.log("Time elapsed: %sms for %s rows.", end - start, batch.length);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}
```

### Read from the database

This example demonstrates how to read a large number of records from the
database, looping over the result set as necessary.
service/jdbc.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/service/jdbc.gs)

```javascript
/**
 * Read up to 1000 rows of data from the table and log them.
 */
function readFromTable() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);
    const start = new Date();
    const stmt = conn.createStatement();
    stmt.setMaxRows(1000);
    const results = stmt.executeQuery("SELECT * FROM entries");
    const numCols = results.getMetaData().getColumnCount();

    while (results.next()) {
      let rowString = "";
      for (let col = 0; col < numCols; col++) {
        rowString += `${results.getString(col + 1)}\t`;
      }
      console.log(rowString);
    }

    results.close();
    stmt.close();

    const end = new Date();
    console.log("Time elapsed: %sms", end - start);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}

/**
 * Read up to 1000 rows of data from the table and log them.
 * Recommended for faster reads
 */
function readFromTableUsingGetRows() {
  try {
    const conn = Jdbc.getCloudSqlConnection(dbUrl, user, userPwd);
    const start = new Date();
    const stmt = conn.createStatement();
    stmt.setMaxRows(1000);
    const results = stmt.executeQuery("SELECT * FROM entries");
    const numCols = results.getMetaData().getColumnCount();
    const getRowArgs = [];
    for (let col = 0; col < numCols; col++) {
      getRowArgs.push(`getString(${col + 1})`);
    }
    const rows = results.getRows(getRowArgs.join(","));
    for (let i = 0; i < rows.length; i++) {
      console.log(rows[i].join("\t"));
    }

    results.close();
    stmt.close();

    const end = new Date();
    console.log("Time elapsed: %sms", end - start);
  } catch (err) {
    // TODO(developer) - Handle exception from the API
    console.log("Failed with an error %s", err.message);
  }
}
```

## Close connections

JDBC connections close automatically when a script finishes executing. (Single
[`google.script.run`](https://developers.google.com/apps-script/guides/html/communication) calls count as a
complete execution, even if the HTML service page that made the call remains
open.)

Nonetheless, if you know you're done with a connection, statement, or result set
before the end of the script, close them manually by calling
[`JdbcConnection.close`](https://developers.google.com/apps-script/reference/jdbc/jdbc-connection#close()),
[`JdbcStatement.close`](https://developers.google.com/apps-script/reference/jdbc/jdbc-statement#close()),
or
[`JdbcResultSet.close`](https://developers.google.com/apps-script/reference/jdbc/jdbc-result-set#close()).

Showing an [alert or prompt dialog](https://developers.google.com/apps-script/guides/dialogs#alert_dialogs)
also terminates any open JDBC connections. However, other showing UI elements
---like custom menus or dialogs and sidebars with custom content ---does
not.

*Google, Google Workspace, and related marks and logos are trademarks of
Google LLC. All other company and product names are trademarks of the companies
with which they are associated.*

# Content Service

that return raw textual content of various MIME types.

When a script is published as a web app, the callback functions `doGet` and
`doPost` execute whenever a request is made to the script's URL. Instead of
returning a user interface object created with the
[HTML service](https://developers.google.com/apps-script/guides/html), the
[Content service](https://developers.google.com/apps-script/reference/content) can return raw textual
content. Write scripts that act as services, responding to `GET` and `POST`
requests and serving data of various MIME types.

## The basics

The following example shows how to use the Content service:

    function doGet() {
      return ContentService.createTextOutput('Hello, world!');
    }

[Deploy the script as a web app](https://developers.google.com/apps-script/guides/web#deploying_a_script_as_a_web_app).
Follow the same steps as serving a user interface. When a `GET` request is made
to the script's URL, the text `Hello, world!` returns. In addition to plain
text, the service supports returning ATOM, CSV, iCal, JavaScript, JSON, RSS,
vCard, and XML content.

## Serve RSS feeds

Filter an RSS feed to modify its content. For example, edit an
[XKCD](http://xkcd.com/) feed to include alt text directly in the feed for
better mobile viewing.

    function doGet() {
      var feed = UrlFetchApp.fetch('http://xkcd.com/rss.xml').getContentText();
      feed = feed.replace(
        /(&lt;img.*?alt="(.*?)".*?&gt;)/g,
        '$1' + new Array(10).join('&lt;br /&gt;') + '$2');
      return ContentService.createTextOutput(feed)
        .setMimeType(ContentService.MimeType.RSS);
    }

The code consists of the following components. Use the
[URL Fetch service](https://developers.google.com/apps-script/reference/url-fetch) to fetch the original
XKCD RSS feed. Use a standard JavaScript regular expression to make the
substitutions. Wrap the edited feed in a
[TextOutput](https://developers.google.com/apps-script/reference/content/text-output) object and set the MIME
type to RSS.

To see this in action, publish the script as a web app and allow anonymous
access. Add the URL of the service to your RSS reader or visit it directly in a
web browser.

## Serve JSON from scripts

Use the Content service to serve JSON to other scripts, websites, and services.
The following script implements a service that checks if a calendar slot is
open at a specific time.

    function doGet(request) {
      var events = CalendarApp.getEvents(
        new Date(Number(request.parameters.start) * 1000),
        new Date(Number(request.parameters.end) * 1000));
      var result = {
        available: events.length == 0
      };
      return ContentService.createTextOutput(JSON.stringify(result))
        .setMimeType(ContentService.MimeType.JSON);
    }

Publish this as an anonymous web app. Users can add URL parameters to the end
of the service URL. The `start` and `end` parameters specify a time range in
the standard Unix epoch.

    curl -L URL_OF_YOUR_SCRIPT?start=1325437200&end=1325439000

The service returns JSON that reports if the calendar is open in that range.

    {"available":true}

## Serve JSONP in web pages

With a slight change, your JSON service can become
[JSONP](http://en.wikipedia.org/wiki/JSONP) to be called from JavaScript in a
browser.

    function doGet(request) {
      var events = CalendarApp.getEvents(
        new Date(Number(request.parameters.start) * 1000),
        new Date(Number(request.parameters.end) * 1000));
      var result = {
        available: events.length == 0
      };
      return ContentService.createTextOutput(
        request.parameters.prefix + '(' + JSON.stringify(result) + ')')
        .setMimeType(ContentService.MimeType.JAVASCRIPT);
    }

To call this service from a browser, create a script tag with a `src` attribute
set to the service URL and an additional `prefix` parameter. This is the name
of the function in your client-side JavaScript that is called with the value
returned by the service.

    <script src="URL_OF_YOUR_SCRIPT?start=1325437200&end=1325439000&prefix=alert"></script>

This example shows a message box in the browser with the service output, using
the browser's built-in `alert` function as the prefix. The JavaScript code
returned looks like:

    alert({"available":true})

Be careful when using JSONP. Because anyone can embed the script tag in their
web page, you can be tricked into executing the script when visiting a
malicious website, which can then capture returned data. Ensure JSONP scripts
are read-only and only return non-sensitive information.

## Redirects

For security, content returned by the Content service is redirected to a
one-time URL at `script.googleusercontent.com`. If you use the Content service
to return data to another application, ensure the HTTP client is configured to
follow redirects. For the curl command-line utility, add the flag `-L`. Check
the documentation for your HTTP client for more information.