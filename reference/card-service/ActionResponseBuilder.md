# ActionResponseBuilder

A builder for ActionResponse objects.

ActionResponseBuilder is a builder class for constructing `ActionResponse` objects in Google Apps Script's Card Service. The `build()` method constructs and validates the ActionResponse, while methods like `setNavigation`, `setNotification`, `setOpenLink`, and `setStateChanged` configure the action response behavior.

## Methods

### build(): ActionResponse

Builds the current action response and validates it.

Returns: ActionResponse — A validated ActionResponse object.

Throws: Error if the constructed action response isn't valid.

### setNavigation(navigation): ActionResponseBuilder

Sets the response to a Navigation action.

Parameters:
- `navigation` (Navigation): The Navigation to use.

Returns: This object, for chaining.

### setNotification(notification): ActionResponseBuilder

Sets the notification to display when the action is activated.

Parameters:
- `notification` (Notification): The Notification to use.

Returns: This object, for chaining.

### setOpenLink(openLink): ActionResponseBuilder

Sets the URL to navigate to when the action is activated.

Parameters:
- `openLink` (OpenLink): The OpenLink to use.

Returns: This object, for chaining.

### setStateChanged(stateChanged): ActionResponseBuilder

Sets a flag to indicate that this action changed the existing data state. For example, if the action created a task or updated contact information. When this flag is set to true, services such as Gmail can attempt to clear any cached state data associated with this action.

Parameters:
- `stateChanged` (Boolean): Whether this action changed data state; defaults to false.

Returns: This object, for chaining.
