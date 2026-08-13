# TimePicker

An input field that allows users to input a time.

An input field that allows users to input a time. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const dateTimePicker =
    CardService.newTimePicker()
        .setTitle('Enter the time.')
        .setFieldName('time_field')
        // Set default value as 3:30 AM.
        .setHours(3)
        .setMinutes(30)
        .setOnChangeAction(
            CardService.newAction().setFunctionName('handleDateTimeChange'),
        );
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setFieldName(fieldName: String): TimePicker

Sets the field name that identifies this picker in the event object generated when UI interaction occurs. Required; must be unique.

### setHours(hours: Integer): TimePicker

Sets prefilled hours value in input field. Range 0-23, always represented as string in form callback parameters.

### setId(id: String): Widget

Sets unique ID identifying widget for mutation (Add-Ons only). Limited to 64 characters, format: `[a-zA-Z0-9-]+`.

### setMinutes(minutes: Integer): TimePicker

Sets prefilled minutes value in input field. Range 0-59, always represented as string in form callback parameters.

### setOnChangeAction(action: Action): TimePicker

Sets an Action the script performs whenever picker input changes.

### setTitle(title: String): TimePicker

Sets the title displayed above the input field.

### setVisibility(visibility: Visibility): Widget

Sets widget visibility. Default value is VISIBLE.
