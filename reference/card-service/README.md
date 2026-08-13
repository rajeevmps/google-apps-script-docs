# Card Service Reference

Offline markdown copy of the Google Apps Script **Card Service** reference documentation, used to build UIs for Google Workspace Add-ons and Google Chat apps. Source: https://developers.google.com/apps-script/reference/card-service

126 classes and enums, grouped below.

## Entry Point

- [CardService](CardService.md) — Allows you to create generic cards for use in various Google extensibility products, such as Google Workspace Add-ons. The factory class for every builder and enum in this service (`CardService.newX()`, `CardService.EnumName`).

## Card Building

- [Card](Card.md) — A context card that represents a single view in the UI.
- [CardBuilder](CardBuilder.md) — A builder for Card objects.
- [CardHeader](CardHeader.md) — The header of a `Card`.
- [CardSection](CardSection.md) — A card section holds groups of widgets and provides visual separation between them.
- [CardWithId](CardWithId.md) — A builder for `CardWithId` objects.
- [CardAction](CardAction.md) — A clickable menu item added to the card header menu.
- [CollapseControl](CollapseControl.md) — A customizable collapse and expand control.
- [Carousel](Carousel.md) — Carousel, also known as slider, rotates and displays a list of widgets in a slideshow format.
- [CarouselCard](CarouselCard.md) — A card that can be displayed as a carousel item.
- [Dialog](Dialog.md) — A builder for Dialog objects.
- [DialogAction](DialogAction.md) — A builder for DialogAction objects.
- [FixedFooter](FixedFooter.md) — A component shown at the bottom of a Card, available for Google Workspace add-ons and Google Chat apps.
- [Navigation](Navigation.md) — A helper object that controls card navigation.
- [Notification](Notification.md) — A notification shown to the user as a response to interacting with a UI element.

## Widgets

- [Widget](Widget.md) — Base class for all widgets that can be added to a Card.
- [Button](Button.md) — A base class for all buttons.
- [ButtonSet](ButtonSet.md) — Holds a set of Button objects displayed in a row.
- [TextButton](TextButton.md) — A TextButton with a text label.
- [ImageButton](ImageButton.md) — An ImageButton with an image displayed on it.
- [Chip](Chip.md) — A `Chip` with an icon and text label.
- [ChipList](ChipList.md) — Holds a set of `Chip` objects that are displayed in a row.
- [Column](Column.md) — A column.
- [Columns](Columns.md) — The `Columns` widget displays up to 2 columns in a card or dialog.
- [DatePicker](DatePicker.md) — An input field that allows inputing a date.
- [DateTimePicker](DateTimePicker.md) — An input field that allows users to input a date and time.
- [TimePicker](TimePicker.md) — An input field that allows users to input a time.
- [DecoratedText](DecoratedText.md) — A widget that displays text with optional decorations.
- [Divider](Divider.md) — A horizontal divider.
- [Grid](Grid.md) — An organized grid used to display a collection of grid items.
- [GridItem](GridItem.md) — The items users interact with within a grid widget.
- [Image](Image.md) — A widget that shows a single image.
- [ImageComponent](ImageComponent.md) — An image component that can be added to grid items.
- [ImageCropStyle](ImageCropStyle.md) — A class that represents a crop style that can be applied to image components.
- [IconImage](IconImage.md) — A predefined icon, a material design icon, or an icon from a URL with a customizable crop style.
- [MaterialIcon](MaterialIcon.md) — An object that supports all Google Font Icons.
- [KeyValue](KeyValue.md) — **Deprecated.** Instead, use `DecoratedText`.
- [LinkPreview](LinkPreview.md) — Card action that displays a link preview card and smart chip in the host app.
- [OverflowMenu](OverflowMenu.md) — Holds a list of OverflowMenuItem objects that are displayed in a pop-up menu.
- [OverflowMenuItem](OverflowMenuItem.md) — An OverflowMenuItem with an icon and text label.
- [SelectionInput](SelectionInput.md) — An input field that allows choosing between a set of predefined options.
- [Suggestions](Suggestions.md) — Autocomplete suggestions to supplement a TextInput widget.
- [Switch](Switch.md) — A UI element that supports being toggled on or off.
- [TextInput](TextInput.md) — An input field widget that accepts text input.
- [TextParagraph](TextParagraph.md) — A widget that displays text and supports basic HTML formatting.
- [UpdatedWidget](UpdatedWidget.md) — The response of the updated widget.
- [Validation](Validation.md) — An object that defines the validation rule for the widget that it is attached to.

