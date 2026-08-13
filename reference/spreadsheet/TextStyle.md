# TextStyle

The rendered style of text in a cell.

The rendered style of text in a cell.

Text styles can have a corresponding RichTextValue . If the RichTextValue spans multiple text runs that have different values for a given text style read
method, the method returns null . To avoid this, query for text styles using the Rich Text
values returned by the RichTextValue.getRuns() method.

## Methods

### `copy()`

Creates a text style builder initialized with the values of this text style.

**Returns:** TextStyleBuilder — A builder from this text style.

### `getFontFamily()`

Gets the font family of the text. Returns null if the font family isn't set or the
corresponding RichTextValue has multiple runs with different font
families.

**Returns:** String — The font family of the text (for example, "Arial") or null .

### `getFontSize()`

Gets the font size of the text in points. Returns null if the font size isn't set or
the corresponding RichTextValue has multiple runs with different font
sizes.

**Returns:** Integer — The font size of the text or null .

### `getForegroundColorObject()`

Gets the font color of the text. Returns null if the font color isn't set or the
corresponding RichTextValue has multiple runs with different font
colors.

**Returns:** Color |null — The font color of the text or null .

### `isBold()`

Gets whether or not the text is bold. Returns null if bold isn't set or the
corresponding RichTextValue has multiple runs with different bold
settings.

**Returns:** Boolean — Whether or not the cell is bold, or null .

### `isItalic()`

Gets whether or not the cell is italic. Returns null if italic isn't set or the
corresponding RichTextValue has multiple runs with different italic
settings.

**Returns:** Boolean — Whether or not the cell is italic, or null .

### `isStrikethrough()`

Gets whether or not the cell has strikethrough. Returns null if strikethrough isn't set
or the corresponding RichTextValue has multiple runs with different
strikethrough settings.

**Returns:** Boolean — Whether or not the cell has strikethrough, or null .

### `isUnderline()`

Gets whether or not the cell is underlined. Returns null if underline isn't set or the
corresponding RichTextValue has multiple runs with different underline
settings.

**Returns:** Boolean — Whether or not the cell is underlined, or null .

## Deprecated Methods

### `getForegroundColor()`

Deprecated. Replaced by getForegroundColorObject()

Gets the font color of the text. Returns null if the font color isn't set or the
corresponding RichTextValue has multiple runs with different font
colors.

**Returns:** String|null — The font color of the text as a hex CSS value (for example, "#ff0000") or null .

