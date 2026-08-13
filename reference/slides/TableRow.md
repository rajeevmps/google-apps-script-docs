# TableRow

A row in a table. A row consists of a list of table cells. A row is identified by the row index.

## Methods

### getCell(cellIndex)

`TableCell`

Returns the cell at the specified index.

**Parameters**

- `cellIndex` (`Integer`) — The 0-based index of the cell to retrieve.

**Returns**

`TableCell` — The cell.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getIndex()

`Integer`

Returns the 0-based index of the row.

**Returns**

`Integer` — The 0-based index of the row.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getMinimumHeight()

`Number`

Returns the minimum height of the row in points. The actual height depends on the length of the content of the cell.

**Returns**

`Number` — The minimum height of the row in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNumCells()

`Integer`

Returns the number of cells in this row.

**Returns**

`Integer` — The number of cells in this row.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParentTable()

`Table`

Returns the table containing the current row.

**Returns**

`Table` — The table containing the current row.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### remove()

Removes the table row.

If all the cells in the row are merged with other rows, the common rows spanned by these cells are removed.

If no rows remain in the table after this removal, the whole table is removed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
