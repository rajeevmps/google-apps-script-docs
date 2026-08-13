# CellImageBuilder

Builder for CellImage.

Builder for `CellImage`. This builder creates the image value needed to add an image to a cell.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `CellImage` | Creates the image value type needed to add an image to a cell. The image value is built from the image properties added to the builder, such as the source URL. |
| `getAltTextDescription()` | `String` | Returns the alt text description for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `getAltTextTitle()` | `String` | Returns the alt text title for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `getContentUrl()` | `String` | Returns a Google-hosted URL to the image. This URL is tagged with the account of the requester, so anyone with the URL effectively accesses the image as the original requester. Access to the image might be lost if the spreadsheet's sharing settings change. The returned URL expires after a short period of time. |
| `setAltTextDescription(description: String)` | `CellImage` | Sets the alt-text description for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `setAltTextTitle(title: String)` | `CellImage` | Sets the alt text title for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `setSourceUrl(url: String)` | `CellImageBuilder` | Sets the image source URL. |
| `toBuilder()` | `CellImageBuilder` | Creates a cell image builder based on the current image properties. Use `setSourceUrl(url)` to set the source URL of the new image. Then you can add it to a cell using `Range.setValue(value)` or `Range.setValues(values)`. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getUrl()` | `String` | Deprecated. Gets the image's source URL. Returns an empty string if the URL is unavailable. For most newly inserted images, the source URL is unavailable regardless how the image is inserted. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |

## Properties

| Property | Type | Description |
|---|---|---|
| `valueType` | `ValueType` | The value type of the cell image, which is `ValueType.IMAGE`. |
