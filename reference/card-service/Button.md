# Button

A base class for all buttons.

A base class for all buttons. Available for Google Workspace add-ons and Google Chat apps.

A button can only have one click action set at a time from the `setOpenLink`, `setOnClickAction`, `setOnClickOpenLinkAction`, `setAuthorizationAction`, or `setComposeAction` methods.

## Methods

### setAuthorizationAction(action: AuthorizationAction): Button

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads.

A UI object can only have one of the five action methods (`setOpenLink`, `setOnClickAction`, `setOnClickOpenLinkAction`, `setAuthorizationAction`, `setComposeAction`) set at once.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): Button

Sets an action that composes a draft email when the object is clicked. The action parameter must specify a callback returning a `ComposeActionResponse` object.

Note: This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an Action that composes draft messages in Apps Script that are opened in Gmail when the action completes.

### setOnClickAction(action: Action): Button

Sets an action that executes when the object is clicked. The Action parameter must specify a callback returning an `ActionResponse` object.

### setOnClickOpenLinkAction(action: Action): Button

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object. The callback must return an `ActionResponse` configured with `setOpenLink()`.

### setOpenLink(openLink: OpenLink): Button

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened.

### setOverflowMenu(menu: OverflowMenu): Button

Sets a pop-up menu to be opened when the object is clicked. Each item in the menu can specify an action to be triggered when clicked. Nested menus are not supported, actions for menu items should not specify an overflow menu.

Available for Google Chat apps; in developer preview for Google Workspace add-ons.
