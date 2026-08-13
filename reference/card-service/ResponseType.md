# ResponseType

An enum that represents the type of Chat app response.

An enum that represents the type of Chat app response. Only available for Google Chat apps. Not available for Google Workspace add-ons.

To call an enum, you call its parent class, name, and property. For example, `CardService.ResponseType.DIALOG`.

## Properties

### TYPE_UNSPECIFIED
Default type that's handled as NEW_MESSAGE.

### NEW_MESSAGE
Post as a new message in the topic.

### UPDATE_MESSAGE
Update the Chat app's message. This is only permitted on a CARD_CLICKED event where the message sender type is BOT.

### UPDATE_USER_MESSAGE_CARDS
Update the cards on a user's message. This is only permitted as a response to a MESSAGE event with a matched URL, or a CARD_CLICKED event where the message sender type is HUMAN. Text is ignored.

### REQUEST_CONFIG
Privately ask the user for additional authentication or configuration.

### DIALOG
Presents a dialog.

### UPDATE_WIDGET
Widget text autocomplete options query.
