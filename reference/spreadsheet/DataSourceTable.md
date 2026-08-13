# DataSourceTable

Access and modify an existing data source table.

Access and modify existing data source table. To create a new data source table on a new sheet, use `Spreadsheet.insertSheetWithDataSourceTable(spec)`. Important limitation: only use this class with BigQuery data sources.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `addColumns(columnNames: String[])` | `DataSourceTable` | Adds columns to the data source table. `columnNames` is the list of the names of the columns to add. |
| `addFilter(columnName: String, filterCriteria: FilterCriteria)` | `DataSourceTable` | Adds a filter applied to the data source table. `columnName` is the name of the column to apply this filter to; `filterCriteria` is the filter criteria to apply. |
| `addSortSpec(columnName: String, ascending: Boolean)` | `DataSourceTable` | Adds a sort spec on a column in the data source table. `columnName` is the name of the column to sort; `ascending` — if `true`, sort the column in ascending order; if `false`, sort the column in descending order. |
| `addSortSpec(columnName: String, sortOrder: SortOrder)` | `DataSourceTable` | Adds a sort spec on a column in the data source table. `columnName` is the name of the column to sort; `sortOrder` is the sort order. |
| `cancelDataRefresh()` | `DataSourceTable` | Cancels the data refresh associated with this object if it's currently running. |
| `forceRefreshData()` | `DataSourceTable` | Refreshes the data of this object regardless of the current state. See `refreshData()` for more details. If you want to cancel a currently running refresh of this object, see `cancelDataRefresh()`. |
| `getColumns()` | `DataSourceTableColumn[]` | Gets all the data source columns added to the data source table. |
| `getDataSource()` | `DataSource` | Gets the data source the object is linked to. |
| `getFilters()` | `DataSourceTableFilter[]` | Returns all filters applied to the data source table. |
| `getRange()` | `Range` | Gets the `Range` this data source table spans. |
| `getRowLimit()` | `Integer\|null` | Returns the row limit for the data source table, or `null` if no limit is set and the table uses the default max limit as in Google Sheets UI. |
| `getSortSpecs()` | `SortSpec[]` | Gets all the sort specs in the data source table. |
| `getStatus()` | `DataExecutionStatus` | Gets the data execution status of the object. |
| `isSyncingAllColumns()` | `Boolean` | Returns whether the data source table is syncing all columns in the associated data source. |
| `refreshData()` | `DataSourceTable` | Refreshes the data of the object. Throws an exception if currently in `error` state. Use `DataSource#updateSpec()` to update the specification. |
| `removeAllColumns()` | `DataSourceTable` | Removes all the columns in the data source table. |
| `removeAllSortSpecs()` | `DataSourceTable` | Removes all the sort specs in the data source table. |
| `setRowLimit(rowLimit: Integer)` | `DataSourceTable` | Updates the row limit for the data source table. If the provided row limit is `null`, then updates the data source table to use the default max row limit as in Google Sheets UI. `rowLimit` is the new row limit for the data table. If `null`, updates the table to use the default row limit. |
| `syncAllColumns()` | `DataSourceTable` | Sync all current and future columns in the associated data source to the data source table. |
| `waitForCompletion(timeoutInSeconds: Integer)` | `DataExecutionStatus` | Waits until the current execution completes, timing out after the provided number of seconds. Throws an exception if the execution is not completed when timing out, but does not cancel the data execution. `timeoutInSeconds` is the time to wait for data execution, in seconds. The maximum is 300 seconds. |

## Code Samples

```javascript
SpreadsheetApp.enableBigQueryExecution();
const spreadsheet = SpreadsheetApp.getActive();
const spec = SpreadsheetApp.newDataSourceSpec()
                 .asBigQuery()
                 .setProjectId('big_query_project')
                 .setRawQuery('select @FIELD from table limit @LIMIT')
                 .setParameterFromCell('FIELD', 'Sheet1!A1')
                 .setParameterFromCell('LIMIT', 'namedRangeCell')
                 .build();
const dataSheet = spreadsheet.insertSheetWithDataSourceTable(spec);
const dataSourceTable = dataSheet.getDataSourceTables()[0];
dataSourceTable.waitForCompletion(60);
Logger.log(
    'Data execution state: %s.',
    dataSourceTable.getStatus().getExecutionState(),
);
```

```javascript
SpreadsheetApp.enableBigQueryExecution();
const dataSheet = SpreadsheetApp.getActive().getSheetByName('Data Sheet 1');
const dataSourceTable = dataSheet.getDataSourceTables()[0];
const dataSource = dataSourceTable.getDataSource();
const newSpec = dataSource.getSpec()
                    .copy()
                    .asBigQuery()
                    .setRawQuery('select name from table limit 2')
                    .removeAllParameters()
                    .build();
dataSource.updateSpec(newSpec);
Logger.log(
    'Data execution state: %s.',
    dataSourceTable.getStatus().getExecutionState(),
);
dataSourceTable.waitForCompletion(60);
Logger.log(
    'Data execution state: %s.',
    dataSourceTable.getStatus().getExecutionState(),
);
```
