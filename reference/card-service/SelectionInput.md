# SelectionInput

An input field that allows choosing between a set of predefined options.

An input field that allows choosing between a set of predefined options.

Supports form submission validation for `SelectionInputType.DROP_DOWN` and `SelectionInputType.MULTI_SELECT` menus only. When `Action.setAllWidgetsAreRequired(allWidgetsAreRequired)` is set to `true` or this widget is specified through `Action.addRequiredWidget(requiredWidget)`, the submission action is blocked unless a value is selected.

Available for Google Workspace add-ons and Google Chat apps.

## Methods

### addDataSourceConfig(dataSourceConfig: DataSourceConfig): SelectionInput

Sets the data source configs for the selection control. This field provides more fine-grained control over the data source. This is an optional field.

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### addItem(text: Object, value: Object, selected: Boolean): SelectionInput

Adds a new item that can be selected.

### addMultiSelectItem(text: Object, value: Object, selected: Boolean, startIconUri: Object, bottomText: Object): SelectionInput

Adds a new item that can be selected, for multi-select menus.

### setExternalDataSource(action: Action): SelectionInput

Sets external data source, such as a relational data base.

### setFieldName(fieldName: String): SelectionInput

Sets the key that identifies this selection input in the event object that is generated when there is a UI interaction. Not visible to the user. Required, must be unique.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setMultiSelectMaxSelectedItems(maxSelectedItems: Integer): SelectionInput

Sets the maximum number of items that a user can select.

### setMultiSelectMinQueryLength(queryLength: Integer): SelectionInput

Sets the number of text characters that a user inputs before the app queries autocomplete and displays suggested items on the card.

### setOnChangeAction(action: Action): SelectionInput

Sets an `Action` to be performed whenever the selection input changes.

### setPlatformDataSource(platformDataSource: PlatformDataSource): SelectionInput

Sets a data source from Google Workspace. Used to populate items in a multiselect menu. Only available for Google Chat apps, not for Google Workspace add-ons.

### setTitle(title: String): SelectionInput

Sets the title to be shown ahead of the input field.

### setType(type: SelectionInputType): SelectionInput

Sets the type of this input. Defaults to `CHECKBOX`.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.
