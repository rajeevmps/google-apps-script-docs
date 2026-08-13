# Chip

A `Chip` with an icon and text label.

A `Chip` with an icon and text label. You can deactivate the chip when needed. Available for Google Chat apps. In developer preview for Google Workspace add-ons.

```javascript
const chip = CardService.newChip()
                 .setLabel('Open Link')
                 .setOpenLink(CardService.newOpenLink().setUrl(
                     'https://www.google.com'));
```

## Methods

### setAltText(altText: String): Chip

Sets the alternative text of the chip for accessibility. If unset, defaults to the text that displays on the chip.

### setAuthorizationAction(action: AuthorizationAction): Chip

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): Chip

Sets an action that composes a draft email when the object is clicked.

### setDisabled(disabled: Boolean): Chip

Sets whether the chip is disabled. A disabled chip is greyed out and cannot be clicked.

### setIcon(icon: IconImage): Chip

Sets the icon to be used as the chip.

### setLabel(label: String): Chip

Sets the title of the chip. Required.

### setOnClickAction(action: Action): Chip

Sets an action that executes when the object is clicked.

### setOnClickOpenLinkAction(action: Action): Chip

Sets an action that opens a URL in a tab when the object is clicked.

### setOpenLink(openLink: OpenLink): Chip

Sets a URL to be opened when the object is clicked.
