# DeveloperMetadata

Access and modify developer metadata.

Access and modify developer metadata. To create new developer metadata use `Range.addDeveloperMetadata(key)`, `Sheet.addDeveloperMetadata(key)`, or `Spreadsheet.addDeveloperMetadata(key)`. The class enables developers to work with metadata attached to spreadsheet objects, with properties including ID, key, location, value, and visibility settings.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getId()` | `Integer` | Returns the unique ID associated with this developer metadata. |
| `getKey()` | `String` | Returns the key associated with this developer metadata. |
| `getLocation()` | `DeveloperMetadataLocation` | Returns the location of this developer metadata. |
| `getValue()` | `String` | Returns the value associated with this developer metadata, or `null` if this metadata has no value. |
| `getVisibility()` | `DeveloperMetadataVisibility` | Returns the visibility of this developer metadata. |
| `moveToColumn(column: Range)` | `DeveloperMetadata` | Moves this developer metadata to the specified column. If the specified range does not represent a single column this throws an exception. `column` is the range representing the column that is the new location for this developer metadata. |
| `moveToRow(row: Range)` | `DeveloperMetadata` | Moves this developer metadata to the specified row. If the specified range does not represent a single row this throws an exception. `row` is the range representing the row that is the new location for this developer metadata. |
| `moveToSheet(sheet: Sheet)` | `DeveloperMetadata` | Moves this developer metadata to the specified sheet. `sheet` is the sheet that is the new location for this developer metadata. |
| `moveToSpreadsheet()` | `DeveloperMetadata` | Moves this developer metadata to the top-level spreadsheet. |
| `remove()` | `void` | Deletes this metadata. |
| `setKey(key: String)` | `DeveloperMetadata` | Sets the key of this developer metadata to the specified value. `key` is the new key to set for this metadata. |
| `setValue(value: String)` | `DeveloperMetadata` | Sets the value associated with this developer metadata to the specified value. `value` is the new value to set for this metadata. |
| `setVisibility(visibility: DeveloperMetadataVisibility)` | `DeveloperMetadata` | Sets the visibility of this developer metadata to the specified visibility. `visibility` is the new visibility to set for this metadata. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
