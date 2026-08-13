# DecoratedText

A widget that displays text with optional decorations.

A widget that displays text with optional decorations. Possible keys include an icon, a label above and a label below. Setting text content via `setText(text)` and one additional element is required. This class is intended to replace `KeyValue`. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setAuthorizationAction(action: AuthorizationAction): DecoratedText

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads. Only one click-related action (setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType)) can be set.

```javascript
CardService.newAuthorizationAction().setAuthorizationUrl('url')
```

### setBottomLabel(text: String): DecoratedText

Sets the label text to be used as the key and is displayed below the text content.

### setButton(button: Button): DecoratedText

Sets the `Button` that is displayed to the right of the text. A `DecoratedText` can only support one button or one switch.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): DecoratedText

Sets an action that composes a draft email when the object is clicked. Only one click action (setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType)) can be set. The Action parameter must specify a callback function that returns a `ComposeActionResponse` object configured using `setGmailDraft(draft)`.

### setEndIcon(endIcon: IconImage): DecoratedText

Sets the optional `IconImage` that is displayed to the right of the content. A `DecoratedText` can only support one button, one switch or one icon.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons. The id has a limit of 64 characters and must be in the format `[a-zA-Z0-9-]+`.

### setOnClickAction(action: Action): DecoratedText

Sets an action that executes when the object is clicked. Only one click action (setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType)) can be set. The Action parameter must specify a callback function that returns an `ActionResponse` object.

### setOnClickOpenLinkAction(action: Action): DecoratedText

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the `OpenLink` object. Only one click action (setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType)) can be set.

### setOpenLink(openLink: OpenLink): DecoratedText

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened. Only one click action (setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType)) can be set.

### setStartIcon(startIcon: IconImage): DecoratedText

Sets the optional `IconImage` to display before the text content.

### setSwitchControl(switchToSet: Switch): DecoratedText

Sets the `Switch` that is displayed to the right of the content. A `DecoratedText` can only support one button or one switch.

### setText(text: String): DecoratedText

Sets the text to be used as the value. Supports basic HTML formatting. Required.

### setTopLabel(text: String): DecoratedText

Sets the label text to be used as the key and is displayed above the text content.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

### setWrapText(wrapText: Boolean): DecoratedText

Sets whether the value text should be displayed on a single line or multiple lines.