## Actions, Links & Responses

- [Action](Action.md) — An action that enables interactivity within UI elements.
- [ActionStatus](ActionStatus.md) — The status for a request to either invoke or submit a dialog.
- [AuthorizationAction](AuthorizationAction.md) — An authorization action that sends the user to an authorization URL.
- [AuthorizationException](AuthorizationException.md) — An error used to trigger an authorization card for the user.
- [OpenLink](OpenLink.md) — Represents an action to open a link with some options.
- [CommonWidgetAction](CommonWidgetAction.md) — Defines actions that don't involve evaluations, such as updating widget visibility.
- [Condition](Condition.md) — A condition used to run an event action as part of CEL expression validation.
- [EventAction](EventAction.md) — An EventAction to run when a CEL expression validation condition is met.
- [ExpressionData](ExpressionData.md) — The expression data that is used to evaluate an expression (Google Workspace Studio).
- [ExpressionDataAction](ExpressionDataAction.md) — Actions for CEL expression validation.
- [ExpressionDataCondition](ExpressionDataCondition.md) — Represents a CEL expression validation result.
- [Trigger](Trigger.md) — A trigger that runs CEL expression validation widget event actions according to the action rule ID.
- [UpdateVisibilityAction](UpdateVisibilityAction.md) — Updates the visibility of a card widget to make it display or to hide it.
- [Attachment](Attachment.md) — Represents an attachment created by an add-on.

### Response objects & builders

- [ActionResponse](ActionResponse.md) / [ActionResponseBuilder](ActionResponseBuilder.md) — The response returned from a callback function to perform one or more client actions.
- [CalendarEventActionResponse](CalendarEventActionResponse.md) / [CalendarEventActionResponseBuilder](CalendarEventActionResponseBuilder.md) — Makes changes to the calendar event the user is currently editing.
- [ChatActionResponse](ChatActionResponse.md) — Parameters that a Chat app can use to configure how its response is posted.
- [ChatResponse](ChatResponse.md) / [ChatResponseBuilder](ChatResponseBuilder.md) — The response object for a card message in Google Chat.
- [ComposeActionResponse](ComposeActionResponse.md) / [ComposeActionResponseBuilder](ComposeActionResponseBuilder.md) — The response from a compose-action callback in a Gmail add-on.
- [DriveItemsSelectedActionResponse](DriveItemsSelectedActionResponse.md) / [DriveItemsSelectedActionResponseBuilder](DriveItemsSelectedActionResponseBuilder.md) — Makes changes to Drive while Drive items are selected.
- [EditorFileScopeActionResponse](EditorFileScopeActionResponse.md) / [EditorFileScopeActionResponseBuilder](EditorFileScopeActionResponseBuilder.md) — Makes changes to an Editor (Docs, Sheets, Slides) file-scope document.
- [SuggestionsResponse](SuggestionsResponse.md) / [SuggestionsResponseBuilder](SuggestionsResponseBuilder.md) — Returned from a suggestions callback function.
- [UniversalActionResponse](UniversalActionResponse.md) / [UniversalActionResponseBuilder](UniversalActionResponseBuilder.md) — Returned from a method that creates a universal action.
- [UpdateDraftActionResponse](UpdateDraftActionResponse.md) / [UpdateDraftActionResponseBuilder](UpdateDraftActionResponseBuilder.md) — Represents an action that updates the email draft the user is currently editing.

### Draft-update actions (Gmail add-ons)

- [UpdateDraftBccRecipientsAction](UpdateDraftBccRecipientsAction.md) — Updates the Bcc recipients of an email draft.
- [UpdateDraftBodyAction](UpdateDraftBodyAction.md) — Updates the email draft body.
- [UpdateDraftCcRecipientsAction](UpdateDraftCcRecipientsAction.md) — Updates the Cc recipients of an email draft.
- [UpdateDraftSubjectAction](UpdateDraftSubjectAction.md) — Updates the subject line of an email draft.
- [UpdateDraftToRecipientsAction](UpdateDraftToRecipientsAction.md) — Updates the To recipients of an email draft.

