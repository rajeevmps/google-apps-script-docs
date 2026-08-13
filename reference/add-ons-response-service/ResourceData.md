# ResourceData

Represents a application specific resource data.

Represents a application specific resource data, a resource data contains a collection of key-value pairs of variable names and `VariableData`. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addVariableData(key, value)

`addVariableData(key: String, value: VariableData): ResourceData`

Adds a `VariableData` keyed by its variable name, a value is overwritten if the key already exists.

**Parameters**
- `key` (String) — The variable name to retrieve the corresponding variable data.
- `value` (VariableData) — The `VariableData` to be added.

### setVariableDataMap(fields)

`setVariableDataMap(fields: Object): ResourceData`

Sets the map of the variable data keyed by variable names.

**Parameters**
- `fields` (Object) — A collection of key-value pairs of string and variable data.

## Code Sample

```javascript
let customResourceData = AddOnsResponseService.newResourceData()
  .setVariableDataMap(
    {
      "field_1": fieldData_1,
      "field_2": fieldData_2
    }
  );

let outputVariableData = AddOnsResponseService.newVariableData()
  .addResourceData(customResourceData);

let workflowAction = AddOnsResponseService.newReturnOutputVariablesAction()
  .setVariableDataMap({ "resource_data": outputVariableData });
```
