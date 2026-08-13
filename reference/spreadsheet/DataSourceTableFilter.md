# DataSourceTableFilter

Access and modify an existing data source table filter.

Access and modify an existing data source table filter. To create a new data source table filter, use `DataSourceTable.addFilter(columnName, filterCriteria)`. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getDataSourceColumn()` | `DataSourceColumn` | Returns the data source column this filter applies to. |
| `getDataSourceTable()` | `DataSourceTable` | Returns the `DataSourceTable` that this filter belongs to. |
| `getFilterCriteria()` | `FilterCriteria` | Returns the filter criteria for this filter. |
| `remove()` | `void` | Removes this filter from the data source object. |
| `setFilterCriteria(filterCriteria: FilterCriteria)` | `DataSourceTableFilter` | Sets the filter criteria for this filter. `filterCriteria` is the filter criteria to set. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
