# VariableData

Represents a variable data which can contain a collection of values in various types.

Represents a variable data which can contain a collection of values in various types. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

| Method | Return Type | Description |
|--------|-------------|-------------|
| `addBooleanValue(value: Boolean)` | `VariableData` | Adds a boolean value to the variable data. |
| `addEmailAddress(emailAddress: String)` | `VariableData` | Adds an email address to the variable data. |
| `addFloatValue(value: Number)` | `VariableData` | Adds a float value to the variable data. |
| `addGoogleUser(googleUser: String)` | `VariableData` | Adds a google user to the variable data. Parameter should have format of "user/xxxx". |
| `addIntegerValue(value: Integer)` | `VariableData` | Adds an integer value to the variable data. |
| `addResourceData(resourceData: ResourceData)` | `VariableData` | Adds a ResourceData value to the variable data. |
| `addResourceReference(resourceReference: String)` | `VariableData` | Adds a resource reference ID to the variable data. Example: "space/123". |
| `addStringValue(value: String)` | `VariableData` | Adds a string value to the variable data. |
| `addTimestampValue(value: TimeStamp)` | `VariableData` | Adds a TimeStamp value to the variable data. |
| `addWorkflowTextFormat(workflowTextFormat: WorkflowTextFormat)` | `VariableData` | Adds a WorkflowTextFormat value to the variable data. |

All methods return the `VariableData` object for method chaining.

## Code Sample

```javascript
const variableData = AddOnsResponseService.newVariableData()
    .addBooleanValue(true)
    .addIntegerValue(123);
```
