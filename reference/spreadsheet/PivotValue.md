# PivotValue

Access and modify value groups in pivot tables.

Access and modify value groups in pivot tables.

## Methods

### `getDisplayType()`

Returns the display type describing how this pivot value is currently displayed in the table.

**Returns:** PivotValueDisplayType — the display type for this pivot value

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getFormula()`

Returns the formula used to calculate this value. If this value is not a calculated field this
method returns null .

**Returns:** String — the pivot value for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getPivotTable()`

Returns the PivotTable which this value belongs to.

**Returns:** PivotTable — the pivot table this value belongs to

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataColumn()`

Returns the number of the source data column the pivot value summarizes. This index is 1-based,
if this group summarizes source data in column "A" of the spreadsheet this method returns 1 .

**Returns:** Integer — The source data column number.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataSourceColumn()`

Returns the data source column the pivot value summarizes. Returns null if the pivot
table is not a {DataSourcePivotTableApi}.

**Returns:** DataSourceColumn |null — The source data source column the pivot value summarizes.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSummarizedBy()`

Returns this group’s summarization function.

**Returns:** PivotTableSummarizeFunction — the group's summarization function

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Remove this value from the pivot table.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setDisplayName(name)`

Sets the display name for this value in the pivot table.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The display name to set. |

**Returns:** PivotValue — the pivot value for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setFormula(formula)`

Sets the formula used to calculate this value. If this value is not a calculated field this
method results in an error.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| formula | String | The formula to use to calculate this value. |

**Returns:** PivotValue — the pivot value for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `showAs(displayType)`

Displays this value in the pivot table as a function of another value.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| display Type | Pivot Value Display Type | The way to display the values. |

**Returns:** PivotValue — the pivot value for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `summarizeBy(summarizeFunction)`

Sets the summarization function.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| summarize Function | Pivot Table Summarize Function | The function to use to summarize data in this value's source data
    column. |

**Returns:** PivotValue — the pivot value for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

