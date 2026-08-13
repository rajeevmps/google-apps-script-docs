# DataSourceSheet

Access and modify an existing data source sheet.

Access and modify existing data source sheet. To create a new data source sheet, use `Spreadsheet.insertDataSourceSheet(spec)`. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `addFilter(columnName: String, filterCriteria: FilterCriteria)` | `DataSourceSheet` | Adds a filter applied to the data source sheet. `columnName` is the name of the column to apply this filter to; `filterCriteria` is the filter criteria to apply. Returns the data source sheet, for method chaining. |
| `asSheet()` | `Sheet` | Returns the data source sheet as a regular sheet object. |
| `autoResizeColumn(columnName: String)` | `DataSourceSheet` | Auto resizes the width of the specified column. Returns this data source sheet, for chaining. |
| `autoResizeColumns(columnNames: String[])` | `DataSourceSheet` | Auto resizes the width of the specified columns. `columnNames` is the list of column names to update. Returns this data source sheet, for chaining. |
| `cancelDataRefresh()` | `DataSourceSheet` | Cancels the data refresh associated with this object if it's currently running. Throws an exception if the data source type is not enabled. |
| `forceRefreshData()` | `DataSourceSheet` | Refreshes the data of this object regardless of the current state. See `refreshData()` for more details. Throws an exception if the data source type is not enabled. |
| `getColumnWidth(columnName: String)` | `Integer\|null` | Returns the width of the specified column. Returns the column's width, or `null` if the column uses the default width. |
| `getDataSource()` | `DataSource` | Gets the data source the object is linked to. |
| `getFilters()` | `DataSourceSheetFilter[]` | Returns all filters applied to the data source sheet. |
| `getSheetValues(columnName: String)` | `Object[]` | Returns all the values for the data source sheet for the provided column name. Returns a one-dimensional array of values. |
| `getSheetValues(columnName: String, startRow: Integer, numRows: Integer)` | `Object[]` | Returns all the values for the data source sheet for the provided column name from the provided start row (based-1) and up to the provided `numRows`. Returns a one-dimensional array of values. |
| `getSortSpecs()` | `SortSpec[]` | Gets all the sort specs in the data source sheet. Returns a list of sort specs. |
| `getStatus()` | `DataExecutionStatus` | Gets the data execution status of the object. |
| `refreshData()` | `DataSourceSheet` | Refreshes the data of the object. Throws an exception if currently in error state. Use `DataSource#updateSpec()` to update specification. |
| `removeFilters(columnName: String)` | `DataSourceSheet` | Removes all filters applied to the data source sheet column. `columnName` is the name of the column to remove filters from. Returns the data source sheet, for method chaining. |
| `removeSortSpec(columnName: String)` | `DataSourceSheet` | Removes the sort spec on a column in the data source sheet. `columnName` is the name of the column. Returns the data source sheet, for chaining. |
| `setColumnWidth(columnName: String, width: Integer)` | `DataSourceSheet` | Sets the width of the specified column. Returns this data source sheet, for chaining. |
| `setColumnWidths(columnNames: String[], width: Integer)` | `DataSourceSheet` | Sets the width of the specified columns. `columnNames` is the list of column names to update; `width` is the new width for the columns. Returns this data source sheet, for chaining. |
| `setSortSpec(columnName: String, ascending: Boolean)` | `DataSourceSheet` | Sets the sort spec on a column in the data source sheet. `columnName` is the name of the column to sort; `ascending` — if true, sort ascending; if false, sort descending. Returns the data source sheet, for chaining. |
| `setSortSpec(columnName: String, sortOrder: SortOrder)` | `DataSourceSheet` | Sets the sort spec on a column in the data source sheet. `columnName` is the name of the column to sort; `sortOrder` is the sort order. Returns the data source sheet, for chaining. |
| `waitForCompletion(timeoutInSeconds: Integer)` | `DataExecutionStatus` | Waits until the current execution completes, timing out after the provided number of seconds. Throws an exception if execution is not completed when timing out, but does not cancel data execution. `timeoutInSeconds` is the time to wait for data execution, in seconds (maximum 300 seconds). |

## Code Samples

```javascript
const spreadsheet = SpreadsheetApp.getActive();
const formula = spreadsheet.getDataSourceFormulas()[0];
formula.cancelDataRefresh();
```
