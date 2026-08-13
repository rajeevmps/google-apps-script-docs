# DatePicker

An input field that allows inputing a date.

An input field that allows inputing a date. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const dateTimePicker =
    CardService.newDatePicker()
        .setTitle('Enter the date.')
        .setFieldName('date_field')
        // Set default value as Jan 1, 2018 UTC. Either a number or string is
        // acceptable.
        .setValueInMsSinceEpoch(1514775600)
        .setOnChangeAction(
            CardService.newAction().setFunctionName('handleDateTimeChange'),
        );
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setFieldName(fieldName: String): DatePicker

Sets the field name that identifies this picker in the event object that is generated when there is a UI interaction. The field name is visible to the user. Required; the specified field name must be unique.

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setOnChangeAction(action: Action): DatePicker

Sets an Action that the script performs whenever the picker input changes.

### setTitle(title: String): DatePicker

Sets the title displayed above the input field.

### setValueInMsSinceEpoch(valueMsEpoch: Number): DatePicker

Sets the prefilled value to be set in the input field.

### setValueInMsSinceEpoch(valueMsEpoch: String): DatePicker

Sets the prefilled value to be set in the input field.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.
