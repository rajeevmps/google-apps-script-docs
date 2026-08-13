# Logger

This class allows the developer to write to the Execution log and to Google Cloud Logging.

This class allows the developer to write to the Execution log and to Google Cloud Logging if the script is associated with a standard Cloud Project. This class is preferred for structured logging and jsonPayload support in Cloud Logging. For time-based logging, use console.

## Methods

### clear() → void

Clears the log.

### getLog() → String

Returns a complete list of messages in the current log. This method can be used to save or email the entire log output generated during script execution.

**Return:** the log from the logging console

**Code Sample:**
```javascript
const files = DriveApp.getFiles();
while (files.hasNext()) {
  Logger.log(files.next().getName());
}
const recipient = Session.getActiveUser().getEmail();
const subject = 'A list of files in your Google Drive';
const body = Logger.getLog();
MailApp.sendEmail(recipient, subject, body);
```

### log(data: Object) → Logger

Writes the data to the log. The data can be a string, a JavaScript object, or an object with a message property.

**Return:** the Logger, for chaining.

**Code Sample:**
```javascript
Logger.log("my log message");
Logger.log({ key: "value" });
Logger.log({ message: "my log message", data: { key: "value" } })
```

### log(format: String, values: Object...) → Logger

Writes a formatted string to the logging console, using the format and values provided. The string can include multiple %s placeholders, which are replaced with corresponding values from the list of arguments, converted to strings.

**Parameters:**
- `format` (String): a format string that contains as many instances of %s as the number of values arguments
- `values` (Object...): a variable number of values to insert into the format string

**Return:** the Logger, for chaining

**Code Sample:**
```javascript
const groups = GroupsApp.getGroups();
Logger.log('You are a member of %s Google Groups.', groups.length);
```
