# TextParagraph

A widget that displays text and supports basic HTML formatting.

A widget that displays text and supports basic HTML formatting. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const textParagraph = CardService.newTextParagraph().setText(
    'This is a text paragraph widget. Multiple lines are allowed if needed.',
);
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters:
- `eventAction` (EventAction): The EventAction to be added.

Return: The Object, for chaining.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters:
- `id` (String): The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

Return: This object, for chaining.

### setMaxLines(maxLines: Integer): TextParagraph

Sets the maximum number of lines of text that are displayed in the widget. If the text exceeds the specified maximum number of lines, the excess content is concealed behind a "show more" button. If the text is equal or shorter than the specified maximum number of lines, a "show more" button isn't displayed. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

```javascript
const textParagraph = CardService.newTextParagraph()
    .setText('This is a text paragraph widget. Multiple lines are allowed if needed.')
    .setMaxLines(1);
```

Parameters:
- `maxLines` (Integer): The maximum number of lines of text that are displayed.

Return: This object, for chaining.

### setText(text: String): TextParagraph

Sets the text of the paragraph. Required.

Parameters:
- `text` (String): The text to display.

Return: This object, for chaining.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters:
- `visibility` (Visibility): The Visibility of the widget.

Return: The Object, for chaining.
