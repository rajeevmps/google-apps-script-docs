# DataSource

Access and modify an existing data source.

Access and modify existing data source. To create a data source table with new data source, see `DataSourceTable`. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `cancelAllLinkedDataSourceObjectRefreshes()` | `void` | Cancels all currently running refreshes of data source objects linked to this data source. |
| `createCalculatedColumn(name: String, formula: String)` | `DataSourceColumn` | Creates a calculated column. This method is only available for BigQuery data sources. |
| `createDataSourcePivotTableOnNewSheet()` | `DataSourcePivotTable` | Creates a data source pivot table from this data source in the first cell of a new sheet. As a side effect, makes the new sheet the active sheet. |
| `createDataSourceTableOnNewSheet()` | `DataSourceTable` | Creates a data source table from this data source in the first cell of a new sheet. As a side effect, makes the new sheet the active sheet. This method is only available for BigQuery data sources. |
| `getCalculatedColumnByName(columnName: String)` | `DataSourceColumn\|null` | Returns the calculated column in the data source that matches the column name. |
| `getCalculatedColumns()` | `DataSourceColumn[]` | Returns all the calculated columns in the data source. Data source specs of `DataSourceType.LOOKER` type returns an empty array. |
| `getColumns()` | `DataSourceColumn[]` | Returns all the columns in the data source. |
| `getDataSourceSheets()` | `DataSourceSheet[]` | Returns the data source sheets associated with this data source. |
| `getSpec()` | `DataSourceSpec` | Gets the data source specification. |
| `refreshAllLinkedDataSourceObjects()` | `void` | Refreshes all data source objects linked to the data source. |
| `updateSpec(spec: DataSourceSpec)` | `DataSource` | Updates the data source specification and refreshes the data source objects linked with this data source with the new specification. |
| `updateSpec(spec: DataSourceSpec, refreshAllLinkedObjects: Boolean)` | `DataSource` | Updates the data source specification and refreshes the linked data source sheets with the new specification. |
| `waitForAllDataExecutionsCompletion(timeoutInSeconds: Integer)` | `void` | Waits until all the current executions of the linked data source objects complete, timing out after the provided number of seconds. |

## Code Samples

```javascript
SpreadsheetApp.enableBigQueryExecution();
const spreadsheet = SpreadsheetApp.getActiveSpreadsheet();
const dataSource = spreadsheet.getDataSources()[0];
dataSource.cancelAllLinkedDataSourceObjectRefreshes();
```
