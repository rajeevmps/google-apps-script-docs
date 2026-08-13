# ActionResponse

The actions that add-ons can use in cards or the host application.

The actions that add-ons can use in cards or the host application. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Sample

```javascript
const notification = AddOnsResponseService.newNotification()
    .setText("You closed a dialog!");

const navigation = AddOnsResponseService.newNavigation()
    .setEndNavigation(AddOnsResponseService.EndNavigation.CLOSE_DIALOG);

// An action that closes the dialog and shows a notification.
const action = AddOnsResponseService.newActionResponseBuilder()
    .setNavigation(navigation)
    .setNotification(notification)
    .build();
```

Note: the reference page shows only one documented method (`printJson()`). The code sample demonstrates usage patterns with builder methods (see `ActionResponseBuilder`).
