# Add-Ons Response Service — Reference Index

Offline local copy of the Google Apps Script "Add-ons Response Service" reference documentation. This service allows scripts to configure and build Google Workspace add-ons, including the newer add-on/agent response APIs used by Google Workspace Studio, Gmail, Calendar, Drive, Editors, and Google Chat.

Source: https://developers.google.com/apps-script/reference/add-ons-response-service/

## Service Entry Point

- [AddOnsResponseService](./AddOnsResponseService.md) — Top-level namespace providing factory methods (`newX()`) to create all builder and response objects in this service.

## Core Action & Response Classes

- [Action](./Action.md) — An action that Google Workspace Studio add-ons use to render a new card.
- [ActionResponse](./ActionResponse.md) — The actions that add-ons can use in cards or the host application (Chat).
- [ActionResponseBuilder](./ActionResponseBuilder.md) — Builder for `ActionResponse` objects.
- [HostAppAction](./HostAppAction.md) — An `Action` handled by individual host apps (Gmail, Chat, Drive, Calendar, Editor, Sheets, Studio, DuetAI).
- [RenderAction](./RenderAction.md) — Renders or updates a card by performing an `Action` in response to a user interaction.
- [RenderActionBuilder](./RenderActionBuilder.md) — Builder for `RenderAction` objects.
- [UniversalActionResponse](./UniversalActionResponse.md) — Response object returned from a method that creates a universal action.
- [UniversalActionResponseBuilder](./UniversalActionResponseBuilder.md) — Builder for `UniversalActionResponse` objects.

## Gmail Compose / Draft Classes

- [ComposeActionResponse](./ComposeActionResponse.md) — Response for a compose action callback in a Gmail add-on.
- [ComposeActionResponseBuilder](./ComposeActionResponseBuilder.md) — Builder for `ComposeActionResponse` objects.
- [AddonComposeUiActionResponse](./AddonComposeUiActionResponse.md) — Represents an action on the addon compose UI.
- [AddonComposeUiActionResponseBuilder](./AddonComposeUiActionResponseBuilder.md) — Builder for `AddonComposeUiActionResponse` objects.
- [UpdateDraftActionResponse](./UpdateDraftActionResponse.md) — Action that updates the email draft the user is currently editing.
- [UpdateDraftActionResponseBuilder](./UpdateDraftActionResponseBuilder.md) — Builder for `UpdateDraftActionResponse` objects.
- [UpdateDraftBccRecipientsAction](./UpdateDraftBccRecipientsAction.md) — Updates the Bcc recipients of an email draft.
- [UpdateDraftCcRecipientsAction](./UpdateDraftCcRecipientsAction.md) — Updates the Cc recipients of an email draft.
- [UpdateDraftToRecipientsAction](./UpdateDraftToRecipientsAction.md) — Updates the To recipients of an email draft.
- [UpdateDraftSubjectAction](./UpdateDraftSubjectAction.md) — Updates the subject line of an email draft.
- [UpdateDraftBodyAction](./UpdateDraftBodyAction.md) — Updates the email draft body.

## Calendar / Drive / Editor Classes

- [CalendarEventActionResponse](./CalendarEventActionResponse.md) — Response that changes the Calendar event currently being edited.
- [CalendarEventActionResponseBuilder](./CalendarEventActionResponseBuilder.md) — Builder for `CalendarEventActionResponse` objects.
- [DriveItemsSelectedActionResponse](./DriveItemsSelectedActionResponse.md) — Response that changes Drive while items are selected.
- [DriveItemsSelectedActionResponseBuilder](./DriveItemsSelectedActionResponseBuilder.md) — Builder for `DriveItemsSelectedActionResponse` objects.
- [EditorFileScopeActionResponse](./EditorFileScopeActionResponse.md) — Response that makes changes to an Editor (Docs, Sheets, Slides).
- [EditorFileScopeActionResponseBuilder](./EditorFileScopeActionResponseBuilder.md) — Builder for `EditorFileScopeActionResponse` objects.
- [Attachment](./Attachment.md) — Represents an attachment created by an add-on (e.g. for Calendar events).

## Google Chat Classes

- [ChatMessage](./ChatMessage.md) — A Google Chat message.
- [ChatDataActionsResponseBuilder](./ChatDataActionsResponseBuilder.md) — Builder for Chat `DataAction` objects.
- [DataActionsResponse](./DataActionsResponse.md) — Creates or updates a message in Google Chat.
- [CreateMessageAction](./CreateMessageAction.md) — Builder for Chat `CreateMessageAction` objects.
- [UpdateMessageAction](./UpdateMessageAction.md) — The Chat app updates text or cards in a message.
- [UpdateInlinePreviewAction](./UpdateInlinePreviewAction.md) — The Chat app previews a link in a message via one or more cards.
- [AccessoryWidget](./AccessoryWidget.md) — Builder for Chat `AccessoryWidget` objects (interactive widgets at bottom of a message).
- [Notification](./Notification.md) — Displays a notification when users submit and close a dialog.
- [Navigation](./Navigation.md) — Helper object that controls card navigation.
- [LinkPreview](./LinkPreview.md) — Card action displaying a link preview card and smart chip in the host app.
- [OpenLink](./OpenLink.md) — Represents an action to open a link with options.

