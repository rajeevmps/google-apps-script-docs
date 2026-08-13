# TextInput

An input field widget that accepts text input.

An input field widget that accepts text input. Supports form submission validation. When `Action.setAllWidgetsAreRequired(allWidgetsAreRequired)` is set to `true` or this widget is specified through `Action.addRequiredWidget(requiredWidget)`, the submission action is blocked unless a value is entered. Available for Google Workspace add-ons and Google Chat apps.

```javascript
const textInput = CardService.newTextInput()
                      .setFieldName('text_input_form_input_key')
                      .setTitle('Text input title')
                      .setHint('Text input hint');
```

## Methods

### addEventAction(eventAction: EventAction): Widget

Adds the event action that can be performed on the widget.

### setFieldName(fieldName: String): TextInput

Sets the key that identifies this text input in the event object that is generated when there is a UI interaction. Not visible to the user. Required, must be unique.

### setHint(hint: String): TextInput

Sets a hint for the text input. Used to give the user extra guidance on what to input. For example, a hint could describe formatting ("xxx-xxx-xxxx") for a phone number field.

### setHostAppDataSource(hostAppDataSource: HostAppDataSource): TextInput

Sets a data source from Google Workspace applications. Currently supports users and Chat spaces. Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const workflowDataSource =
    CardService.newWorkflowDataSource().setIncludeVariables(true);

const hostAppDataSource =
    CardService.newHostAppDataSource().setWorkflowDataSource(workflowDataSource);

const textInput = CardService.newTextInput()
                      .setFieldName('text_input_form_input_key')
                      .setTitle('Text input title')
                      .setHint('Text input hint')
                      .setHostAppDataSource(hostAppDataSource);
```

### setId(id: String): Widget

Sets the unique ID assigned that's used to identify the widget to be mutated. Widget mutation is only supported in Add-Ons.

### setInputMode(inputMode: TextInputMode): TextInput

Sets whether this text input field supports variable insertion. Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const textInput = CardService.newTextInput()
                      .setFieldName('text_input_form_input_key')
                      .setTitle('Text input title')
                      .setInputMode(CardService.TextInputMode.PLAIN_TEXT);
```

### setMultiline(multiline: Boolean): TextInput

Sets whether the input text shows on one line or multiple lines.

### setOnChangeAction(action: Action): TextInput

Sets an action to be performed whenever the text input changes.

### setSuggestions(suggestions: Suggestions): TextInput

Sets the suggestions for autocompletion in the text field.

### setSuggestionsAction(suggestionsAction: Action): TextInput

Sets the callback action to fetch suggestions based on user input for autocompletion. The `Action` parameter must specify a callback function that returns a `SuggestionsResponse` object.

```javascript
const action = CardService.newAction()
                   .setFunctionName('suggestionCallback')
                   .setParameters({numSuggestions: 3});

CardService.newTextInput()
    .setFieldName('option-field')
    .setTitle('Option Selected')
    .setSuggestionsAction(action);

function suggestionCallback(e) {
  const suggestions = CardService.newSuggestions();
  const numSuggestions = Number.parseInt(e.parameter.numSuggestions);
  for (let i = 1; i <= numSuggestions; i++) {
    suggestions.addSuggestion(`Suggestion ${i}`);
  }
  return CardService.newSuggestionsResponseBuilder()
      .setSuggestions(suggestions)
      .build();
}
```

### setTitle(title: String): TextInput

Sets the title to be shown above the input field. Required.

### setValidation(validation: Validation): TextInput

Sets the validation rule for this widget.

```javascript
const validation = CardService.newValidation().setCharacterLimit('10').setType(
    CardService.InputType.TEXT);

const input = CardService.newTextInput()
                  .setFieldName('text_name_xxx1')
                  .setTitle('Max 10 characters')
                  .setValidation(validation);
```

### setValue(value: String): TextInput

Sets the pre-filled value to be set in the input field.

### setVisibility(visibility: Visibility): Widget

Sets the visibility of the widget. The default value is `VISIBLE`.
