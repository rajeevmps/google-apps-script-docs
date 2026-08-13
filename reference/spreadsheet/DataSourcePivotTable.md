# DataSourcePivotTable

Access and modify an existing data source pivot table.

Access and modify existing data source pivot table. To create a new data source pivot table, use `Range.createDataSourcePivotTable(dataSource)`. Only use this class with data that's connected to a database.

Key capabilities include: adding column groups, filters, and pivot values to data source pivot tables; methods available to refresh, force refresh, cancel refresh, and check execution status; conversion to regular pivot table objects via `asPivotTable()`.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `addColumnGroup(columnName: String)` | `PivotGroup` | Adds a new pivot column group based on the specified data source column. |
| `addFilter(columnName: String, filterCriteria: FilterCriteria)` | `PivotFilter` | Adds a new filter based on the specified data source column with the specified filter criteria. |
| `addPivotValue(columnName: String)` | `PivotValue` | Adds a new pivot value based on the specified data source column without any summarize function. For Looker measures only. |
| `addPivotValue(columnName: String, summarizeFunction: PivotTableSummarizeFunction)` | `PivotValue` | Adds a new pivot value based on the specified data source column with the specified summarize function. In order to add pivot values for Looker measures, use addPivotValue(columnName). |
| `addRowGroup(columnName: String)` | `PivotGroup` | Adds a new pivot row group based on the specified data source column. |
| `asPivotTable()` | `PivotTable` | Returns the data source pivot table as a regular pivot table object. |
| `cancelDataRefresh()` | `DataSourcePivotTable` | Cancels the data refresh associated with this object if it's currently running. |
| `forceRefreshData()` | `DataSourcePivotTable` | Refreshes the data of this object regardless of the current state. |
| `getDataSource()` | `DataSource` | Gets the data source the object is linked to. |
| `getStatus()` | `DataExecutionStatus` | Gets the data execution status of the object. |
| `refreshData()` | `DataSourcePivotTable` | Refreshes the data of the object. |
| `waitForCompletion(timeoutInSeconds: Integer)` | `DataExecutionStatus` | Waits until the current execution completes, timing out after the provided number of seconds. |

## Code Samples

```javascript
const spreadsheet = SpreadsheetApp.openById('abcd1234');
const datasource = spreadsheet.getDataSources()[0];
const pivotTable = datasource.createDataSourcePivotTableOnNewSheet();
pivotTable.addPivotValue('columnName');
```
