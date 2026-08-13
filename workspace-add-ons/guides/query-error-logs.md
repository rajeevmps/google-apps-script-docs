# Query error logs for Google Workspace add-ons

When a published Google Workspace add-on returns an error, the add-on interface returns a generic message of "Something went wrong when executing the add-on." However, these errors are logged to Cloud Logs Explorer.

**Note:** For Apps Script, if your add-on is deployed as a test, then errors are reported in both the Cloud Logs Explorer and in the add-on interface.

For example, an add-on test deployment might display an error message like this in its interface: `TypeError: card.INVALIDFUNCTIONNAME is not a function [line: 33, function: getContextualAddOn, file: GetContextualAddOn]`.

Although error messages like this are helpful, additional information is available in the Logs Explorer. As a best practice, query the error logs for more information. For further information about testing add-on deployments, refer to Test and debug Google Workspace add-ons.

This guide describes how to query add-on error logs in Cloud Logs Explorer, so you can:

*   Learn if users encounter errors.
*   See how often errors occur, and which are most frequent.
*   Read descriptive error messages that help you fix them.

## Prerequisites

Before querying add-on error logs:

*   Enable the "Cloud Logging API" in the add-on's Google Cloud project. To enable an API, refer to Create a Cloud project and enable the API.
*   Publish the add-on on Google Workspace Marketplace. To publish an add-on on the Marketplace, refer to Publish an app.

## Query add-on error logs

To get logs for an add-on:

1.  Open the Google Cloud console.
2.  Next to "Google Cloud Platform," click the Down arrow arrow_drop_down and select the add-on project.
3.  In the top-left corner, click Menu menu > **Logging**. The Logs Explorer opens.
4.  For add-on error logs, in the query builder, enter the following query:

    ```
    severity>=ERROR
        protoPayload.serviceName="gsuiteaddons.googleapis.com"
    ```

5.  To see recent errors, click **Run query**. Or, to see errors as they occur, click **Stream logs**. Add-ons error logs appear in the "Query results" pane.

For further information about Cloud Logs Explorer and writing queries, refer to the following:

*   Use the Logs Explorer
*   Build queries

## Enable or disable error logging

By default, error logging is enabled. When error logging is enabled, the manifest file has the following:

```
"exceptionLogging": "STACKDRIVER",
```

To disable error logging, replace `"exceptionLogging": "STACKDRIVER",` with the following line in the manifest file:

```
// Disable error logging
    "exceptionLogging": "NONE"
```

To re-enable error logging, replace `"exceptionLogging": "NONE"` with `"exceptionLogging": "STACKDRIVER",`.

## Considerations

As you work with add-on error logs in Cloud Logs Explorer, take note of these considerations:

*   Add-ons only log errors in Logs Explorer. Other log types are not recorded.
*   Error messages are always written in English.
*   Cloud Logging incurs a cost. For further information about Cloud Logging pricing, refer to Google Cloud Observability pricing.
