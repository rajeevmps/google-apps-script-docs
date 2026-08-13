# Validation

An object that defines the validation rule for the widget that it is attached to.

An object that defines the validation rule for the widget that it is attached to.

Available for Google Chat apps and Google Workspace add-ons.

```javascript
const validation = CardService.newValidation().setCharacterLimit('10').setInputType(
    CardService.InputType.TEXT);
```

## Methods

### setCharacterLimit(characterLimit: Integer): Validation

Sets the character limit of the widget. Available for Google Chat apps and Google Workspace add-ons.

Parameters:
- `characterLimit` (Integer): The character limit to set. Note that this restriction is only effective for `TextInput` and is ignored for other widgets.

Returns: This object, for chaining.

### setInputType(inputType: InputType): Validation

Sets the input type of the widget. Available for Google Chat apps and Google Workspace add-ons.

Parameters:
- `inputType` (InputType): The `InputType` to set.

Returns: This object, for chaining.
