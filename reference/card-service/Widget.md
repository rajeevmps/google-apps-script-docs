# Widget

Base class for all widgets that can be added to a Card.

Base class for all widgets that can be added to a Card.

The following widgets extend this base class: ButtonSet, Carousel, TextParagraph, ChipList, Columns, DecoratedText, Divider, Grid, Image, SelectionInput, TextInput.

## Methods

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
