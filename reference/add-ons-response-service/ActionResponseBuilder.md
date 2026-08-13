# ActionResponseBuilder

A builder for `ActionResponse` objects.

A builder for `ActionResponse` objects. Available for Google Workspace add-ons.

## Methods

### addModifyCard(modifyCard)

`addModifyCard(modifyCard: ModifyCard): ActionResponseBuilder`

Sets the modify card operation to the action.

### build()

`build(): ActionResponse`

Builds the current action response and validates it.

**Throws:** Error if the constructed action response isn't valid.

### setLinkPreview(linkPreview)

`setLinkPreview(linkPreview: LinkPreview): ActionResponseBuilder`

Sets the LinkPreview to the action.

### setNavigation(navigation)

`setNavigation(navigation: Navigation): ActionResponseBuilder`

Sets the response to a Navigation action.

### setNotification(notification)

`setNotification(notification: Notification): ActionResponseBuilder`

Sets the notification to display when the action is activated.

### setOpenLink(openLink)

`setOpenLink(openLink: OpenLink): ActionResponseBuilder`

Sets the URL to navigate to when the action is activated.

### setStateChanged(stateChanged)

`setStateChanged(stateChanged: Boolean): ActionResponseBuilder`

Sets a flag to indicate that this action changed the existing data state. When this flag is set to true, services such as Gmail can attempt to clear any cached state data. Defaults to `false`.

## Code Sample

```javascript
const notification = AddOnsResponseService.newNotification()
    .setText("You closed a dialog!");

const navigation = AddOnsResponseService.newNavigation()
    .setEndNavigation(AddOnsResponseService.EndNavigation.CLOSE_DIALOG);

const action = AddOnsResponseService.newActionResponseBuilder()
    .setNavigation(navigation)
    .setNotification(notification)
    .build();
```
