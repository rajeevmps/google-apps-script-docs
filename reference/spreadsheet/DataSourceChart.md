# DataSourceChart

Access and modify an existing data source chart.

Access and modify an existing data source chart. Only use this class with data that's connected to a BigQuery database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `cancelDataRefresh()` | `DataSourceChart` | Cancels the data refresh associated with this object if it's currently running. Throws an exception if the data source type is not enabled. Use `SpreadsheetApp#enable...Execution()` methods to enable data execution for specific data source type. |
| `forceRefreshData()` | `DataSourceChart` | Refreshes the data of this object regardless of the current state. See `refreshData()` for more details. If you want to cancel a currently running refresh of this object, see `cancelDataRefresh()`. Throws an exception if the data source type is not enabled. |
| `getDataSource()` | `DataSource` | Gets the data source the object is linked to. |
| `getStatus()` | `DataExecutionStatus` | Gets the data execution status of the object. |
| `refreshData()` | `DataSourceChart` | Refreshes the data of the object. Throws an exception if currently in error state. Use `DataSource#updateSpec()` to update the specification. The method is preferred over `forceRefreshData()` to prevent unexpected edits on data source. Throws an exception if the data source type is not enabled. |
| `waitForCompletion(timeoutInSeconds: Integer)` | `DataExecutionStatus` | Waits until the current execution completes, timing out after the provided number of seconds. Throws an exception if the execution is not completed when timing out, but does not cancel the data execution. `timeoutInSeconds` is the time to wait for data execution, in seconds. The maximum is 300 seconds. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Code Samples

```javascript
const spreadsheet = SpreadsheetApp.getActive();
const formula = spreadsheet.getDataSourceFormulas()[0];
// Cancel the ongoing refresh on the formula.
formula.cancelDataRefresh();
```
