# RichTextValue

A stylized text string used to represent cell text.

A stylized text string used to represent cell text. Substrings of the text can have different
text styles.

A run is the longest unbroken substring having the same text style. For example, the
sentence, "This child is carrying apples" has 4 runs: ['This ', 'child ',
'is carrying ', 'apples'] .

## Methods

### `copy()`

Returns a builder for a Rich Text value initialized with the values of this Rich Text value.

**Returns:** RichTextValueBuilder — A builder for a Rich Text value.

### `getEndIndex()`

Gets the end index of this value in the cell.

**Returns:** Integer — The end index of this value in the cell.

### `getLinkUrl()`

Returns the link URL for this value.

**Returns:** String|null — The link URL for this value, or null if there is no link or if there are
    multiple different links.

### `getLinkUrl(startOffset, endOffset)`

Returns the link URL for the text from startOffset to endOffset . Offsets are 0
based and relative to the cell's text, with the start offset being inclusive and the end offset
being exclusive.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Offset | Integer | The start offset. |
| end Offset | Integer | The end offset. |

**Returns:** String|null — The link URL for this value, or null if there is no link or if multiple
    different links are in the given range.

### `getRuns()`

Returns the Rich Text string split into an array of runs, wherein each run is the longest
possible substring having a consistent text style.

**Returns:** RichTextValue[] — An array of runs.

### `getStartIndex()`

Gets the start index of this value in the cell.

**Returns:** Integer — The start index of this value in the cell.

### `getText()`

Returns the text of this value.

**Returns:** String — The text of this value.

### `getTextStyle()`

Returns the text style of this value.

**Returns:** TextStyle — The text style of this value.

### `getTextStyle(startOffset, endOffset)`

Returns the text style of the text from startOffset to endOffset . Offsets are 0
based and relative to the cell's text, with the start offset being inclusive and the end offset
being exclusive.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| start Offset | Integer | The start offset. |
| end Offset | Integer | The end offset. |

**Returns:** TextStyle — The text style of the given substring of this value.

