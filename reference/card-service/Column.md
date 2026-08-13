# Column

A column.

A column. Available for Google Chat apps and Google Workspace add-ons.

```javascript
const columnWidget = CardService.newTextParagraph();
const column = CardService.newColumn()
    .setHorizontalSizeStyle(CardService.HorizontalSizeStyle.FILL_AVAILABLE_SPACE)
    .setHorizontalAlignment(CardService.HorizontalAlignment.CENTER)
    .setVerticalAlignment(CardService.VerticalAlignment.CENTER)
    .addWidget(columnWidget);
```

## Methods

### addWidget(widget: Widget): Column

Adds a widget to the column. Widgets are displayed in the order they are added. You can add the following widgets to a column: TextParagraph, Image, DecoratedText, ButtonSet, TextInput, SelectionInput, DateTimePicker

Parameters: `widget` (Widget) — The widget to add to the column.

Returns: This object, for chaining.

### setHorizontalAlignment(horizontalAlignment: HorizontalAlignment): Column

Sets the HorizontalAlignment of the Column. Optional.

Parameters: `horizontalAlignment` (HorizontalAlignment) — The horizontal alignment of the column.

Returns: This object, for chaining.

### setHorizontalSizeStyle(horizontalSizeStyle: HorizontalSizeStyle): Column

Sets the HorizontalSizeStyle of the Column. Optional.

Parameters: `horizontalSizeStyle` (HorizontalSizeStyle) — The horizontal size of the column.

Returns: This object, for chaining.

### setVerticalAlignment(verticalAlignment: VerticalAlignment): Column

Sets the VerticalAlignment of the Column. Optional.

Parameters: `verticalAlignment` (VerticalAlignment) — The vertical alignment of the column.

Returns: This object, for chaining.
