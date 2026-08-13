# Logging

When developing any kind of app, log information to help diagnose faults during
development, to identify and diagnose customer issues, and for other purposes.

Google Apps Script provides three different mechanisms for logging:

- The built-in [Apps Script execution log](https://developers.google.com/apps-script/guides/logging#execution_log_logging).
  This log is lightweight and streams in real time, but persists only for a
  short time.

- The [Cloud Logging](https://developers.google.com/apps-script/guides/logging#cloud_logging) interface in the Developer Console, which
  provides logs that persist for many days after their creation.

- The [Error Reporting](https://developers.google.com/apps-script/guides/logging#error_reporting) interface in the Developer Console,
  which collects and records errors that occur while your script is running.

These are described in the following sections. In addition to these mechanisms,
build your own logger code that, for example, writes information to a logging
[Spreadsheet](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app) or
[JDBC database](https://developers.google.com/apps-script/guides/jdbc).

## Use the Apps Script execution log

A basic approach to logging in Apps Script is to use the
built-in execution log. To view these logs, at the top of the editor, click
**Execution log**. When you run a function or use the debugger, the logs
stream in real time.

Use either the [`Logger`](https://developers.google.com/apps-script/reference/base/logger) or
[`console`](https://developers.google.com/apps-script/reference/base/console) logging services in the
built-in execution log.

These logs are intended for checks during development and debugging,
and don't persist very long.

For example, consider this function:
utils/logging.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/utils/logging.gs)

```javascript
/**
 * Logs Google Sheet information.
 * @param {number} rowNumber The spreadsheet row number.
 * @param {string} email The email to send with the row data.
 */
function emailDataRow(rowNumber, email) {
  console.log(`Emailing data row ${rowNumber} to ${email}`);
  const sheet = SpreadsheetApp.getActiveSheet();
  const data = sheet.getDataRange().getValues();
  const rowData = data[rowNumber - 1].join(" ");
  console.log(`Row ${rowNumber} data: ${rowData}`);
  MailApp.sendEmail(email, `Data in row ${rowNumber}`, rowData);
}
```

When this script runs with inputs "2" and "john@example.com" the following logs
are written:

    > [16-09-12 13:50:42:193 PDT] Emailing data row 2 to john@example.com
    > [16-09-12 13:50:42:271 PDT] Row 2 data: Cost 103.24

## Cloud Logging

Apps Script also provides partial access to the Google Cloud
[Cloud Logging](https://cloud.google.com/logging/docs/) service. When you require
logging that persists for several days, or need a more complex logging solution
for a multi-user production environment, Cloud Logging is the preferred choice.
See [Cloud Logging quotas and limits](https://cloud.google.com/logging/quotas)
for data retention and other quota details.

To request more logging quota,
[submit a Google Cloud quota request](https://cloud.google.com/docs/quota#requesting_higher_quota).
This requires that you have access to the
[Cloud Platform project](https://developers.google.com/apps-script/guides/cloud-platform-projects) that your
script uses.

Cloud Logging provides a number of services beyond storing logs, such as alerts
and metrics. These services aren't available from
Apps Script.

### Use Cloud Logging

Cloud logs are attached to the [Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects)
associated with your Apps Script. View a simplified version of
these logs in the [Apps Script dashboard](https://script.google.com/home/executions).

To make full use of Cloud Logging and its capabilities, use a
[standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects)
with your script project. This lets you access Cloud logs directly in the
[Google Cloud console](https://developers.google.com/apps-script/guides/cloud-platform-projects#viewing_cloud_logs_and_error_reports_in_the_google_cloud_platform_console)
and gives you more viewing and filtering options.

If you use the Rhino runtime, Cloud Logging doesn't support the Apps Script
[`Logger`](https://developers.google.com/apps-script/reference/base/logger) service. Instead, use the
[`console`](https://developers.google.com/apps-script/reference/base/console) service.

When logging, it is good privacy practice to avoid recording any personal
information about the user, such as email addresses. Cloud logs are
automatically labeled with
[active user keys](https://developers.google.com/apps-script/guides/logging#active_user_keys) to locate a
specific user's log messages when necessary.

Log strings, formatted strings, and even JSON objects using the functions
provided by the Apps Script
[`console`](https://developers.google.com/apps-script/reference/base/console) service.

The following example shows how to use the
[`console`](https://developers.google.com/apps-script/reference/base/console) service to log information in
Cloud Operations.
utils/logging.gs [View on GitHub](https://github.com/googleworkspace/apps-script-samples/blob/main/utils/logging.gs)

```javascript
/**
 * A placeholder function to be timed.
 * @param {Object} parameters
 */
function myFunction(parameters) {
  // Placeholder for the function being timed.
}

/**
 * Logs the time taken to execute 'myFunction'.
 */
function measuringExecutionTime() {
  // A simple INFO log message, using sprintf() formatting.
  console.info("Timing the %s function (%d arguments)", "myFunction", 1);

  // Log a JSON object at a DEBUG level. The log is labeled
  // with the message string in the log viewer, and the JSON content
  // is displayed in the expanded log structure under "jsonPayload".
  const parameters = {
    isValid: true,
    content: "some string",
    timestamp: new Date(),
  };
  console.log({ message: "Function Input", initialData: parameters });
  const label = "myFunction() time"; // Labels the timing log entry.
  console.time(label); // Starts the timer.
  try {
    myFunction(parameters); // Function to time.
  } catch (e) {
    // Logs an ERROR message.
    console.error(`myFunction() yielded an error: ${e}`);
  }
  console.timeEnd(label); // Stops the timer, logs execution duration.
}
```

### Active user keys

Temporary active user keys provide a convenient way to spot unique users in
Cloud Log entries without revealing the identities of those users. Keys are per
script and change roughly once a month to provide additional security should a
user reveal their identity to a developer, for example while reporting an issue.

Temporary active user keys are superior to logging identifiers like email
addresses because:

- You don't have to add anything to your logging; they're already there!
- They don't require user authorization.
- They protect user privacy.

To find temporary active user keys in your Cloud Log entries,
[view your Cloud logs in the Google Cloud console](https://developers.google.com/apps-script/guides/cloud-platform-projects#viewing_cloud_logs_and_error_reports_in_the_google_cloud_platform_console).
Do this only if your script project is using a
[standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects)
that you have access to. Once you've opened the Google Cloud project in the console,
select a log entry of interest and expand it to view
**metadata \> labels \> script.googleapis.com/user_key**.

To get the temporary active user key, call
[`Session.getTemporaryActiveUserKey`](https://developers.google.com/apps-script/reference/base/session#getTemporaryActiveUserKey())
in your script. One way to use this method is to display the key to the user
while they are running your script. Then users may choose to include their keys
when reporting issues to help you identify the relevant logs.

### Exception logging

Exception logging sends unhandled exceptions in your script project code to
Cloud Logging, along with a stack trace.

To view exception logs, follow these steps:

1. Open the Apps Script project.
2. At the left, click **Executions** .
3. At the top, click **Add a filter \> Status**.
4. Select the **Failed** and **Timed out** checkboxes.

View logged exceptions in the
[Google Cloud console](https://developers.google.com/apps-script/guides/cloud-platform-projects#viewing_cloud_logs_and_error_reports_in_the_google_cloud_platform_console)
if your script project is using a
[standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects)
that you have access to.

#### Enable exception logging

Exception logging is enabled by default for new projects. To enable exception
logging for older projects, follow these steps:

1. Open the script project.
2. At the left, click **Project Settings** .
3. Select the **Log uncaught exceptions to Cloud Operations** checkbox.

## Error Reporting

Exception logging automatically integrates with [Cloud Error
Reporting](https://cloud.google.com/error-reporting/docs/), a service that
aggregates and displays errors produced in your script. View your Cloud error
reports in the Google Cloud console. You don't need to manually configure Error
Reporting or create trace entries. Apps Script automatically
populates the required fields when an exception is thrown or when you use
`console.error` with an `Error` object. If you are prompted to "Set up Error
Reporting" this is because your script has not yet logged any exceptions. No
setup is required beyond [enabling exception logging](https://developers.google.com/apps-script/guides/logging#exception_logging).

## Logging requirements

There are no requirements for using the built-in execution log.

View a simplified version of Cloud logs in the
[Apps Script dashboard](https://script.google.com/home/executions). However,
to make the most of Cloud Logging and error reporting you must have access to
the Google Cloud project of the script. This is only possible if your script
project is using a [standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects).