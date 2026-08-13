# CardService

Allows you to create generic cards for use in various Google extensibility products, such as Google Workspace Add-ons.

CardService allows you to create generic cards for use in various Google extensibility products like Google Workspace add-ons. The service enables developers to build cards with headers, text, images, and interactive components including buttons, sections, and input fields. Cards can be returned individually or as arrays.

## Methods

### newAction(): Action
Creates a new Action.

### newActionResponseBuilder(): ActionResponseBuilder
Creates a new ActionResponseBuilder.

### newActionStatus(): ActionStatus
Creates a new ActionStatus.

### newAttachment(): Attachment
Creates a new Attachment.

### newAuthorizationAction(): AuthorizationAction
Creates a new AuthorizationAction.

### newAuthorizationException(): AuthorizationException
Creates a new AuthorizationException.

### newBorderStyle(): BorderStyle
Creates a new BorderStyle.

### newButtonSet(): ButtonSet
Creates a new ButtonSet.

### newCalendarEventActionResponseBuilder(): CalendarEventActionResponseBuilder
Creates a new CalendarEventActionResponseBuilder.

### newCardAction(): CardAction
Creates a new CardAction.

### newCardBuilder(): CardBuilder
Creates a new Card builder.

### newCardHeader(): CardHeader
Creates a new CardHeader.

### newCardSection(): CardSection
Creates a new CardSection.

### newCardWithId(): CardWithId
Creates a new CardWithId.

### newCarousel(): Carousel
Creates a Carousel.

### newCarouselCard(): CarouselCard
Creates a new CarouselCard.

### newChatActionResponse(): ChatActionResponse
Creates a new ChatActionResponse.

### newChatResponseBuilder(): ChatResponseBuilder
Creates a new ChatResponseBuilder.

### newChip(): Chip
Creates a new Chip.

### newChipList(): ChipList
Creates a new ChipList.

### newCollapseControl(): CollapseControl
Creates a new CollapseControl.

### newColumn(): Column
Creates a new Column.

### newColumns(): Columns
Creates a new set of Columns.

### newCommonWidgetAction(): CommonWidgetAction
Creates a new CommonWidgetAction.

### newComposeActionResponseBuilder(): ComposeActionResponseBuilder
Creates a new ComposeActionResponseBuilder.

### newCondition(): Condition
Creates a new Condition used for client-side validation.

### newDataSourceConfig(): DataSourceConfig
Creates a new, empty DataSourceConfig.

### newDatePicker(): DatePicker
Creates a new DatePicker.

### newDateTimePicker(): DateTimePicker
Creates a new DateTimePicker.

### newDecoratedText(): DecoratedText
Creates a new DecoratedText.

### newDialog(): Dialog
Creates a new Dialog.

### newDialogAction(): DialogAction
Creates a new DialogAction.

### newDivider(): Divider
Creates a new Divider.

### newDriveDataSourceSpec(): DriveDataSourceSpec
Creates a new DriveDataSourceSpec.

### newDriveItemsSelectedActionResponseBuilder(): DriveItemsSelectedActionResponseBuilder
Creates a new DriveItemsSelectedActionResponseBuilder.

### newEditorFileScopeActionResponseBuilder(): EditorFileScopeActionResponseBuilder
Creates a new EditorFileScopeActionResponseBuilder.

### newEventAction(): EventAction
Creates a new EventAction used for client-side validation.

### newExpressionData(): ExpressionData
Creates a new ExpressionData used for client-side validation.

### newExpressionDataAction(): ExpressionDataAction
Creates a new ExpressionDataAction used for client-side validation.

### newExpressionDataCondition(): ExpressionDataCondition
Creates a new ExpressionDataCondition used for client-side validation.

### newFixedFooter(): FixedFooter
Creates a new FixedFooter.

### newGrid(): Grid
Creates a new Grid.

### newGridItem(): GridItem
Creates a new GridItem.

### newHostAppDataSource(): HostAppDataSource
Creates a new HostAppDataSource.

### newIconImage(): IconImage
Creates a new IconImage.

### newImage(): Image
Creates a new Image.

### newImageButton(): ImageButton
Creates a new ImageButton.

### newImageComponent(): ImageComponent
Creates a new ImageComponent.

### newImageCropStyle(): ImageCropStyle
Creates a new ImageCropStyle.

### newKeyValue(): KeyValue
Creates a new KeyValue.

### newLinkPreview(): LinkPreview
Creates a new LinkPreview.

### newMaterialIcon(): MaterialIcon
Creates a new MaterialIcon.

### newNavigation(): Navigation
Creates a new Navigation.

### newNotification(): Notification
Creates a new Notification.

### newOpenLink(): OpenLink
Creates a new OpenLink.

### newOverflowMenu(): OverflowMenu
Creates a new OverflowMenu.

