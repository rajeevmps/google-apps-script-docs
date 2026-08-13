# TextButton

A TextButton with a text label.

A `TextButton` with a text label. You can set the background color and deactivate the button when needed. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setAltText(altText: String): TextButton

Sets the alternative text of the button for accessibility. If unset, defaults to the text that displays on the button.

### setAuthorizationAction(action: AuthorizationAction): TextButton

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads. A UI object can only have one of `setOpenLink(openLink)`, `setOnClickAction(action)`, `setOnClickOpenLinkAction(action)`, `setAuthorizationAction(action)`, or `setComposeAction(action, composedEmailType)` set.

```javascript
const action = CardService.newAuthorizationAction().setAuthorizationUrl('url');
CardService.newTextButton().setText('Authorize').setAuthorizationAction(action);
```

### setBackgroundColor(backgroundColor: String): TextButton

Sets the background color for `TextButtonStyle.FILLED` button. If unset for a `TextButtonStyle.FILLED` button, the button uses the secondary color defined in the add-on manifest. This method is a no-op for `TextButtonStyle.OUTLINED` buttons.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): TextButton

Sets an action that composes a draft email when the object is clicked. A UI object can only have one of `setOpenLink(openLink)`, `setOnClickAction(action)`, `setOnClickOpenLinkAction(action)`, `setAuthorizationAction(action)`, or `setComposeAction(action, composedEmailType)` set. The `Action` parameter must specify a callback function that returns a `ComposeActionResponse` object configured using `ComposeActionResponseBuilder.setGmailDraft(draft)`. Note: This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an `Action` that composes draft messages in Apps Script that are opened in Gmail when the action completes.

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

### setDisabled(disabled: Boolean): TextButton

Sets whether the button is disabled. A disabled button is greyed out and cannot be clicked.

### setIcon(icon: Icon): TextButton

Sets a predefined `Icon` to display on the button. Either this or `setIconUrl(url)` must be used to define the button image.

### setIconUrl(url: String): TextButton

Sets the URL of an image to use as this button's icon. Either this or `setIcon(icon)` must be used to define the button image.

### setMaterialIcon(icon: MaterialIcon): TextButton

Sets the material design icon.

```javascript
const textButton = CardService.newTextButton().setMaterialIcon(
    CardService.newMaterialIcon().setName('search'),
);
```

### setOnClickAction(action: Action): TextButton

Sets an action that executes when the object is clicked. A UI object can only have one of `setOpenLink(openLink)`, `setOnClickAction(action)`, `setOnClickOpenLinkAction(action)`, `setAuthorizationAction(action)`, or `setComposeAction(action, composedEmailType)` set. The `Action` parameter must specify a callback function that returns an `ActionResponse` object.

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

### setOnClickOpenLinkAction(action: Action): TextButton

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the `OpenLink` object. A UI object can only have one of `setOpenLink(openLink)`, `setOnClickAction(action)`, `setOnClickOpenLinkAction(action)`, `setAuthorizationAction(action)`, or `setComposeAction(action, composedEmailType)` set. The `Action` parameter must specify a callback function that returns an `ActionResponse` object configured using `ActionResponseBuilder.setOpenLink(openLink)`.

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

### setOpenLink(openLink: OpenLink): TextButton

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened. A UI object can only have one of `setOpenLink(openLink)`, `setOnClickAction(action)`, `setOnClickOpenLinkAction(action)`, `setAuthorizationAction(action)`, or `setComposeAction(action, composedEmailType)` set.

```javascript
const textButton = CardService.newTextButton()
                       .setText('Open Link')
                       .setOpenLink(CardService.newOpenLink().setUrl(
                           'https://www.google.com'));
```

### setOverflowMenu(menu: OverflowMenu): TextButton

Sets a pop-up menu to be opened when the object is clicked. Each item in the menu can specify an action to be triggered when clicked. Nested menus are not supported, actions for menu items should not specify an overflow menu. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

```javascript
const overflowMenuItem =
    CardService.newOverflowMenuItem()
        .setStartIcon(
            CardService.newIconImage().setIconUrl(
                'https://www.google.com/images/branding/googleg/1x/googleg_standard_color_64dp.png',
                ),
            )
        .setText('Open Link')
        .setOpenLink(
            CardService.newOpenLink().setUrl('https://www.google.com'));

const overflowMenu =
    CardService.newOverflowMenu().addMenuItem(overflowMenuItem).build();
```

### setText(text: String): TextButton

Sets the text that displays on the button.

### setTextButtonStyle(textButtonStyle: TextButtonStyle): TextButton

Sets the button style. If unset, it defaults to `TextButtonStyle.OUTLINED` button.

```javascript
const button =
    CardService.newTextButton()
        .setText('Filled')
        .setTextButtonStyle(CardService.TextButtonStyle.FILLED)
        .setOpenLink(CardService.newOpenLink().setUrl('www.google.com'));
```
