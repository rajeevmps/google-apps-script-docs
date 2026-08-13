# SortSpec

The sorting specification.

The sorting specification.

## Methods

### `getBackgroundColor()`

Returns the background color used for sorting, or null if absent.

**Returns:** Color |null — The background color.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getDataSourceColumn()`

Gets the data source column the sort spec acts on. Returns null if this sort spec is
not acting on a data source column.

**Returns:** DataSourceColumn |null — The data source column the sort spec acts on.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getDimensionIndex()`

Returns the dimension index or null if not linked to a local filter.

**Returns:** Integer|null — The dimension index.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getForegroundColor()`

Returns the foreground color used for sorting, or null if absent.

**Returns:** Color |null — The foreground color.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getSortOrder()`

Returns the sort order.

**Returns:** SortOrder — The sort order.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `isAscending()`

Returns whether the sort order is ascending.

**Returns:** Boolean — true if the sort order is ascending, or false otherwise.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

