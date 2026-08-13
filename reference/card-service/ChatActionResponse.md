# ChatActionResponse

A class that represents the parameters that a Chat app can use to configure how its response is posted.

A class that represents the parameters that a Chat app can use to configure how its response is posted. Only available for Google Chat apps. Not available for Google Workspace add-ons.

```javascript
const card = CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle('Card title'))
    .build();
const dialog = CardService.newDialog().setBody(card);
const dialogAction = CardService.newDialogAction().setDialog(dialog);
const chatActionResponse = CardService.newChatActionResponse()
    .setResponseType(CardService.Type.DIALOG)
    .setDialogAction(dialogAction);
```

## Methods

### setDialogAction(dialogAction: DialogAction): ChatActionResponse

Sets the dialog action to an event related to a dialog.

### setResponseType(responseType: ResponseType): ChatActionResponse

The type of Chat app response.

### setUpdatedWidget(updatedWidget: UpdatedWidget): ChatActionResponse

Sets the updated widget, used to provide autocomplete options for a widget. Only available for Google Chat apps. Not available for Google Workspace add-ons.

### setUrl(url: String): ChatActionResponse

The URL for users to authenticate or configure. Only for the `REQUEST_CONFIG` response type.
