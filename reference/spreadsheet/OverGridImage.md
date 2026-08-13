# OverGridImage

Represents an image over the grid in a spreadsheet.

Represents an image over the grid in a spreadsheet. The OverGridImage class enables manipulation of images placed atop spreadsheet grids, allowing assignment of functions, retrieval and modification of positioning, dimensions, and alt text properties.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `assignScript(functionName: String)` | `OverGridImage` | Assigns the function with the specified function name to this image. This must be a public top level function, not one ending in underscore such as `privateFunction_`. |
| `remove()` | `void` | Deletes this image from the spreadsheet. Any further operation on the image results in a script error. |
| `replace(blob: BlobSource)` | `OverGridImage` | Replaces this image with the one specified by the provided BlobSource. The maximum supported blob size is 2MB. |
| `replace(url: String)` | `OverGridImage` | Replaces this image with the one from the specified URL. |
| `getHeight()` | `Integer` | Returns the actual height of this image in pixels. |
| `setHeight(height: Integer)` | `OverGridImage` | Sets the actual height of this image in pixels. |
| `getWidth()` | `Integer` | Returns the actual width of this image in pixels. |
| `setWidth(width: Integer)` | `OverGridImage` | Sets the actual width of this image in pixels. |
| `getInherentHeight()` | `Integer` | Returns the inherent height of this image in pixels. |
| `getInherentWidth()` | `Integer` | Returns the inherent height of this image in pixels. |
| `resetSize()` | `OverGridImage` | Resets this image to its inherent dimensions. |
| `getAnchorCell()` | `Range` | Returns the cell where an image is anchored. |
| `setAnchorCell(cell: Range)` | `OverGridImage` | Sets the cell where an image is anchored. |
| `getAnchorCellXOffset()` | `Integer` | Returns the horizontal pixel offset from the anchor cell. |
| `setAnchorCellXOffset(offset: Integer)` | `OverGridImage` | Sets the horizontal pixel offset from the anchor cell. |
| `getAnchorCellYOffset()` | `Integer` | Returns the vertical pixel offset from the anchor cell. |
| `setAnchorCellYOffset(offset: Integer)` | `OverGridImage` | Sets the vertical pixel offset from the anchor cell. |
| `getAltTextTitle()` | `String` | Returns the alt text title for this image. |
| `setAltTextTitle(title: String)` | `OverGridImage` | Sets the alt text title for this image. |
| `getAltTextDescription()` | `String` | Returns the alt text description for this image. |
| `setAltTextDescription(description: String)` | `OverGridImage` | Sets the alt-text description for this image. |
| `getScript()` | `String` | Returns the name of the function assigned to this image. |
| `getSheet()` | `Sheet` | Returns the sheet this image appears on. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getUrl()` | `String` | Deprecated. For most newly inserted images, the source URL is unavailable. Gets the image's source URL. Returns an empty string if unavailable. |

## Code Samples

```javascript
// Logs the height of all images in a spreadsheet
const images = SpreadsheetApp.getActiveSpreadsheet().getImages();
for (let i = 0; i < images.length; i++) {
  Logger.log(images[i].getHeight());
}

// Logs the width of all images in a spreadsheet
const images = SpreadsheetApp.getActiveSpreadsheet().getImages();
for (let i = 0; i < images.length; i++) {
  Logger.log(images[i].getWidth());
}

// Logs the parent sheet of all images in a spreadsheet
const images = SpreadsheetApp.getActiveSpreadsheet().getImages();
for (let i = 0; i < images.length; i++) {
  Logger.log(images[i].getSheet());
}

// Deletes all images in a spreadsheet
const images = SpreadsheetApp.getActiveSpreadsheet().getImages();
for (let i = 0; i < images.length; i++) {
  images[i].remove();
}
```
