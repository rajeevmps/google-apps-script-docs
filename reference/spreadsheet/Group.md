# Group

Access and modify spreadsheet groups.

Spreadsheet groups associate contiguous rows or columns that can be expanded or collapsed to hide or show content. Each group has a control toggle to expand or collapse the group as a unit. The depth indicates nested position within larger groups, and the collapsed state determines visibility after parent group expansion. Groups can be manipulated using collapse(), expand(), and remove() methods.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `collapse()` | `Group` | Collapses this group. |
| `expand()` | `Group` | Expands this group. |
| `getControlIndex()` | `Integer` | Returns the control toggle index of this group. This is the index just before the range when the control toggle is shown before the group, or the index just after the range otherwise. |
| `getDepth()` | `Integer` | Returns the depth of this group. |
| `getRange()` | `Range` | Returns the range over which this group exists. |
| `isCollapsed()` | `Boolean` | Returns `true` if this group is collapsed. |
| `remove()` | `void` | Removes this group from the sheet, reducing the group depth of the range by one. This may modify other groups. After calling this, the group object becomes invalid to use. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
const range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
group.collapse();
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
const range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
group.expand();
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
sheet.setRowGroupControlAfter(true);
const range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
const controlIndex = group.getControlIndex(); // Returns 4
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
const range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
const depth = group.getDepth(); // Returns 1 if group at depth 1
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
let range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(1, 1);
range = group.getRange(); // Returns range 2:3
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
const range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
const isCollapsed = group.isCollapsed(); // True if collapsed
```

```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
let range = sheet.getRange('2:3');
range.shiftRowGroupDepth(1);
const group = sheet.getRowGroup(2, 1);
range = group.remove();
```
