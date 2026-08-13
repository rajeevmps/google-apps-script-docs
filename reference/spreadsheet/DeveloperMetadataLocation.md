# DeveloperMetadataLocation

Access information about the location of developer metadata.

The `DeveloperMetadataLocation` class provides access to information about the location of developer metadata within a spreadsheet. You can retrieve the location type using `getLocationType()`. Methods like `getColumn()`, `getRow()`, `getSheet()`, and `getSpreadsheet()` return specific locations based on metadata type, or `null` if type doesn't match. Accessing this information requires spreadsheet-related authorization scopes.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getColumn()` | `Range\|null` | Returns the Range for the column location of this metadata, or null if the location type is not `DeveloperMetadataLocationType.COLUMN`. |
| `getLocationType()` | `DeveloperMetadataLocationType` | Gets the type of location. |
| `getRow()` | `Range\|null` | Returns the Range for the row location of this metadata, or null if the location type is not `DeveloperMetadataLocationType.ROW`. |
| `getSheet()` | `Sheet\|null` | Returns the Sheet location of this metadata, or null if the location type is not `DeveloperMetadataLocationType.SHEET`. |
| `getSpreadsheet()` | `Spreadsheet\|null` | Returns the Spreadsheet location of this metadata, or null if the location type is not `DeveloperMetadataLocationType.SPREADSHEET`. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
