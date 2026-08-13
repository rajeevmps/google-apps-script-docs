# ParagraphStyle

The styles of text that apply to entire paragraphs.

"The styles of text that apply to entire paragraphs." Read methods return `null` if the corresponding TextRange spans multiple paragraphs with different values. To avoid this issue, query using the TextRange from `Paragraph.getRange()`. Additionally, "Editing text fit within a shape deactivates any autofit settings on paragraph styles."

## Methods

### getIndentEnd()

`Number|null`

Returns the text end indentation for paragraphs in the TextRange in points, or null if multiple paragraph styles exist. The end side corresponds to the text direction.

**Returns**

`Number|null` — the end indentation in points, or null.

### getIndentFirstLine()

`Number|null`

Returns the indentation for the first line of paragraphs in points, or null if multiple styles are present.

**Returns**

`Number|null` — the first line indentation in points, or null.

### getIndentStart()

`Number|null`

Returns the text start indentation in points, or null with multiple styles. The start side is based on current text direction.

**Returns**

`Number|null` — the start indentation in points, or null.

### getLineSpacing()

`Number|null`

Returns the line spacing value representing space between lines as a percentage of normal (100.0), or null with multiple styles.

**Returns**

`Number|null` — the line spacing, or null.

### getParagraphAlignment()

`ParagraphAlignment|null`

Returns the ParagraphAlignment of paragraphs, or null if multiple styles exist.

**Returns**

`ParagraphAlignment|null` — the paragraph alignment, or null.

### getSpaceAbove()

`Number|null`

Returns the extra space above paragraphs in points, or null with multiple styles.

**Returns**

`Number|null` — the space above, or null.

### getSpaceBelow()

`Number|null`

Returns the extra space below paragraphs in points, or null with multiple styles.

**Returns**

`Number|null` — the space below, or null.

### getSpacingMode()

`SpacingMode|null`

Returns the SpacingMode for paragraphs, or null with multiple styles.

**Returns**

`SpacingMode|null` — the spacing mode, or null.

### getTextDirection()

`TextDirection|null`

Returns the TextDirection for paragraphs, or null with multiple styles.

**Returns**

`TextDirection|null` — the text direction, or null.

### setIndentEnd(indent)

`ParagraphStyle`

Sets the text end indentation in points. Enables method chaining.

**Parameters**

- `indent` (`Number`) — the end indentation in points.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setIndentFirstLine(indent)

`ParagraphStyle`

Sets first line indentation in points. Supports chaining.

**Parameters**

- `indent` (`Number`) — the first line indentation in points.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setIndentStart(indent)

`ParagraphStyle`

Sets text start indentation in points. Returns this object for chaining.

**Parameters**

- `indent` (`Number`) — the start indentation in points.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setLineSpacing(spacing)

`ParagraphStyle`

Sets line spacing as a percentage of normal. Chainable.

**Parameters**

- `spacing` (`Number`) — the line spacing percentage.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setParagraphAlignment(alignment)

`ParagraphStyle`

Sets the ParagraphAlignment. Returns this for chaining.

**Parameters**

- `alignment` (`ParagraphAlignment`) — the paragraph alignment.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setSpaceAbove(space)

`ParagraphStyle`

Sets extra space above paragraphs in points. Chainable.

**Parameters**

- `space` (`Number`) — the space above, in points.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setSpaceBelow(space)

`ParagraphStyle`

Sets extra space below paragraphs in points. Chainable.

**Parameters**

- `space` (`Number`) — the space below, in points.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setSpacingMode(mode)

`ParagraphStyle`

Sets the SpacingMode for paragraphs. Chainable.

**Parameters**

- `mode` (`SpacingMode`) — the spacing mode.

**Returns**

`ParagraphStyle` — this object, for chaining.

### setTextDirection(direction)

`ParagraphStyle`

Sets the TextDirection for paragraphs. Chainable.

**Parameters**

- `direction` (`TextDirection`) — the text direction.

**Returns**

`ParagraphStyle` — this object, for chaining.

**Authorization**

Scripts that use these methods require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
