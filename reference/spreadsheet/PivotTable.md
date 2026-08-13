# PivotTable

Access and modify pivot tables.

Access and modify pivot tables.

## Methods

### `addCalculatedPivotValue(name, formula)`

Creates a new pivot value in the pivot table calculated from the specified formula with
the specified name .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| name | String | The name for this calculated pivot value. |
| formula | String | The formula used to calculate this value. |

**Returns:** PivotValue — the newly created PivotValue

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addColumnGroup(sourceDataColumn)`

Defines a new pivot column grouping in the pivot table. The specified sourceDataColumn indicates the column in the source data this grouping is based on.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| source Data Column | Integer | The number of the column this group summarizes. This index represents
    the absolute number of the column in the spreadsheet; 1 representing column "A," 2 representing column B, etc. |

**Returns:** PivotGroup — the newly created PivotGroup

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addFilter(sourceDataColumn, filterCriteria)`

Creates a new pivot filter for the pivot table. The specified sourceDataColumn indicates the column in the source data this filter operates on.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| source Data Column | Integer | The number of the column this group summarizes. This index represents
    the absolute number of the column in the spreadsheet; 1 representing column "A," 2 representing column B, etc. |
| filter Criteria | Filter Criteria | The filter criteria used to perform the filtering. |

**Returns:** PivotFilter — the newly created PivotFilter

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addPivotValue(sourceDataColumn, summarizeFunction)`

Defines a new pivot value in the pivot table with the specified summarizeFunction . The
specified sourceDataColumn indicates the column in the source data this value is based
on.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| source Data Column | Integer | The number of the column this group summarizes. This index represents
    the absolute number of the column in the spreadsheet; 1 representing column "A," 2 representing column B, etc. |
| summarize Function | Pivot Table Summarize Function |  |

**Returns:** PivotValue — the newly created PivotValue

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `addRowGroup(sourceDataColumn)`

Defines a new pivot row grouping in the pivot table. The specified sourceDataColumn indicates the column in the source data this grouping is based on.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| source Data Column | Integer | The number of the column this group summarizes. This index represents
    the absolute number of the column in the spreadsheet; 1 representing column "A," 2 representing column B, etc. |

**Returns:** PivotGroup — the newly created PivotGroup

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `asDataSourcePivotTable()`

Returns the pivot table as a data source pivot table if the pivot table is linked to a DataSource , or null otherwise.

**Returns:** DataSourcePivotTable |null — A data source pivot table.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getAnchorCell()`

Returns the Range representing the cell where this pivot table is anchored.

**Returns:** Range — this pivot table's anchor cell

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getColumnGroups()`

Returns an ordered list of the column groups in this pivot table.

**Returns:** PivotGroup[] — the column groups in this pivot table

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getFilters()`

Returns an ordered list of the filters in this pivot table.

**Returns:** PivotFilter[] — the filters in this pivot table

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getPivotValues()`

Returns an ordered list of the pivot values in this pivot table.

**Returns:** PivotValue[] — the pivot values in this pivot table

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getRowGroups()`

Returns an ordered list of the row groups in this pivot table.

**Returns:** PivotGroup[] — the row groups in this pivot table

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSourceDataRange()`

Returns the source data range on which the pivot table is constructed.

**Returns:** Range — The source data range of this pivot table.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getValuesDisplayOrientation()`

Returns whether values are displayed as rows or columns.

**Returns:** Dimension — whether values are displayed as rows or columns

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Deletes this pivot table. Further operations on this pivot table results in an error.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setValuesDisplayOrientation(dimension)`

Sets the layout of this pivot table to display values as columns or rows.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| dimension | Dimension | The dimension indicating how to display pivot values. |

**Returns:** PivotTable — the pivot table for chaining

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

