# ResourceFieldsDefinitionRetrievedAction

Used to retrieve the definition of a list of resource fields.

A `ResourceFieldsDefinitionRetrievedAction` is a type of `ResourceFieldsDefinitionRetrievedAction` that is used to retrieve the definition of a list of resource fields through the `dynamicResourceDefinitionProvider` function specified in the manifest. A `ResourceFieldsDefinitionRetrievedAction` can contain one or more `DynamicResourceDefinition`.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addDynamicResourceDefinition(dynamicResourceDefinition)

`addDynamicResourceDefinition(dynamicResourceDefinition: DynamicResourceDefinition): ResourceFieldsDefinitionRetrievedAction`

Adds a `DynamicResourceDefinition` to the resource fields definition retrieved action.

**Parameters**
- `dynamicResourceDefinition` (DynamicResourceDefinition) — The dynamic resource definition to add to the action.

## Code Sample

```javascript
let resourceDefinitions = AddOnsResponseService.newDynamicResourceDefinition()
   .setResourceId("resource_definition_1")
   .addResourceField(AddOnsResponseService.newResourceField()
     .setSelector("question_1")
     .setDisplayText("Question 1"))

let workflowAction = AddOnsResponseService.newResourceFieldsDefinitionRetrievedAction()
   .addDynamicResourceDefinition(resourceDefinitions)

let hostAppAction = AddOnsResponseService.newHostAppAction()
   .setWorkflowAction(workflowAction);

return AddOnsResponseService.newRenderActionBuilder()
   .setHostAppAction(hostAppAction)
   .build();
```
