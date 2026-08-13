# ActionResponse

The response object that may be returned from a callback function.

The response object that may be returned from a callback function (e.g., a form response handler) to perform one or more actions on the client. Some combinations of actions are not supported. ActionResponse enables developers to execute client-side operations following callback execution, including navigation, notifications, and link opening.

Instances are created via an ActionResponseBuilder (see `CardService.newActionResponseBuilder()`).

## Code Sample

```javascript
// Opens a link via setOpenLink() with a URL.
var actionResponse = CardService.newActionResponseBuilder()
    .setOpenLink(CardService.newOpenLink().setUrl('https://www.example.com'))
    .build();

// Displays a notification using setNotification() with custom text.
var actionResponse = CardService.newActionResponseBuilder()
    .setNotification(CardService.newNotification()
        .setText("Some info to display to user"))
    .build();

// Navigates to additional cards with setNavigation().pushCard() while
// flagging state changes via setStateChanged(true).
var actionResponse = CardService.newActionResponseBuilder()
    .setNavigation(CardService.newNavigation().pushCard(card))
    .setStateChanged(true)
    .build();
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.

Returns: String — the JSON representation of this object.
