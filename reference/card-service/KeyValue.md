# KeyValue

This class is deprecated. Instead, use `DecoratedText`.

The KeyValue class is deprecated and should not be used in new scripts. Key features include:

- Setting authorization actions that open URLs to authorization flows when clicked
- Setting actions that compose draft emails when clicked
- Setting actions that execute or open URLs in tabs when clicked
- Setting URLs to open directly when clicked

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters:
- `eventAction` (EventAction) - The EventAction to be added.

### setAuthorizationAction(action: AuthorizationAction): KeyValue

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `action` (AuthorizationAction) - The object that specifies the authorization action to take when this element is clicked.

```javascript
const action = CardService.newAuthorizationAction().setAuthorizationUrl('url');
CardService.newTextButton().setText('Authorize').setAuthorizationAction(action);
```

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): KeyValue

Sets an action that composes a draft email when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns a ComposeActionResponse object configured using ComposeActionResponseBuilder.setGmailDraft(draft). This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an Action that composes draft messages in Apps Script that are opened in Gmail when the action completes.

Parameters:
- `action` (Action) - The object that specifies the compose action to take when this element is clicked.
- `composedEmailType` (ComposedEmailType) - An enum value that specifies whether the composed draft is a standalone or reply draft.

```javascript
const action = CardService.newAction().setFunctionName('composeEmailCallback');
CardService.newTextButton()
    .setText('Compose Email')
    .setComposeAction(action, CardService.ComposedEmailType.REPLY_AS_DRAFT);

function composeEmailCallback(e) {
  const thread = GmailApp.getThreadById(e.threadId);
  const draft = thread.createDraftReply('This is a reply');
  return CardService.newComposeActionResponseBuilder()
      .setGmailDraft(draft)
      .build();
}
```

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters:
- `id` (String) - The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

### setOnClickAction(action: Action): KeyValue

Sets an action that executes when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns a ActionResponse object.

Parameters:
- `action` (Action) - The action to take when this element is clicked.

```javascript
const action = CardService.newAction().setFunctionName('notificationCallback');
CardService.newTextButton()
    .setText('Create notification')
    .setOnClickAction(action);

function notificationCallback() {
  return CardService.newActionResponseBuilder()
      .setNotification(
          CardService.newNotification().setText('Some info to display to user'),
          )
      .build();
}
```

### setOnClickOpenLinkAction(action: Action): KeyValue

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns a ActionResponse object configured using ActionResponseBuilder.setOpenLink(openLink).

Parameters:
- `action` (Action) - The object that specifies the open link action to take when this element is clicked.

```javascript
const action = CardService.newAction().setFunctionName('openLinkCallback');
CardService.newTextButton()
    .setText('Open Link')
    .setOnClickOpenLinkAction(action);

function openLinkCallback() {
  return CardService.newActionResponseBuilder()
      .setOpenLink(CardService.newOpenLink().setUrl('https://www.google.com'))
      .build();
}
```

### setOpenLink(openLink: OpenLink): KeyValue

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `openLink` (OpenLink) - An OpenLink object describing the URL to open.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters:
- `visibility` (Visibility) - The Visibility of the widget.

### setBottomLabel(text: String): KeyValue

*Deprecated.* Sets the label text to be used as the key. Displayed below the text-content.

Parameters:
- `text` (String) - The label text. Note: It doesn't support basic HTML formatting.

### setButton(button: Button): KeyValue

*Deprecated.* Sets the Button that is displayed to the right of the context. A KeyValue can only support one button, one switch or one icon.

Parameters:
- `button` (Button) - The button to add.

### setContent(text: String): KeyValue

*Deprecated.* Sets the text to be used as the value. Supports basic HTML formatting. Required.

Parameters:
- `text` (String) - The text content for this widget.

### setIcon(icon: Icon): KeyValue

*Deprecated.* Sets the icon to be used as the key.

Parameters:
- `icon` (Icon) - One of the predefined Icon values.

### setIconAltText(altText: String): KeyValue

*Deprecated.* Sets the alternative text for the icon.

Parameters:
- `altText` (String) - The alternative text for the icon.

### setIconUrl(url: String): KeyValue

*Deprecated.* Sets the URL of the icon to be used as the key.

Parameters:
- `url` (String) - The URL address of a hosted image to use as an icon.

### setMultiline(multiline: Boolean): KeyValue

*Deprecated.* Sets whether the value text should be displayed on a single line or multiple lines.

Parameters:
- `multiline` (Boolean) - The multiline setting.

### setSwitch(switchToSet: Switch): KeyValue

*Deprecated.* Sets the Switch that is displayed to the right of the content. A KeyValue can only support one button, one switch or one icon.

Parameters:
- `switchToSet` (Switch) - The switch to add.

### setTopLabel(text: String): KeyValue

*Deprecated.* Sets the label text to be used as the key. Displayed above the text-content.

Parameters:
- `text` (String) - The label text. Note: It doesn't support basic HTML formatting.
