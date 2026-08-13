# NamedRange

Create, access and modify named ranges in a spreadsheet.

Create, access and modify named ranges in a spreadsheet. Named ranges are ranges that have associated string aliases. They can be viewed and edited via the Sheets UI under the Data > Named ranges... menu.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getName()` | `String` | Gets the name of this named range. |
| `getRange()` | `Range` | Gets the range referenced by this named range. Returns the spreadsheet range that is associated with this named range. |
| `remove()` | `void` | Deletes this named range. |
| `setName(name: String)` | `NamedRange` | Sets/updates the name of the named range. `name` is the new name of the named range. Returns the range whose name was set by the call. |
| `setRange(range: Range)` | `NamedRange` | Sets/updates the range for this named range. `range` is the spreadsheet range to associate with this named range. Returns the named range for which the spreadsheet range was set. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Code Samples

```javascript
const namedRanges = SpreadsheetApp.getActive().getNamedRanges();
for (let i = 0; i < namedRanges.length; i++) {
  namedRanges[i].remove();
}
```

```javascript
const namedRanges = SpreadsheetApp.getActiveSpreadsheet().getNamedRanges();
if (namedRanges.length > 1) {
  namedRanges[0].setName('UpdatedNamedRange');
}
```
