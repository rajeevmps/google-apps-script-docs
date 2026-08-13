# Image

A widget that shows a single image. For information about cropping images, see `ImageCropStyle`.

Available for Google Workspace add-ons and Google Chat apps.

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

Parameters:
- `eventAction` (EventAction) - The EventAction to be added.

### setAltText(altText: String): Image

Sets the alternative text of the image for accessibility. Required.

Parameters:
- `altText` (String) - The alternative text to assign to this image.

### setAuthorizationAction(action: AuthorizationAction): Image

Sets an authorization action that opens a URL to the authorization flow when the object is clicked. This opens the URL in a new window. When the user finishes the authorization flow and returns to the application, the add-on reloads.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `action` (AuthorizationAction) - The object that specifies the authorization action to take when this element is clicked.

### setComposeAction(action: Action, composedEmailType: ComposedEmailType): Image

Sets an action that composes a draft email when the object is clicked.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

This method doesn't set a compose action that is used to extend the compose UI. Rather, this method connects this UI element to an Action that composes draft messages in Apps Script that are opened in Gmail when the action completes.

Parameters:
- `action` (Action) - The object that specifies the compose action to take when this element is clicked.
- `composedEmailType` (ComposedEmailType) - An enum value that specifies whether the composed draft is a standalone or reply draft.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

Parameters:
- `id` (String) - The id of the widget, with a limit of 64 characters and in format of `[a-zA-Z0-9-]+`.

### setImageUrl(url: String): Image

Sets the image to use by providing its URL or data string. Required.

The provided URL can either be a publicly accessible URL or a base64 encoded image string.

Parameters:
- `url` (String) - The URL address of a hosted image to use, or an encoded image string.

### setOnClickAction(action: Action): Image

Sets an action that executes when the object is clicked.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

The Action parameter must specify a callback function that returns a ActionResponse object.

Parameters:
- `action` (Action) - The action to take when this element is clicked.

### setOnClickOpenLinkAction(action: Action): Image

Sets an action that opens a URL in a tab when the object is clicked. Use this function when the URL needs to be built or when you need to take other actions in addition to creating the OpenLink object.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

The Action parameter must specify a callback function that returns a ActionResponse object configured using ActionResponseBuilder.setOpenLink(openLink).

Parameters:
- `action` (Action) - The object that specifies the open link action to take when this element is clicked.

### setOpenLink(openLink: OpenLink): Image

Sets a URL to be opened when the object is clicked. Use this function when the URL is already known and only needs to be opened.

A UI object can only have one of setOpenLink(openLink), setOnClickAction(action), setOnClickOpenLinkAction(action), setAuthorizationAction(action), or setComposeAction(action, composedEmailType) set.

Parameters:
- `openLink` (OpenLink) - An OpenLink object describing the URL to open.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.

Parameters:
- `visibility` (Visibility) - The Visibility of the widget.

```javascript
const image = CardService.newImage()
                  .setAltText('A nice image')
                  .setImageUrl('https://image.png');
```
