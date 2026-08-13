# Switch

A UI element that supports being toggled on or off.

A UI element that supports being toggled on or off. This can only be used within a `DecoratedText` widget. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### setControlType(controlType: SwitchControlType): Switch

Sets the control type of the switch. Defaults to `SWITCH`.

### setFieldName(fieldName: String): Switch

Sets the key that identifies this switch in the event object that is generated when there is a UI interaction. Not visible to the user. Required. Unlike other form fields, this field name does not need to be unique. The form input values for switches using the same field name are returned as an array. The array consists of the values for all enabled switches with that field name.

### setOnChangeAction(action: Action): Switch

Sets the action to take when the switch is toggled.

### setSelected(selected: Boolean): Switch

Sets whether this switch should start as selected or unselected.

### setValue(value: String): Switch

Sets the value that is sent as the form input when this switch is toggled on. When this is sent to the form callback, it is always represented as a string.

```javascript
const switchDecoratedText =
    CardService.newDecoratedText()
        .setTopLabel('Switch decorated text widget label')
        .setText('This is a decorated text widget with a switch on the right')
        .setWrapText(true)
        .setSwitchControl(
            CardService.newSwitch()
                .setFieldName('form_input_switch_key')
                .setValue('form_input_switch_value')
                .setOnChangeAction(
                    CardService.newAction().setFunctionName(
                        'handleSwitchChange'),
                    ),
        );
```