## Card Modification Classes (Google Workspace Studio)

- [ModifyCard](./ModifyCard.md) — Builder that changes and updates an existing card's interface.
- [InsertSection](./InsertSection.md) — Builder for inserting a new section into a card.
- [InsertWidget](./InsertWidget.md) — Builder for inserting a new widget into a card.
- [RemoveSection](./RemoveSection.md) — Builder for removing a section from a card.
- [RemoveWidget](./RemoveWidget.md) — Builder for removing a widget from a card.
- [UpdateWidget](./UpdateWidget.md) — Builder for updating a widget in a card.

## Workflow / Google Workspace Studio Action Classes

- [WorkflowAction](./WorkflowAction.md) — A `HostAppAction` used to perform a specific action in Google Workspace Studio.
- [SaveWorkflowAction](./SaveWorkflowAction.md) — Indicates the host app should save the agent.
- [ReturnOutputVariablesAction](./ReturnOutputVariablesAction.md) — Contains output variables generated by an executed action.
- [ReturnElementErrorAction](./ReturnElementErrorAction.md) — Indicates an error occurred during element invocation.
- [ResourceRetrievedAction](./ResourceRetrievedAction.md) — Retrieves custom resource content when needed.
- [ResourceFieldsDefinitionRetrievedAction](./ResourceFieldsDefinitionRetrievedAction.md) — Retrieves the definition of a list of resource fields.
- [WorkflowValidationErrorAction](./WorkflowValidationErrorAction.md) — Indicates the host app should display a validation error.

## Workflow Data Model Classes

- [DataType](./DataType.md) — Sets the type of a variable (basic or resource type).
- [BasicDataType (enum)](./BasicDataType.md) — Basic generic data types.
- [ResourceType](./ResourceType.md) — Application-specific resource type tied to a `WorkflowResourceDefinition`.
- [ResourceData](./ResourceData.md) — Application-specific resource data (key-value pairs of variable names and `VariableData`).
- [ResourceField](./ResourceField.md) — Basic building block of a `DynamicResourceDefinition`.
- [DynamicResourceDefinition](./DynamicResourceDefinition.md) — Building block for a `ResourceFieldsDefinitionRetrievedAction`.
- [ValueMetadata](./ValueMetadata.md) — Information about the potential values of a variable.
- [VariableData](./VariableData.md) — A variable data value that can contain values of various types.
- [TimeStamp](./TimeStamp.md) — A timestamp object that can be added to a `VariableData`.

## Text Formatting Classes (Google Workspace Studio)

- [WorkflowTextFormat](./WorkflowTextFormat.md) — A block of text with rich formatting made of `TextFormatElement`s.
- [TextFormatElement](./TextFormatElement.md) — A text format element: chip, styled text, hyperlink, or list container.
- [StyledText](./StyledText.md) — Text element with styles such as bold, italic and color.
- [TextFormatChip](./TextFormatChip.md) — A clickable chip in the text format.
- [TextFormatIcon](./TextFormatIcon.md) — An icon displayed in a `TextFormatChip`.
- [Hyperlink](./Hyperlink.md) — A hyperlink element used in `TextFormatElement`.
- [ListContainer](./ListContainer.md) — Container for list items, each containing multiple `TextFormatElement`s.
- [ListItem](./ListItem.md) — A single list item containing multiple `TextFormatElement`s.
- [Link](./Link.md) — Link object from a third-party resource converted to a smart chip in the host app.
- [Color](./Color.md) — A Color object representing a color in the RGBA color space.

## Enums

- [AddonComposeUiActionType](./AddonComposeUiActionType.md) — Type of an `AddonComposeUiActionResponse`.
- [BasicDataType](./BasicDataType.md) — Basic generic data types.
- [ComposedEmailType](./ComposedEmailType.md) — Whether a composed email is standalone or a reply draft.
- [ContentType](./ContentType.md) — Content type generated by an `UpdateDraftActionResponse`.
- [EndNavigation](./EndNavigation.md) — Action during navigation (e.g. close dialog).
- [ErrorActionability](./ErrorActionability.md) — Whether an error is fixable by the user.
- [ErrorRetryability](./ErrorRetryability.md) — Whether an action invocation error is retryable.
- [FontWeight](./FontWeight.md) — Font weight of styled text.
- [ListType](./ListType.md) — Ordered or unordered list type.
- [OnClose](./OnClose.md) — Behavior when a URL opened through `OpenLink` is closed.
- [OpenAs](./OpenAs.md) — How a URL is opened (full size or overlay).
- [SendStatus](./SendStatus.md) — Send status of an `UpdateDraftActionResponse`.
- [TextStyle](./TextStyle.md) — Style of styled text (italic, underline, etc.).
- [UpdateDraftBodyType](./UpdateDraftBodyType.md) — Type of an `UpdateDraftBodyAction` (insert position).
- [ValidationErrorSeverity](./ValidationErrorSeverity.md) — Severity of a workflow validation error.

---

**Total files:** 84 classes/enums successfully fetched (out of 84 requested). No 404s encountered.
