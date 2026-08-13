# CardAction

A clickable menu item added to the card header menu.

CardAction is a clickable menu item added to the card header menu. It represents "A clickable menu item that is added to the card header menu."

CardAction objects can be configured to perform various actions when clicked, including opening authorization flows, composing emails, executing defined actions, or opening URLs. A CardAction can only have one click action type set at a time.

## Methods

### setAuthorizationAction(action: AuthorizationAction): CardAction

Sets an authorization action that opens a URL to the authorization flow when clicked, opening the URL in a new window. When users finish the authorization flow and return, the add-on reloads. A UI object can only have one of: `setOpenLink()`, `setOnClickAction()`, `setOnClickOpenLinkAction()`, `setAuthorizationAction()`, or `setComposeAction()` set.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): CardAction

Sets an action that composes a draft email when clicked. Connects the UI element to an Action that composes draft messages in Apps Script that open in Gmail upon completion. A UI object can only have one click action type set at a time.

### setOnClickAction(action: Action): CardAction

Sets an action that executes when clicked. The Action parameter must specify a callback function returning an ActionResponse object. A UI object can only have one of the five possible click action types set.

### setOnClickOpenLinkAction(action: Action): CardAction

Sets an action that opens a URL in a tab when clicked. Use this when the URL must be built or additional actions needed. The Action parameter must specify a callback returning an ActionResponse configured with `setOpenLink()`. Only one click action type allowed per UI object.

### setOpenLink(openLink: OpenLink): CardAction

Sets a URL to be opened when clicked. Use this when the URL is already known and only needs to be opened. A UI object can only have one of the five possible click action types set.

### setText(text: String): CardAction

Sets the menu text for this action.
