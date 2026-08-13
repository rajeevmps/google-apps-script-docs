# HorizontalSizeStyle

An enum that sets how widgets fill the space of a column.

An enum that sets how widgets fill the space of a column. Available for Google Chat apps and Google Workspace add-ons.

To call an enum, you call its parent class, name, and property. For example, `CardService.HorizontalSizeStyle.FILL_AVAILABLE_SPACE`.

## Properties

### FILL_AVAILABLE_SPACE
Sizes the Widget to fill the available horizontal space of a Column. If the other column has more space, the widget can fill the space beyond the space of its own column. Default.

### FILL_MINIMUM_SPACE
Resizes the Widget to fill the least amount of horizontal space in a Column. The minimum space is based on the size of the widget. If the widget is smaller than the space of the column, it doesn't expand to fill the space.
