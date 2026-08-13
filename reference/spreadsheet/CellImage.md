# CellImage

Represents an image value in a cell.

Represents an image value in a cell. To add an image to a cell, you must create a new image value for the image using `SpreadsheetApp.newCellImage()` and `CellImageBuilder`. Then you can use `Range.setValue(value)` or `Range.setValues(values)` to add the image value to the cell.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getAltTextDescription()` | `String` | Returns the alt text description for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `getAltTextTitle()` | `String` | Returns the alt text title for this image. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |
| `getContentUrl()` | `String` | Returns a Google-hosted URL to the image. This URL is tagged with the account of the requester, so anyone with the URL effectively accesses the image as the original requester. Access to the image might be lost if the spreadsheet's sharing settings change. The returned URL expires after a short period of time. |
| `toBuilder()` | `CellImageBuilder` | Creates a cell image builder based on the current image properties. Use `CellImageBuilder.setSourceUrl(url)` to set the source URL of the new image. Then you can add it to a cell using `Range.setValue(value)` or `Range.setValues(values)`. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getUrl()` | `String` | Deprecated. Gets the image's source URL. Returns an empty string if the URL is unavailable. For most newly inserted images, the source URL is unavailable regardless how the image is inserted. Requires `https://www.googleapis.com/auth/spreadsheets.currentonly` or `https://www.googleapis.com/auth/spreadsheets`. |

## Properties

| Property | Type | Description |
|---|---|---|
| `valueType` | `ValueType` | The value type of the cell image, which is `ValueType.IMAGE`. |

## Code Samples

```javascript
const range = SpreadsheetApp.getActiveSpreadsheet().getRange("Sheet1!A1");
const value = range.getValue();
if (value.valueType == SpreadsheetApp.ValueType.IMAGE) {
  console.log(value.getContentUrl());
}
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const range = ss.getRange("Sheet1!A1");
const value = range.getValue();
if (value.valueType == SpreadsheetApp.ValueType.IMAGE) {
  const newImage =
      value.toBuilder()
          .setSourceUrl(
              'https://www.gstatic.com/images/branding/productlogos/apps_script/v10/web-64dp/logo_apps_script_color_1x_web_64dp.png',
              )
          .build();
  const newRange = ss.getRange("Sheet1!A2");
  newRange.setValue(newImage);
}
```
