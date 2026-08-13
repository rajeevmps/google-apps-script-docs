# ImageButton

An ImageButton with an image displayed on it. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setAltText(altText: String): ImageButton

Sets the alternative text of the button for accessibility. Required.

Parameters:
- `altText` (String) - The alternative text to assign to this button.

Returns: This object, for chaining.

### setAuthorizationAction(action: AuthorizationAction): ImageButton

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `action` (AuthorizationAction) - The object that specifies the authorization action to take when this element is clicked.

Returns: This object, for chaining.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): ImageButton

Sets an action that composes a draft email when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

The Action parameter must specify a callback function that returns a ComposeActionResponse object configured using ComposeActionResponseBuilder.setGmailDraft(draft).

Note: This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an Action that composes draft messages in Apps Script that are opened in Gmail when the action completes.

Parameters:
- `action` (Action) - The object that specifies the compose action to take when this element is clicked.
- `composedEmailType` (ComposedEmailType) - An enum value that specifies whether the composed draft is a standalone or reply draft.

Returns: This object, for chaining.

### setIcon(icon: Icon): ImageButton

Sets a predefined Icon to display on the button. Either this or setIconUrl(url) must be used to define the button image.

Parameters:
- `icon` (Icon) - One of the predefined Icon values.

Returns: This object, for chaining.

### setIconUrl(url: String): ImageButton

Sets the URL of an image to use as this button's icon. Either this or setIcon(icon) must be used to define the button image.

Parameters:
- `url` (String) - The URL address of a hosted image to use as this button's icon.

Returns: This object, for chaining.

### setImageButtonStyle(imageButtonStyle: ImageButtonStyle): ImageButton

Sets the button style. If unset, it defaults to ImageButtonStyle.BORDERLESS button.

Available for Google Chat apps. In developer preview for Google Workspace add-ons.

Parameters:
- `imageButtonStyle` (ImageButtonStyle) - The button style.

Returns: This object, for chaining.

### setMaterialIcon(icon: MaterialIcon): ImageButton

Sets the material design icon.

Parameters:
- `icon` (MaterialIcon) - The material design icon.

Returns: This object, for chaining.

### setOnClickAction(action: Action): ImageButton

Sets an action that executes when the object is clicked. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

The Action parameter must specify a callback function that returns an ActionResponse object.

Parameters:
- `action` (Action) - The action to take when this element is clicked.

Returns: This object, for chaining.

### setOnClickOpenLinkAction(action: Action): ImageButton

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

The Action parameter must specify a callback function that returns an ActionResponse object configured using ActionResponseBuilder.setOpenLink(openLink).

Parameters:
- `action` (Action) - The object that specifies the open link action to take when this element is clicked.

Returns: This object, for chaining.

### setOpenLink(openLink: OpenLink): ImageButton

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened. A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `openLink` (OpenLink) - An OpenLink object describing the URL to open.

Returns: This object, for chaining.

### setOverflowMenu(menu: OverflowMenu): ImageButton

Sets a pop-up menu to be opened when the object is clicked. Each item in the menu can specify an action to be triggered when clicked. Nested menus are not supported, actions for menu items should not specify an overflow menu.

Available for Google Chat apps. In developer preview for Google Workspace add-ons.

Parameters:
- `menu` (OverflowMenu) - The object that specifies the overflow menu to display when this element is clicked.

Returns: This object, for chaining.
