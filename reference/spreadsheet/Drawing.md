# Drawing

Represents a drawing over a sheet in a spreadsheet.

Represents a drawing over a sheet in a spreadsheet. The Drawing class enables interaction with drawing objects placed on spreadsheet sheets, providing access to positioning, dimensions, macros, and z-index management.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getContainerInfo()` | `ContainerInfo` | Gets information about where the drawing is positioned in the sheet. Returns an object containing the drawing's container position. |
| `getHeight()` | `Integer` | Returns the actual height of this drawing in pixels. |
| `getOnAction()` | `String\|null` | Returns the name of the macro attached to this drawing. |
| `getSheet()` | `Sheet` | Returns the sheet this drawing appears on. |
| `getWidth()` | `Integer` | Returns the actual width of this drawing in pixels. |
| `getZIndex()` | `Number` | Returns the z-index of this drawing. |
| `remove()` | `void` | Deletes this drawing from the spreadsheet. Any further operation on the drawing results in a script error. |
| `setHeight(height: Integer)` | `Drawing` | Sets the actual height of this drawing in pixels. `height` is the desired height in pixels. |
| `setOnAction(macroName: String)` | `Drawing` | Assigns a macro function to this drawing. `macroName` is the name of the macro function. |
| `setPosition(anchorRowPos: Integer, anchorColPos: Integer, offsetX: Integer, offsetY: Integer)` | `Drawing` | Sets the position where the drawing appears on the sheet. The anchor row and column position indices are 1-indexed. `anchorRowPos` — the drawing's top side is anchored in this row; `anchorColPos` — the drawing's top side is anchored in this col; `offsetX` — the horizontal offset from the cell corner in pixels; `offsetY` — the vertical offset from the cell corner in pixels. |
| `setWidth(width: Integer)` | `Drawing` | Sets the actual width of this drawing in pixels. `width` is the desired width in pixels. |
| `setZIndex(zIndex: Number)` | `Drawing` | Sets the z-index of this drawing. `zIndex` is the z-index of this drawing. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Code Samples

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  Logger.log(drawings[i].getHeight());
}
```

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  Logger.log(drawings[i].getOnAction());
}
```

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  Logger.log(drawings[i].getSheet());
}
```

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  Logger.log(drawings[i].getWidth());
}
```

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  Logger.log(drawings[i].getZIndex());
}
```

```javascript
const drawings = SpreadsheetApp.getActiveSheet().getDrawings();
for (let i = 0; i < drawings.length; i++) {
  drawings[i].remove();
}
```
