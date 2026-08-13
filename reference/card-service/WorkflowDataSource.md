# WorkflowDataSource

For a SelectionInput, DateTimePicker or TextInput widget, a data source used in Google Workspace Studio.

For a `SelectionInput`, `DateTimePicker` or `TextInput` widget, a data source used in Google Workspace Studio. The data source populates available options for a widget.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const workflowDataSource = CardService.newWorkflowDataSource()
  .setIncludeVariables(true)
  .setType(CardService.WorkflowDataSourceType.USER);
```

## Methods

### setIncludeVariables(includeVariables: Boolean): WorkflowDataSource

Whether to include variables from the previous step in the data source.

Parameters:
- `includeVariables` (Boolean): Whether to include variables from the previous step in the data source.

Returns: This object, for chaining.

### setType(type: WorkflowDataSourceType): WorkflowDataSource

Sets the type of the workflow data source.

Parameters:
- `type` (WorkflowDataSourceType): The type of the workflow data source.

Returns: This object, for chaining.

### setVariableButtonLabel(variableButtonLabel: String): WorkflowDataSource

Sets the label of the variable picker button, which displays after the `+` sign in FULL_SIZE button size.

Parameters:
- `variableButtonLabel` (String): The label of the variable picker button.

Returns: This object, for chaining.

### setVariableButtonSize(variableButtonSize: VariableButtonSize): WorkflowDataSource

Sets the size of the variable picker button, Workflow automatically uses COMPACT in side panel and FULL_SIZE in other cases if UNSPECIFIED is selected. A COMPACT button only displays the `+` sign.

Parameters:
- `variableButtonSize` (VariableButtonSize): The size of the variable picker button.

Returns: This object, for chaining.
