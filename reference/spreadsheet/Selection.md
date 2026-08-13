# Selection

Access the current active selection in the active sheet.

Access the current active selection in the active sheet. A selection is the set of cells the user
has highlighted in the sheet, which can be non-adjacent ranges. One cell in the selection is the current cell , where the user's current focus is. The current cell is highlighted with a
darker border in the Google Sheets UI.

## Methods

### `getActiveRange()`

Returns the selected range in the active sheet, or null if there is no active range. If
multiple ranges are selected this method returns only the last selected range.

**Returns:** Range |null — The active range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const selection = SpreadsheetApp.getActiveSpreadsheet().getSelection();
const activeRange = selection.getActiveRange();
```

### `getActiveRangeList()`

Returns the list of active ranges in the active sheet or null if there are no active
ranges.

If there is a single range selected, this behaves as a getActiveRange() call.

**Returns:** RangeList |null — The list of active ranges.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
// Returns the list of active ranges.
const activeRangeList = sheet.getActiveRangeList();
```

### `getActiveSheet()`

Returns the active sheet in the spreadsheet.

**Returns:** Sheet — The active sheet in the spreadsheet.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const selection = SpreadsheetApp.getActiveSpreadsheet().getSelection();
const activeSheet = selection.getActiveSheet();
```

### `getCurrentCell()`

Returns the current (highlighted) cell that is selected in one of the active ranges or null if there is no current cell.

**Returns:** Range |null — The current cell.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
const selection = SpreadsheetApp.getActiveSpreadsheet().getSelection();
// Returns the current highlighted cell in the one of the active ranges.
const currentCell = selection.getCurrentCell();
```

### `getNextDataRange(direction)`

Starting from the current cell and active range and moving in the given direction, returns an adjusted range where the appropriate edge of the
range has been shifted to cover the next data cell while still
covering the current cell. If the active range is unbounded along the dimension of the direction, the original active range is returned. If there is no current cell
or active range, null is returned. This is equivalent to selecting a range in the
editor and hitting Ctrl+Shift+[arrow key] .

**Parameters:**

| Name | Type | Description |
|---|---|---|
| direction | Direction | The direction in which to find the next data region edge cell. |

**Returns:** Range |null — The adjusted range that includes the data cell, or null if there is no
    selection.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

```javascript
// Assume the active spreadsheet is blank.
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

// Makes C3 the current cell and C3:E5 the active range.
sheet.getRange('C3:E5').activate();
// Logs 'C1:E3'
console.log(
    SpreadsheetApp.getSelection()
        .getNextDataRange(SpreadsheetApp.Direction.UP)
        .getA1Notation(),
);
```

