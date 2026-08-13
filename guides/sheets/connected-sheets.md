# Use Connected Sheets

## Page Summary

- Connected Sheets allows you to analyze BigQuery and Looker data directly within Google Sheets and is accessible programmatically using the Spreadsheet service.
- Common actions with Connected Sheets, such as connecting to a data source or adding charts, are performed using specific `DataSource` classes and methods in Apps Script.
- To access BigQuery or Looker data, you must include `enableBigQueryExecution()` or `enableLookerExecution()` respectively in your Apps Script code, which adds the necessary OAuth scopes.
- Data source objects can be added and refreshed asynchronously, with methods available to check the execution status and handle errors.
- Triggers, including time-driven and event triggers, can be used to automate data source functions, such as refreshing data on a schedule or when a parameter is edited.

[Connected Sheets](https://cloud.google.com/blog/products/g-suite/connected-sheets-is-generally-available)
is a Google Sheets feature that lets you analyze BigQuery and Looker
data directly within Sheets. Access
Connected Sheets programmatically with the Spreadsheet service.

## Common Connected Sheets actions

Use the `DataSource` classes and objects to connect to BigQuery or Looker and
analyze data.
The following table lists the most common `DataSource` actions and
how to create them in Google Apps Script:

| Action | Apps Script class | Method to use |
|---|---|---|
| Connect a sheet to a supported data source | [`DataSourceSpec`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec) | `SpreadsheetApp.newDataSourceSpec()` |
| Choose a data source | [`DataSource`](https://developers.google.com/apps-script/reference/spreadsheet/data-source) | `Spreadsheet.insertDataSourceSheet().getDataSource()` |
| Add a data source sheet | [`DataSourceSheet`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-sheet) | `Spreadsheet.insertDataSourceSheet()` |
| Add a pivot table | [`DataSourcePivotTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-pivot-table) | `Range.insertDataSourcePivotTable()` |
| Pull data into an extract | [`DataSourceTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-table) | `Range.insertDataSourceTable()` |
| Use a formula | [`DataSourceFormula`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-formula) | `Range.setFormula()` |
| Add a chart | [`DataSourceChart`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-chart) | `Sheet.insertDataSourceChart()` |

## Add required authorization scopes

To access BigQuery data, include the `enableBigQueryExecution()` method
in your Apps Script code. This method adds the required
`bigquery.readonly` OAuth scope to your Apps Script project.

The following sample shows the `SpreadsheetApp.enableBigQueryExecution()` method
called within a function:

```javascript
function addDataSource() {
  SpreadsheetApp.enableBigQueryExecution();
  var spreadsheet = SpreadsheetApp.getActive();
  }
```

To access Looker data, include the `enableLookerExecution()` method in
your Apps Script code. Accessing Looker in
Apps Script reuses your existing Google Account Link with Looker.

The following sample shows the `SpreadsheetApp.enableLookerExecution()` method
called within a function:

```javascript
function addDataSource() {
  SpreadsheetApp.enableLookerExecution();
  var spreadsheet = SpreadsheetApp.getActive();
  }
```

### Add additional OAuth scopes to the manifest file

When connecting with BigQuery, most OAuth scopes are automatically added to the
manifest file based on the functions used in your code. If you need additional
scopes to access certain BigQuery data, you can
[set explicit scopes](https://developers.google.com/apps-script/concepts/scopes#setting_explicit_scopes).

For example, to [query BigQuery data hosted within
Google Drive](https://cloud.google.com/bigquery/external-data-drive#api),
you must add a Drive OAuth scope to your manifest file.

The following sample shows the `oauthScopes` portion of a manifest file. It adds
a Drive OAuth scope in addition to the minimum required
`spreadsheet` and `bigquery.readonly` OAuth scopes:

```json
{ ...
  "oauthScopes": [
    "https://www.googleapis.com/auth/bigquery.readonly",
    "https://www.googleapis.com/auth/spreadsheets",
    "https://www.googleapis.com/auth/drive" ],
... }
```

## Example: Create and refresh a data source object

The following examples shows how to add a data source, create a data
source object from the data source, refresh the data source object, and get
the execution status.

### Add a data source

The following examples show how to add a BigQuery and a Looker data source
respectively.

#### BigQuery

To add a BigQuery data source to a spreadsheet, insert a data source sheet with
a data source spec. The data source sheet is automatically refreshed to fetch
preview data.

Replace `<YOUR_PROJECT_ID>` below with a valid Google Cloud project ID.

```javascript
// For operations that fetch data from BigQuery, enableBigQueryExecution() must be called.
SpreadsheetApp.enableBigQueryExecution();
var spreadsheet = SpreadsheetApp.create('Test connected sheets');
Logger.log('New test spreadsheet: %s', spreadsheet.getUrl());

// Build data source spec by selecting a table.
var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
    .asBigQuery()
    .setProjectId('<YOUR_PROJECT_ID>')
    .setTableProjectId('bigquery-public-data')
    .setDatasetId('ncaa_basketball')
    .setTableId('mbb_historical_tournament_games')
    .build();
// Add data source and its associated data source sheet.
var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
var dataSource = dataSourceSheet.getDataSource();
```

#### Looker

To add a Looker data source to a spreadsheet, insert a data source sheet with a
data source spec. The data source sheet is automatically refreshed to fetch
preview data.

Replace `<INSTANCE_URL>`,`<MODEL_NAME>`, `<EXPLORE_NAME>` in the following
sample with a valid Looker instance URL, model name and explore name
respectively.

```javascript
// For operations that fetch data from Looker, enableLookerExecution() must be called.
SpreadsheetApp.enableLookerExecution();
var spreadsheet = SpreadsheetApp.create('Test connected sheets');
Logger.log('New test spreadsheet: %s', spreadsheet.getUrl());

// Build data source spec by selecting a table.
var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
    .asLooker()
    .setInstanceUrl('<INSTANCE_URL>')
    .setModelName('<MODEL_NAME>')
    .setExploreName('<EXPLORE_NAME>')
    .build();
// Add data source and its associated data source sheet.
var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
var dataSource = dataSourceSheet.getDataSource();
```

### Add a data source object

Once the data source is added to the spreadsheet, data source objects can be
created from the data source. In this example, a pivot table is created using
 `DataSourcePivotTable` on the BigQuery `dataSource` created in
the code sample which adds a BigQuery data source.

Unlike regular data in grid sheets that are referenced by cell index or A1
notations, data from data sources are usually referenced by column names.
Therefore, most property setters on data source objects use column name as
input.

```javascript
var rootCell = spreadsheet.insertSheet('pivotTableSheet').getRange('A1');

// Add data source pivot table and set data source specific configurations.
var dataSourcePivotTable = rootCell.createDataSourcePivotTable(dataSource);
var rowGroup = dataSourcePivotTable.addRowGroup('season');
rowGroup.sortDescending().setGroupLimit(5);
dataSourcePivotTable.addColumnGroup('win_school_ncaa');
dataSourcePivotTable.addPivotValue('win_pts',
SpreadsheetApp.PivotTableSummarizeFunction.AVERAGE);
dataSourcePivotTable.addPivotValue('game_date',
SpreadsheetApp.PivotTableSummarizeFunction.COUNTA);
var filterCriteria = SpreadsheetApp.newFilterCriteria()
    .whenTextEqualToAny(['Duke', 'North Carolina'])
    .build();
dataSourcePivotTable.addFilter('win_school_ncaa', filterCriteria);

// Get a regular pivot table instance and set shared configurations.
var pivotTable = dataSourcePivotTable.asPivotTable();
pivotTable.setValuesDisplayOrientation(SpreadsheetApp.Dimension.ROWS);
```

### Refresh a data source object

Refresh data source objects to fetch the latest data from BigQuery
based on the data source specs and object configurations.

The process to refresh data is asynchronous. To refresh a data source object,
use the following methods:

1. `refreshData()` starts the data refresh execution.
2. `waitForCompletion()` returns the end state once the data execution is
completed. This eliminates the need to keep polling the execution status.
3. `DataExecutionStatus.getErrorCode()` gets the error code in case the data
execution fails.

The following sample illustrates a refresh of the pivot table data:

```javascript
var status = dataSourcePivotTable.getStatus();
Logger.log('Initial state: %s', status.getExecutionState());

dataSourcePivotTable.refreshData();

status = dataSourcePivotTable.waitForCompletion(/* timeoutInSeconds= */ 60);
Logger.log('Ending state: %s', status.getExecutionState());
if (status.getExecutionState() == SpreadsheetApp.DataExecutionState.ERROR) {
  Logger.log('Error: %s (%s)', status.getErrorCode(),
  status.getErrorMessage());
}
```

## Use triggers with Connected Sheets

Automate your Connected Sheets data source functions with
[triggers and events](https://developers.google.com/apps-script/guides/triggers/installable).
For example, use 
[time-driven triggers](https://developers.google.com/apps-script/guides/triggers/installable#time-driven_triggers)
to refresh data source objects repeatedly at a specific time, and use
spreadsheet
[event triggers](https://developers.google.com/apps-script/guides/triggers/installable#g_suite_application_triggers)
to trigger data execution on a predefined event.

The following sample adds a BigQuery data source with a query parameter and
refreshes the data source sheet when the query parameter is edited.

Replace `<YOUR_PROJECT_ID>` with a valid Google Cloud project ID.

```javascript
// Add data source with query parameter.
function addDataSource() {
  SpreadsheetApp.enableBigQueryExecution();
  var spreadsheet = SpreadsheetApp.getActive();

  // Add a new sheet and use A1 cell as the parameter cell.
  var parameterCell = spreadsheet.insertSheet('parameterSheet').getRange('A1');
  parameterCell.setValue('Duke');

  // Add data source with query parameter.
  var dataSourceSpec = SpreadsheetApp.newDataSourceSpec()
      .asBigQuery()
      .setProjectId('<YOUR_PROJECT_ID>')
      .setRawQuery('select * from `bigquery-public-data`.`ncaa_basketball`.`mbb_historical_tournament_games` WHERE win_school_ncaa = @SCHOOL')
      .setParameterFromCell('SCHOOL', 'parameterSheet!A1')
      .build();
  var dataSourceSheet = spreadsheet.insertDataSourceSheet(dataSourceSpec);
  dataSourceSheet.asSheet().setName('ncaa_data');
}

// Function used to configure event trigger to refresh data source sheet.
function refreshOnParameterEdit(e) {
  var editedRange = e.range;
  if (editedRange.getSheet().getName() != 'parameterSheet') {
    return;
  }
  // Check that the edited range includes A1.
  if (editedRange.getRow() > 1 || editedRange.getColumn() > 1) {
     return;
  }

  var spreadsheet = e.source;
  SpreadsheetApp.enableBigQueryExecution();
  spreadsheet.getSheetByName('ncaa_data').asDataSourceSheet().refreshData();
}
```

In the preceding sample, the `addDataSource()` function adds a data source to
the spreadsheet. After you execute `addDataSource()`, create an event trigger in
the Apps Script editor. To learn how to create an event trigger,
see [Installable triggers](https://developers.google.com/apps-script/guides/triggers/installable).

Select the following options for your trigger:

- **Event source**: **From spreadsheet**
- **Event type**: **On edit**
- **Function to run**: **`refreshOnParameterEdit`**

Once the trigger is created, the data source sheet refreshes automatically
every time the parameter cell is edited.

## Troubleshoot

| Error message | Resolution |
|---|---|
| Use `enableBigQuery()` to enable data executions for BIGQUERY data sources. | This error indicates that `SpreadsheetApp.enableBigQueryExecution()` is not called before fetching BigQuery data. Call `SpreadsheetApp.enableBigQueryExecution()` in functions that use methods for BigQuery execution. Such as, `refreshData()` on data source objects, `Spreadsheet.insertDataSourceTable()` , and `DataSource.updateSpec()` . These methods require an additional bigquery.readonly OAuth scope to work. |
| Not permitted to act on data sources. Please contact your administrator to enable the feature. | This error indicates that the account doesn't have Connected Sheets enabled. Connected Sheets is only available to Google Workspace users with certain subscriptions. Contact your administrator to enable the feature. |
