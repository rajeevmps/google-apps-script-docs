# DoubleClick Bid Manager Service

Source: https://developers.google.com/apps-script/advanced/doubleclick-bidmanager

Note: The slug `dbm` returned a 404. The live page is served at the `doubleclick-bidmanager` slug; content below was fetched from that URL.

## Overview

"The DoubleClick Bid Manager service lets you use the [DV360 Bid Manager API](https://developers.google.com/bid-manager) in Google Apps Script. This API provides programmatic access to DoubleClick Bid Manager (DBM) Reporting."

This advanced service must be enabled before use and utilizes the same objects, methods, and parameters as the public DBM Reporting API.

## Reference Documentation

For detailed information, refer to the [DBM Reporting API reference documentation](https://developers.google.com/bid-manager/reference/rest). The service follows the same method signature patterns as other advanced services in Apps Script.

For support issues, consult the [DBM Reporting and Trafficking support guide](https://developers.google.com/bid-manager/support).

## Code Samples

The following samples use API version 2:

### List Queries

```javascript
/**
 * Logs all of the queries available in the account.
 */
function listQueries() {
  try {
    const queries = DoubleClickBidManager.Queries.list();
    if (queries.queries) {
      for (let i = 0; i < queries.queries.length; i++) {
        const query = queries.queries[i];
        console.log(
          'Found query with ID %s and name "%s".',
          query.queryId,
          query.metadata.title,
        );
      }
    }
  } catch (e) {
    console.log("Failed with error: %s", e.error);
  }
}
```

### Create and Run Query

```javascript
/**
 * Create and run a new DBM Query
 */
function createAndRunQuery() {
  let result;
  let execution;
  const defaultDateRange = {};
  const partnerId = "1234567";
  const query = {
    metadata: {
      title: "Apps Script Example Report",
      dataRange: {
        range: "YEAR_TO_DATE",
      },
      format: "CSV",
    },
    params: {
      type: "STANDARD",
      groupBys: [
        "FILTER_PARTNER",
        "FILTER_PARTNER_NAME",
        "FILTER_ADVERTISER",
        "FILTER_ADVERTISER_NAME",
      ],
      filters: [{ type: "FILTER_PARTNER", value: partnerId }],
      metrics: ["METRIC_IMPRESSIONS"],
    },
    schedule: {
      frequency: "ONE_TIME",
    },
  };

  try {
    result = DoubleClickBidManager.Queries.create(query);
    if (result.queryId) {
      console.log(
        'Created query with ID %s and name "%s".',
        result.queryId,
        result.metadata.title,
      );
      execution = DoubleClickBidManager.Queries.run(
        defaultDateRange,
        result.queryId,
      );
      if (execution.key) {
        console.log(
          'Created query report with query ID %s and report ID "%s".',
          execution.key.queryId,
          execution.key.reportId,
        );
      }
    }
  } catch (e) {
    console.log(e);
    console.log("Failed with error: %s", e.error);
  }
}
```

### Fetch Most Recent Report

```javascript
/**
 * Fetches a report file
 */
function fetchReport() {
  const queryId = "1234567";
  const orderBy = "key.reportId desc";

  try {
    const report = DoubleClickBidManager.Queries.Reports.list(queryId, {
      orderBy: orderBy,
    });
    if (report.reports) {
      const firstReport = report.reports[0];
      if (firstReport.metadata.status.state === "DONE") {
        const reportFile = UrlFetchApp.fetch(
          firstReport.metadata.googleCloudStoragePath,
        );
        console.log("Printing report content to log...");
        console.log(reportFile.getContentText());
      } else {
        console.log(
          "Report status is %s, and is not available for download",
          firstReport.metadata.status.state,
        );
      }
    }
  } catch (e) {
    console.log(e);
    console.log("Failed with error: %s", e.error);
  }
}
```
