# DataSourceFormula

Access and modify existing data source formulas.

Access and modify existing data source formulas. To create a new data source formula, use `Range.setFormula(formula)`. Only use this class with data that's connected to a BigQuery database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `cancelDataRefresh()` | `DataSourceFormula` | Cancels the data refresh associated with this object if it's currently running. Throws an exception if the data source type is not enabled. Use `SpreadsheetApp#enable...Execution()` methods to enable data execution for specific data source type. |
| `forceRefreshData()` | `DataSourceFormula` | Refreshes the data of this object regardless of the current state. See `refreshData()` for more details and `cancelDataRefresh()` to cancel currently running refresh operations. Throws exception if data source type is not enabled. |
| `getAnchorCell()` | `Range` | Returns the `Range` representing the cell where this data source formula is anchored. |
| `getDataSource()` | `DataSource` | Gets the data source the object is linked to. |
| `getDisplayValue()` | `String` | Returns the display value of the data source formula. |
| `getFormula()` | `String` | Returns the formula for this data source formula. |
| `getStatus()` | `DataExecutionStatus` | Gets the data execution status of the object. |
| `refreshData()` | `DataSourceFormula` | Refreshes the data of the object. Throws an exception if currently in `error` state. Use `DataSource#updateSpec()` to update the specification. The method is preferred over `forceRefreshData()` to prevent unexpected edits on data source. Throws exception if data source type is not enabled. |
| `setFormula(formula: String)` | `DataSourceFormula` | Updates the formula. `formula` is the new formula. |
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
