# TableColumn

A column in a table. A column consists of a list of table cells. A column is identified by the column index.

## Methods

### getCell(cellIndex)

`TableCell`

Returns the cell at the specified index.

**Parameters**

- `cellIndex` (`Integer`) — The 0-based index of the cell to retrieve.

**Returns**

`TableCell` — The cell at the specified index.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getIndex()

`Integer`

Returns the 0-based index of the column.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNumCells()

`Integer`

Returns the number of cells in this column.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParentTable()

`Table`

Returns the table containing the current column.

**Returns**

`Table`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getWidth()

`Number`

Returns the width of the column in points.

**Returns**

`Number`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### remove()

Removes the table column.

If all the cells in the column are merged with other columns, the common columns spanned by these cells are removed.

If no columns remain in the table after this removal, the whole table is removed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
