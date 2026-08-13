# PivotGroupLimit

Access and modify pivot table group limit.

Access and modify pivot table group limit.

## Methods

### `getCountLimit()`

Gets the count limit on rows or columns in the pivot group.

**Returns:** Integer — The count limit on rows or columns.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getPivotGroup()`

Returns the pivot group the limit belongs to.

**Returns:** PivotGroup — The pivot group.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Removes the pivot group limit.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setCountLimit(countLimit)`

Sets the count limit on rows or columns in the pivot group.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| count Limit | Integer | The count limit on rows or columns to set. Must be positive. |

**Returns:** PivotGroupLimit — The pivot group limit, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

