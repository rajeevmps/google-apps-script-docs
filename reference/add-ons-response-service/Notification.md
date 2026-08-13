# Notification

Displays a notification when users submit and close a dialog.

Displays a notification when users submit and close a dialog. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### setText(text)

`setText(text: String): Notification`

Sets the text to show in the notification. Required.

**Parameters**
- `text` (String) — The notification text.

**Returns**
- `Notification` — This object, for chaining.

## Code Sample

```javascript
const notification = AddOnsResponseService.newNotification()
  .setText("You closed a dialog!");
```
