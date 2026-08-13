# BigQuery Service

Source: https://developers.google.com/apps-script/advanced/bigquery

## Overview

The BigQuery service in Google Apps Script enables developers to manage BigQuery projects, upload data, and execute queries using the Google BigQuery API. "The BigQuery service lets you use the Google BigQuery API in Google Apps Script."

## Key Information

**Service Type:** Advanced service (must be enabled before use)

**API Reference:** Uses the same objects, methods, and parameters as the [BigQuery API v2 reference documentation](https://developers.google.com/bigquery/docs/reference/v2)

## Enabling the Service

The BigQuery service is classified as an advanced service and requires explicit enablement before it can be used in Apps Script projects.

## Sample Code Examples

### Run Query Example

```javascript
/**
 * Runs a BigQuery query and logs the results in a spreadsheet.
 */
function runQuery() {
  // Replace this value with the project ID listed in the Google
  // Cloud Platform project.
  const projectId = "XXXXXXXX";

  const request = {
    // TODO (developer) - Replace query with yours
    query:
      "SELECT refresh_date AS Day, term AS Top_Term, rank " +
      "FROM `bigquery-public-data.google_trends.top_terms` " +
      "WHERE rank = 1 " +
      "AND refresh_date >= DATE_SUB(CURRENT_DATE(), INTERVAL 2 WEEK) " +
      "GROUP BY Day, Top_Term, rank " +
      "ORDER BY Day DESC;",
    useLegacySql: false,
  };
  let queryResults = BigQuery.Jobs.query(request, projectId);
  const jobId = queryResults.jobReference.jobId;

  // Check on status of the Query Job.
  let sleepTimeMs = 500;
  while (!queryResults.jobComplete) {
    Utilities.sleep(sleepTimeMs);
    sleepTimeMs *= 2;
    queryResults = BigQuery.Jobs.getQueryResults(projectId, jobId);
  }

  // Get all the rows of results.
  let rows = queryResults.rows;
  while (queryResults.pageToken) {
    queryResults = BigQuery.Jobs.getQueryResults(projectId, jobId, {
      pageToken: queryResults.pageToken,
    });
    rows = rows.concat(queryResults.rows);
  }

  if (!rows) {
    console.log("No rows returned.");
    return;
  }
  const spreadsheet = SpreadsheetApp.create("BigQuery Results");
  const sheet = spreadsheet.getActiveSheet();

  // Append the headers.
  const headers = queryResults.schema.fields.map((field) => field.name);
  sheet.appendRow(headers);

  // Append the results.
  const data = new Array(rows.length);
  for (let i = 0; i < rows.length; i++) {
    const cols = rows[i].f;
    data[i] = new Array(cols.length);
    for (let j = 0; j < cols.length; j++) {
      data[i][j] = cols[j].v;
    }
  }
  sheet.getRange(2, 1, rows.length, headers.length).setValues(data);

  console.log("Results spreadsheet created: %s", spreadsheet.getUrl());
}
```

### Load CSV Data Example

```javascript
/**
 * Loads a CSV into BigQuery
 */
function loadCsv() {
  // Replace this value with the project ID listed in the Google
  // Cloud Platform project.
  const projectId = "XXXXXXXX";
  // Create a dataset in the BigQuery UI (https://bigquery.cloud.google.com)
  // and enter its ID below.
  const datasetId = "YYYYYYYY";
  // Sample CSV file of Google Trends data conforming to the schema below.
  // https://docs.google.com/file/d/0BwzA1Orbvy5WMXFLaTR1Z1p2UDg/edit
  const csvFileId = "0BwzA1Orbvy5WMXFLaTR1Z1p2UDg";

  // Create the table.
  const tableId = `pets_${new Date().getTime()}`;
  let table = {
    tableReference: {
      projectId: projectId,
      datasetId: datasetId,
      tableId: tableId,
    },
    schema: {
      fields: [
        { name: "week", type: "STRING" },
        { name: "cat", type: "INTEGER" },
        { name: "dog", type: "INTEGER" },
        { name: "bird", type: "INTEGER" },
      ],
    },
  };
  try {
    table = BigQuery.Tables.insert(table, projectId, datasetId);
    console.log("Table created: %s", table.id);
  } catch (err) {
    console.log("unable to create table");
  }
  // Load CSV data from Drive and convert to the correct format for upload.
  const file = DriveApp.getFileById(csvFileId);
  const data = file.getBlob().setContentType("application/octet-stream");

  // Create the data upload job.
  const job = {
    configuration: {
      load: {
        destinationTable: {
          projectId: projectId,
          datasetId: datasetId,
          tableId: tableId,
        },
        skipLeadingRows: 1,
      },
    },
  };
  try {
    const jobResult = BigQuery.Jobs.insert(job, projectId, data);
    console.log(`Load job started. Status: ${jobResult.status.state}`);
  } catch (err) {
    console.log("unable to insert job");
  }
}
```

## Support

For issues and additional support, refer to the [Google Cloud support guide](https://cloud.google.com/support/).
