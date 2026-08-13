# Slicer

Represents a slicer , which is used
to filter ranges, charts and pivot tables in a non-collaborative manner.

Represents a slicer , which is used
to filter ranges, charts and pivot tables in a non-collaborative manner. This class contains
methods to access and modify existing slicers. To create a new slicer, use Sheet.insertSlicer(range, anchorRowPos, anchorColPos) .

## Methods

### `getBackgroundColorObject()`

Return the background Color of the slicer.

**Returns:** Color |null — The background color of this slicer. Returns null if no color is set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getColumnPosition()`

Returns the column position (relative to the data range of the slicer) on which the filter is
applied in the slicer, or null if the column position is not set. This should be
1-indexed position of the column similar to filter.

**Returns:** Integer|null — The column position of this slicer.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getContainerInfo()`

Gets information about where the slicer is positioned in the sheet.

**Returns:** ContainerInfo — An object containing the slicer's container position.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getFilterCriteria()`

Returns the filter criteria of the slicer, or null if the filter criteria is not set.

**Returns:** FilterCriteria |null — The filter criteria of this slicer.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getRange()`

Gets the data range on which the slicer is applied to.

**Returns:** Range — The slicer range.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getTitle()`

Returns the title of the slicer.

**Returns:** String — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getTitleHorizontalAlignment()`

Gets the horizontal alignment of the title.

**Returns:** String — The horizontal alignment of this slicer's title.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getTitleTextStyle()`

Returns the text style of the slicer's title.

**Returns:** TextStyle — The text style of this slicer's title.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `isAppliedToPivotTables()`

Returns whether the given slicer is applied to pivot tables.

**Returns:** Boolean — true if this slicer is applied to pivot tables, otherwise false .

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `remove()`

Deletes the slicer.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setApplyToPivotTables(applyToPivotTables)`

Sets if the given slicer should be applied to pivot tables in the worksheet.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| apply To Pivot Tables | Boolean | Specifies whether this slicer should apply to pivot tables. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setBackgroundColor(color)`

Sets the background color of the slicer. A null value resets the background color.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| color | String | The new background color of this slicer in CSS notation (such as '#ffffff'). |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setBackgroundColorObject(color)`

Sets the background Color of the slicer. A null value resets the background
color.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| color | Color | The new background color of this slicer. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setColumnFilterCriteria(columnPosition, filterCriteria)`

Sets the column index and filtering criteria of the slicer. A null value resets the
slicer filter.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| column Position | Integer | The new column position of this slicer. |
| filter Criteria | Filter Criteria | The new filter criteria of this slicer. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setPosition(anchorRowPos, anchorColPos, offsetX, offsetY)`

Sets the position where the slicer appears on the sheet. The anchor row and column position
indices are 1-indexed.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| anchor Row Pos | Integer | The slicer's top side is anchored in this row. |
| anchor Col Pos | Integer | The slicer's top side is anchored in this col. |
| offsetX | Integer | The horizontal offset from cell corner in pixels. |
| offsetY | Integer | The vertical offset from cell corner in pixels. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setRange(rangeApi)`

Sets the data range on which the slicer is applied.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| range Api | Range | The new range for this slicer. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setTitle(title)`

Sets the title of the slicer. An empty title resets the title to default value.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| title | String | The new title of this slicer. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setTitleHorizontalAlignment(horizontalAlignment)`

Sets the horizontal alignment of the title in the slicer. A null value resets the
alignment.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| horizontal Alignment | String | The new horizontal alignment of this slicer's title. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setTitleTextStyle(textStyle)`

Sets the text style of the slicer.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| text Style | Text Style | The new text style of the slicer's title. |

**Returns:** Slicer — This slicer, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

## Deprecated Methods

### `getBackgroundColor()`

Deprecated. Replaced by getBackgroundColorObject()

Returns the background color of the slicer in CSS notation (such as '#ffffff').

**Returns:** String|null — The background color of this slicer. Returns null if no color is set.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

