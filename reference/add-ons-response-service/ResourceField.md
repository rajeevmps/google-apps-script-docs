# ResourceField

A basic building block of a `DynamicResourceDefinition`.

A ResourceField is a basic building block of a `DynamicResourceDefinition`, each resource field corresponds to a output variable of the current step. A single `DynamicResourceDefinition` can contain multiple resource fields.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setDataType(dataType)

`setDataType(dataType: DataType): ResourceField`

Sets the data type of the field, allows other steps to filter the variables by type at selection.

### setDisplayText(displayText)

`setDisplayText(displayText: String): ResourceField`

Sets the description of the field that is displayed to the end user during variable selection in subsequent steps.

### setSelector(selector)

`setSelector(selector: String): ResourceField`

Sets a key for the provider function to provide the value to during the step's execution.

## Code Sample

```javascript
function onDynamicDefinitionFunction(e) {
  let resourceField = AddOnsResponseService.newResourceField()
    .setSelector("question_1")
    .setDisplayText("Question 1")
    .setDataType(AddOnsResponseService.newDataType()
       .setBasicDataType(AddOnsResponseService.BasicDataType.STRING)
    );

  let resourceDefinitions = AddOnsResponseService.newDynamicResourceDefinition()
    .setResourceId("resource_definition_1")
    .addResourceField(resourceField);
}

function onDynamicProviderFunction(e) {
  let workflowAction = AddOnsResponseService.newResourceRetrievedAction()
    .setResourceData(
      AddOnsResponseService.newResourceData()
        .addVariableData("question_1", AddOnsResponseService.newVariableData().addStringValue("Answer 1"))
    );
}
```
