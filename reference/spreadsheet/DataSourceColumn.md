# DataSourceColumn

Access and modify a data source column.

Access and modify a data source column. Only use this class with data that's connected to a database.

The DataSourceColumn class enables developers to retrieve associated data source, formula, and column name information; determine if a column has array dependencies or is calculated; and modify calculated columns by removing them or updating formulas and names.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getDataSource()` | `DataSource` | Gets the data source associated with the data source column. |
| `getFormula()` | `String` | Gets the formula for the data source column. Returns an empty string if the data source column is not a calculated column. |
| `getName()` | `String` | Gets the name for the data source column. |
| `hasArrayDependency()` | `Boolean` | Returns whether the column has an array dependency. |
| `isCalculatedColumn()` | `Boolean` | Returns whether the column is a calculated column. |
| `remove()` | `void` | Removes the data source column. Only supported for calculated columns. |
| `setFormula(formula: String)` | `DataSourceColumn` | Sets the formula for the data source column. Only supported for calculated columns. |
| `setName(name: String)` | `DataSourceColumn` | Sets the name of the data source column. Only supported for calculated columns. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
