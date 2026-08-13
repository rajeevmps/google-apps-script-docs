# ButtonSet

Holds a set of Button objects displayed in a row.

Holds a set of Button objects that are displayed in a row. Available for Google Workspace add-ons and Google Chat apps. You can add a button to a ButtonSet using the `addButton()` method.

## Methods

### addButton(button: Button): ButtonSet

Adds a button.

Parameters:
- `button` (Button): The button to add.

Returns: This object, for chaining.

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters:
- `eventAction` (EventAction): The EventAction to be added.

Returns: The Object, for chaining.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters:
- `id` (String): The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

Returns: This object, for chaining.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters:
- `visibility` (Visibility): The Visibility of the widget.

Returns: The Object, for chaining.