### newOverflowMenuItem(): OverflowMenuItem
Creates a new OverflowMenuItem.

### newPlatformDataSource(): PlatformDataSource
Creates a new PlatformDataSource.

### newSelectionInput(): SelectionInput
Creates a new SelectionInput.

### newSuggestions(): Suggestions
Creates a new Suggestions.

### newSuggestionsResponseBuilder(): SuggestionsResponseBuilder
Creates a new SuggestionsResponseBuilder.

### newSwitch(): Switch
Creates a new Switch.

### newTextButton(): TextButton
Creates a new TextButton.

### newTextInput(): TextInput
Creates a new TextInput.

### newTextParagraph(): TextParagraph
Creates a new TextParagraph.

### newTimePicker(): TimePicker
Creates a new TimePicker.

### newTrigger(): Trigger
Creates and returns a new Trigger used for client-side validation.

### newUniversalActionResponseBuilder(): UniversalActionResponseBuilder
Creates a new UniversalActionResponseBuilder.

### newUpdateDraftActionResponseBuilder(): UpdateDraftActionResponseBuilder
Creates a new UpdateDraftActionResponseBuilder.

### newUpdateDraftBccRecipientsAction(): UpdateDraftBccRecipientsAction
Creates a new UpdateDraftBccRecipientsAction.

### newUpdateDraftBodyAction(): UpdateDraftBodyAction
Creates a new UpdateDraftBodyAction.

### newUpdateDraftCcRecipientsAction(): UpdateDraftCcRecipientsAction
Creates a new UpdateDraftCcRecipientsAction.

### newUpdateDraftSubjectAction(): UpdateDraftSubjectAction
Creates a new UpdateDraftSubjectAction.

### newUpdateDraftToRecipientsAction(): UpdateDraftToRecipientsAction
Creates a new UpdateDraftToRecipientsAction.

### newUpdateVisibilityAction(): UpdateVisibilityAction
Creates a new UpdateVisibilityAction.

### newValidation(): Validation
Creates a new Validation used for client-side validation.

### newWorkflowDataSource(): WorkflowDataSource
Creates a new WorkflowDataSource.

## Properties

CardService also exposes every enum in the service as a static property (namespace), so enum values are accessed as `CardService.<EnumName>.<VALUE>` (e.g. `CardService.Icon.EMAIL`). The following properties are listed on the reference page:

| Property | Type | Description |
|----------|------|-------------|
| BorderType | BorderType | The `BorderType` enumeration. |
| ChipListLayout | ChipListLayout | The `ChipListLayout` enumeration. |
| CommonDataSource | CommonDataSource | The `CommonDataSource` enumeration. |
| ComposedEmailType | ComposedEmailType | The `ComposedEmailType` enumeration. |
| ContentType | ContentType | The `ContentType` enumeration. |
| DriveItemType | DriveItemType | The `DriveItemType` enumeration. |
| ExpressionDataActionType | ExpressionDataActionType | The `ExpressionDataActionType` enumeration. |
| ExpressionDataConditionType | ExpressionDataConditionType | The `ExpressionDataConditionType` enumeration. |
| GridItemLayout | GridItemLayout | The `GridItemLayout` enumeration. |
| HorizontalAlignment | HorizontalAlignment | The `HorizontalAlignment` enumeration. |
| Icon | Icon | The `Icon` enumeration. |
| ImageButtonStyle | ImageButtonStyle | The `ImageButtonStyle` enumeration. |
| ImageCropType | ImageCropType | The `ImageCropType` enumeration. |
| ImageStyle | ImageStyle | The `ImageStyle` enumeration. |
| InputType | InputType | The `InputType` enumeration. |
| LoadIndicator | LoadIndicator | The `LoadIndicator` enumeration. |
| OnClose | OnClose | The `OnClose` enumeration. |
| OpenAs | OpenAs | The `OpenAs` enumeration. |
| SelectionInputType | SelectionInputType | The `SelectionInputType` enumeration. |
| TextButtonStyle | TextButtonStyle | The `TextButtonStyle` enumeration. |
| TextInputMode | TextInputMode | The `TextInputMode` enumeration. |
| UpdateDraftBodyType | UpdateDraftBodyType | The `UpdateDraftBodyType` enumeration. |
| VariableButtonSize | VariableButtonSize | The `VariableButtonSize` enumeration. |
| Visibility | Visibility | The `Visibility` enumeration. |
| WorkflowDataSourceType | WorkflowDataSourceType | The `WorkflowDataSourceType` enumeration. |

Note: `HorizontalSizeStyle`, `Interaction`, `ResponseType`, `Status`, `SwitchControlType`, `VerticalAlignment`, and `WrapStyle` are also enums in this service (see their individual reference files) but were not captured in the CardService Properties table extraction above; consult CardService.<EnumName> for access if not listed here.
