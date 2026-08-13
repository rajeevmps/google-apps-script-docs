# Action

An action that enables interactivity within UI elements.

An action that enables interactivity within UI elements. The action does not happen directly on the client but rather invokes an Apps Script callback function with optional parameters. Available for Google Workspace add-ons and Google Chat apps.

## Methods

### addRequiredWidget(requiredWidget): Action

Adds the names of the widgets that this Action needs for a valid submission. If the widgets in this list don't have a value when this Action is invoked, the form submission is aborted.

Parameters:
- `requiredWidget` (String): The name of the widget required by this Action.

Returns: This object, for chaining.

### setAllWidgetsAreRequired(allWidgetsAreRequired): Action

Indicates whether this Action requires inputs from all widgets.

Parameters:
- `allWidgetsAreRequired` (Boolean): Whether the action requires inputs from all widgets. Defaults to `false`.

Returns: This object, for chaining.

### setFunctionName(functionName): Action

Sets the name of the callback function to be called. Required.

Parameters:
- `functionName` (String): The name of the function. You can use functions from included libraries, such as `Library.libFunction1`.

Returns: This object, for chaining.

### setInteraction(interaction): Action

Sets the interaction with a user, only required when opening a dialog. If unspecified, the app responds by executing an Action like opening a link or running a function—as normal.

Only available for Google Chat apps.

Parameters:
- `interaction` (Interaction): The interaction to specify.

Returns: This object, for chaining.

### setLoadIndicator(loadIndicator): Action

Sets the loading indicator that displays while the action is in progress.

Parameters:
- `loadIndicator` (LoadIndicator): The indicator to display.

Returns: This object, for chaining.

### setParameters(parameters): Action

Allows custom parameters to be passed to the callback function. Optional.

Parameters:
- `parameters` (Object): Both keys and values must be strings.

Returns: This object, for chaining.

### setPersistValues(persistValues): Action

Indicates whether form values are determined by the client's values or the server's values after an action response updates the form's Card. When set to true, the client's values persist after the server response. When set to false, the server's values overwrite the form values. Defaults to false.

Parameters:
- `persistValues` (Boolean): Whether to persist values. Defaults to `false`.

Returns: This object, for chaining.

### setMethodName(functionName): Action

**Deprecated.** Legacy alias for `setFunctionName(functionName)`.

Parameters:
- `functionName` (String): The name of the function. You can use functions from included libraries, such as `Library.libFunction1`.

Returns: This object, for chaining.