## Data Sources

- [DataSourceConfig](DataSourceConfig.md) — A configuration object that helps configure the data sources for a widget.
- [ChatClientDataSource](ChatClientDataSource.md) — A data source for a multiselect menu in a SelectionInput widget, specific to Google Chat.
- [ChatSpaceDataSource](ChatSpaceDataSource.md) — A data source that populates Google Chat spaces as selection items for a multiselect menu.
- [DriveDataSourceSpec](DriveDataSourceSpec.md) — Holds a set of DriveItemType objects that are displayed in a row.
- [HostAppDataSource](HostAppDataSource.md) — A data source from a Google Workspace application for a multiselect menu.
- [PlatformDataSource](PlatformDataSource.md) — Used for populating items in a multiselect menu within a SelectionInput widget.
- [WorkflowDataSource](WorkflowDataSource.md) — A data source used in Google Workspace Studio for SelectionInput, DateTimePicker or TextInput widgets.

## Enums

- [BorderType](BorderType.md) — The border types that can be applied to widgets.
- [BorderStyle](BorderStyle.md) — Represents a complete border style applied to widgets (not itself an enum — a style object referencing `BorderType`).
- [ChipListLayout](ChipListLayout.md) — The layout of a ChipList.
- [CommonDataSource](CommonDataSource.md) — A data source shared by all Google Workspace applications.
- [ComposedEmailType](ComposedEmailType.md) — The type of a composed email.
- [ContentType](ContentType.md) — The content type of generated content.
- [DisplayStyle](DisplayStyle.md) — A style for displaying cards when they are pushed.
- [DriveItemType](DriveItemType.md) — The file type for a drive item.
- [ExpressionDataActionType](ExpressionDataActionType.md) — The type of the expression data action.
- [ExpressionDataConditionType](ExpressionDataConditionType.md) — Whether a CEL expression evaluated successfully.
- [GridItemLayout](GridItemLayout.md) — The image and text style of a GridItem.
- [HorizontalAlignment](HorizontalAlignment.md) — The horizontal alignment of a widget.
- [HorizontalSizeStyle](HorizontalSizeStyle.md) — How widgets fill the space of a column.
- [Icon](Icon.md) — Predefined icons usable in UI objects such as ImageButton or DecoratedText widgets.
- [ImageButtonStyle](ImageButtonStyle.md) — Styles for image buttons.
- [ImageCropType](ImageCropType.md) — The crop style applied to an image.
- [ImageStyle](ImageStyle.md) — An image cropping style.
- [InputType](InputType.md) — The input type of the widget.
- [Interaction](Interaction.md) — What to do in response to an interaction with a user, such as clicking a button in a card message.
- [LoadIndicator](LoadIndicator.md) — The type of loading/progress indicator to display while an Action is being processed.
- [OnClose](OnClose.md) — What to do when a URL opened through an OpenLink is closed.
- [OpenAs](OpenAs.md) — How to open a URL.
- [ResponseType](ResponseType.md) — The type of Chat app response.
- [SelectionInputType](SelectionInputType.md) — The format of the items that users can select.
- [Status](Status.md) — A status code.
- [SwitchControlType](SwitchControlType.md) — Type of a Switch widget control.
- [TextButtonStyle](TextButtonStyle.md) — The style of a TextButton.
- [TextInputMode](TextInputMode.md) — What type of input is allowed for a text input field.
- [UpdateDraftBodyType](UpdateDraftBodyType.md) — The type of an UpdateDraftBodyAction.
- [VariableButtonSize](VariableButtonSize.md) — The size of the variable picker button.
- [VerticalAlignment](VerticalAlignment.md) — The vertical alignment of widgets in a column.
- [Visibility](Visibility.md) — The visibility state of widgets.
- [WorkflowDataSourceType](WorkflowDataSourceType.md) — The type of the workflow data source.
- [WrapStyle](WrapStyle.md) — The wrapping style for content within a column.

---

*Generated from the official Google Apps Script Card Service reference documentation. Each file was fetched and transcribed individually; some very long pages (e.g. `CardService`, `Icon`) were fetched in multiple passes to ensure completeness. Content may occasionally be lightly paraphrased rather than character-for-character verbatim, since it passed through an automated extraction step — verify exact wording against the live docs for anything safety- or contract-critical.*
