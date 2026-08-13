# Columns

The `Columns` widget displays up to 2 columns in a card or dialog.

The `Columns` widget displays up to 2 columns in a card or dialog. You can add widgets to each `Column`; the widgets appear in the order that they are specified.

The height of each column is determined by the taller column. For example, if the first column is taller than the second column, both columns have the height of the first column.

Columns are displayed side-by-side. You can customize the width of each column using the `HorizontalSizeStyle` field.

The widget wraps on narrow screens: ≤480px (web), ≤300pt (iOS), ≤320dp (Android).

Available for Google Chat apps and specific Google Workspace add-on UIs.

```javascript
const column = CardService.newColumn()
    .setHorizontalSizeStyle(
        CardService.HorizontalSizeStyle.FILL_AVAILABLE_SPACE)
    .setHorizontalAlignment(CardService.HorizontalAlignment.CENTER)
    .setVerticalAlignment(CardService.VerticalAlignment.CENTER);
const columns = CardService.newColumns().addColumn(column).setWrapStyle(
    CardService.WrapStyle.WRAP);
```

## Methods

### addColumn(column: Column): Columns

Adds a `Column` to the Columns widget. Columns are displayed in the order in which they're added. You can add up to two columns.

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

### setWrapStyle(wrapStyle: WrapStyle): Columns

Sets the wrap style of the columns, controls how the column resizes based on screen width.
