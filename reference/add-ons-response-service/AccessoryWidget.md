# AccessoryWidget

A builder for Chat `AccessoryWidget` objects.

A builder for Chat `AccessoryWidget` objects. [Accessory widgets](https://developers.google.com/workspace/chat/create-messages#add-accessory-widgets) are interactive widgets that appear at the bottom of a message.

Available for Google Workspace add-ons that extend Google Chat.

## Methods

### addWidget(widget)

`addWidget(widget: Widget): AccessoryWidget`

Sets the widget for this action.

**Parameters**
- `widget` (Widget): The widget to set.

**Return**
- `AccessoryWidget` — This object, for chaining.

## Code Sample

```javascript
const widget = CardService.newButtonSet()
    .addButton(CardService.newImageButton()
      .setIcon(CardService.Icon.PHONE)
      .setOnClickAction(CardService.newAction()
        .setFunctionName("phone")))
    .addButton(CardService.newTextButton()
      .setText("Robot")
      .setIconUrl("https://developers.google.com/chat/images/quickstart-app-avatar.png")
      .setOnClickAction(CardService.newAction()
        .setFunctionName("robot")));

const accessoryWidget = AddOnsResponseService.newAccessoryWidget()
    .addWidget(widget);
```
