# DeveloperMetadataFinder

Search for developer metadata in a spreadsheet.

Search for developer metadata in a spreadsheet. To create new developer metadata finder use `Range.createDeveloperMetadataFinder()`, `Sheet.createDeveloperMetadataFinder()`, or `Spreadsheet.createDeveloperMetadataFinder()`. The DeveloperMetadataFinder enables locating developer metadata within spreadsheets through refined search capabilities. It implements a fluent search interface supporting method chaining — all filter methods return the finder instance, allowing sequential refinement before executing the final `find()` method to retrieve results.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `find()` | `DeveloperMetadata[]` | Executes this search and returns the matching metadata. |
| `onIntersectingLocations()` | `DeveloperMetadataFinder` | Configures the search to consider intersecting locations that have metadata. This option is only valid for range-scoped searches. |
| `withId(id: Integer)` | `DeveloperMetadataFinder` | Limits this search to consider only metadata that match the specified ID. `id` is the ID to match when searching for metadata. |
| `withKey(key: String)` | `DeveloperMetadataFinder` | Limits this search to consider only metadata that match the specified key. `key` is the key to match when searching for metadata. |
| `withLocationType(locationType: DeveloperMetadataLocationType)` | `DeveloperMetadataFinder` | Limits this search to consider only metadata that match the specified location type. `locationType` is the location type to match when searching for metadata. |
| `withValue(value: String)` | `DeveloperMetadataFinder` | Limits this search to consider only metadata that match the specified value. `value` is the value to match when searching for metadata. |
| `withVisibility(visibility: DeveloperMetadataVisibility)` | `DeveloperMetadataFinder` | Limits this search to consider only metadata that match the specified visibility. `visibility` is the visibility to match when searching for metadata. |

## Authorization

`find()` requires one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
