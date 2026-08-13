# ChatDataActionsResponseBuilder

A builder for Chat `DataAction` objects.

A builder for Chat `DataAction` objects. Available for Google Workspace add-ons that extend Google Chat.

## Methods

### build()

`build(): DataActionsResponse`

Builds the current action response.

### setCreateChatMessageAction(createMessageAction)

`setCreateChatMessageAction(createMessageAction: CreateMessageAction): ChatDataActionsResponseBuilder`

Sets the `CreateMessageAction` for this `DataActionsResponse`.

**Parameters**
- `createMessageAction` (CreateMessageAction) — The create message action to use.

### setUpdateChatMessageAction(updateMessageAction)

`setUpdateChatMessageAction(updateMessageAction: UpdateMessageAction): ChatDataActionsResponseBuilder`

Sets the `UpdateMessageAction` for this `DataActionsResponse`.

**Parameters**
- `updateMessageAction` (UpdateMessageAction) — The update message action to use.

### setUpdateInlinePreviewAction(updateInlinePreviewAction)

`setUpdateInlinePreviewAction(updateInlinePreviewAction: UpdateInlinePreviewAction): ChatDataActionsResponseBuilder`

Sets the `UpdateInlinePreviewAction` for this `DataActionsResponse`.

**Parameters**
- `updateInlinePreviewAction` (UpdateInlinePreviewAction) — The update inline preview to use.

## Code Samples

Three complete code examples are provided in the documentation demonstrating usage of `setCreateChatMessageAction()`, `setUpdateChatMessageAction()`, and `setUpdateInlinePreviewAction()` methods.
