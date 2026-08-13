# Divider

A horizontal divider.

A horizontal divider. To add a divider to your add-on card, use the `newDivider()` method within `CardService`.

```javascript
function buildCard() {
  const cardSection1TextParagraph1 =
      CardService.newTextParagraph().setText('Hello world!');

  const cardSection1Divider1 = CardService.newDivider();

  const cardSection1TextParagraph2 =
      CardService.newTextParagraph().setText('Hello world!');

  const cardSection1 = CardService.newCardSection()
                           .addWidget(cardSection1TextParagraph1)
                           .addWidget(cardSection1Divider1)
                           .addWidget(cardSection1TextParagraph2);

  const card = CardService.newCardBuilder().addSection(cardSection1).build();

  return card;
}
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters:
- `eventAction` (EventAction): The `EventAction` to be added.

Returns: The Object, for chaining.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters:
- `id` (String): The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

Returns: This object, for chaining.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters:
- `visibility` (Visibility): The `Visibility` of the widget.

Returns: The Object, for chaining.
