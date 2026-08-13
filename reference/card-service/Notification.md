# Notification

A notification shown to the user as a response to interacting with a UI element.

A notification shown to the user as a response to interacting with a UI element.

## Methods

### setText(text: String): Notification

Sets the text to show in the notification. Required.

```javascript
const action = CardService.newAction().setFunctionName('notificationCallback');
CardService.newTextButton().setText('Save').setOnClickAction(action);

// ...

function notificationCallback() {
  return CardService.newActionResponseBuilder()
      .setNotification(
          CardService.newNotification().setText('Some info to display to user'),
          )
      .build();
}
```
