# DateTimePicker

An input field that allows users to input a date and time.

An input field that allows users to input a date and time. Supports form submission validation. When `Action.setAllWidgetsAreRequired(allWidgetsAreRequired)` is set to `true` or this widget is specified through `Action.addRequiredWidget(requiredWidget)`, the submission action is blocked unless a value is selected. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const dateTimePicker = CardService.newDateTimePicker()
    .setTitle('Enter the date and time.')
    .setFieldName('date_time_field')
    .setValueInMsSinceEpoch(1514775600)
    .setTimeZoneOffsetInMins(-5 * 60)
    .setOnChangeAction(
        CardService.newAction().setFunctionName('handleDateTimeChange'),
    );
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setFieldName(fieldName: String): DateTimePicker

Sets the field name that identifies this picker in the event object that is generated when there is a UI interaction. The field name is visible to the user. Required; the specified field name must be unique.

### setHostAppDataSource(hostAppDataSource: HostAppDataSource): DateTimePicker

In a Google Workspace Studio agent, lets input variables accept datetime outputs from other steps. Only available for Google Workspace add-ons that extend Google Workspace Studio.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setOnChangeAction(action: Action): DateTimePicker

Sets an Action that the script performs whenever the picker input changes.

### setTimeZoneOffsetInMins(timeZoneOffsetMins: Integer): DateTimePicker

Sets the number of minutes that the time zone should be offset from UTC. If set, the date and time is displayed in the specified time zone. If not set, the time is displayed in the user's time zone.

### setTitle(title: String): DateTimePicker

Sets the title displayed above the input field.

### setValueInMsSinceEpoch(valueMsEpoch: Number): DateTimePicker

Sets the prefilled value to be set in the input field.

### setValueInMsSinceEpoch(valueMsEpoch: String): DateTimePicker

Sets the prefilled value to be set in the input field.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.
