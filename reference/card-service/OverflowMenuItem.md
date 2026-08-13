# OverflowMenuItem

An OverflowMenuItem with an icon and text label.

An `OverflowMenuItem` with an icon and text label. You can deactivate the menu item when needed. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

OverflowMenuItem is a UI element for Google Chat apps and Google Workspace add-ons that displays an icon and text. You can set the text, starting icon, and disable the OverflowMenuItem. An OverflowMenuItem can trigger various actions when clicked, such as opening a link, executing a custom action, initiating an authorization flow, or composing an email draft. An OverflowMenuItem can only have one click action set at a time.

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
```

## Methods

### setAuthorizationAction(action: AuthorizationAction): OverflowMenuItem

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): OverflowMenuItem

Sets an action that composes a draft email when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns a ComposeActionResponse object configured using ComposeActionResponseBuilder.setGmailDraft(draft). Note: This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an Action that composes draft messages in Apps Script that are opened in Gmail when the action completes.

### setDisabled(disabled: Boolean): OverflowMenuItem

Sets whether the menu item is disabled. A disabled item is greyed out and cannot be clicked.

### setOnClickAction(action: Action): OverflowMenuItem

Sets an action that executes when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns an ActionResponse object.

### setOnClickOpenLinkAction(action: Action): OverflowMenuItem

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set. The Action parameter must specify a callback function that returns an ActionResponse object configured using ActionResponseBuilder.setOpenLink(openLink).

### setOpenLink(openLink: OpenLink): OverflowMenuItem

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

### setStartIcon(icon: IconImage): OverflowMenuItem

Sets the menu item's leading icon.

### setText(text: String): OverflowMenuItem

Sets the title of the menu item. Required.
