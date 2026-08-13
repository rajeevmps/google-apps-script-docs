# DataSourceTableColumn

Access and modify an existing column in a DataSourceTable.

Access and modify an existing column in a DataSourceTable. To add columns to a data source table, use `DataSourceTable.addColumns(columnNames)`. Important restriction: only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getDataSourceColumn()` | `DataSourceColumn` | Gets the data source column. |
| `remove()` | `void` | Removes the column from the DataSourceTable. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
