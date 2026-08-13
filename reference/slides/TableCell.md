# TableCell

A cell in a table.

## Methods

### getColumnIndex()

`Integer`

Returns the 0-based column index of the table cell.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getColumnSpan()

`Integer`

Returns the column span of the table cell.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getContentAlignment()

`ContentAlignment`

Returns the ContentAlignment of the text in the table cell.

**Returns**

`ContentAlignment`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getFill()

`Fill`

Returns the fill of the table cell.

**Returns**

`Fill`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getHeadCell()

`TableCell|null`

Returns the head cell of this table cell. Returns null if this cell has not been merged or if this cell is the head cell.

**Returns**

`TableCell|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getMergeState()

`CellMergeState`

Returns the merge state of the table cell.

**Returns**

`CellMergeState`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParentColumn()

`TableColumn`

Returns the table column containing the current cell.

**Returns**

`TableColumn`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParentRow()

`TableRow`

Returns the table row containing the current cell.

**Returns**

`TableRow`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getParentTable()

`Table`

Returns the table containing the current cell.

**Returns**

`Table`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getRowIndex()

`Integer`

Returns the 0-based row index of the table cell.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getRowSpan()

`Integer`

Returns the row span of the table cell.

**Returns**

`Integer`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getText()

`TextRange`

Returns the text content of the table cell. Returns null if the cell is merged but is not a head cell.

Text within a table cell always terminates with a newline character.

**Returns**

`TextRange`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setContentAlignment(contentAlignment)

`TableCell`

Sets the ContentAlignment of the text in the table cell.

**Parameters**

- `contentAlignment` (`ContentAlignment`) — The content alignment to set.

**Returns**

`TableCell` — This TableCell, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
