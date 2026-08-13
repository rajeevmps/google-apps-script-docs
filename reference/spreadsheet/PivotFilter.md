# PivotFilter

Access and modify pivot table filters.

Access and modify pivot table filters.

## Methods

### `getFilterCriteria()`

Returns the filter criteria for this pivot filter.

**Returns:** FilterCriteria — The filter criteria for this pivot filter.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getPivotTable()`

Returns the PivotTable that this filter belongs to.

**Returns:** PivotTable — The pivot table this filter belongs to.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataColumn()`

Returns the number of the source data column this filter operates on. These indices are
1-based, for example if this filter applies to data in column A of the spreadsheet this method
returns "1."

**Returns:** Integer — The number of the source data column this filter applies to.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataSourceColumn()`

Returns the data source column the filter operates on. Returns null if the pivot table
is not a {DataSourcePivotTableApi}.

**Returns:** DataSourceColumn |null — The data source column the filter operates on.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Removes this pivot filter from the pivot table.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setFilterCriteria(filterCriteria)`

Sets the filter criteria for this pivot filter.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| filter Criteria | Filter Criteria | The filter criteria to set. |

**Returns:** PivotFilter — The pivot filter for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

