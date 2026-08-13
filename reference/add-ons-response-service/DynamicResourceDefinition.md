# DynamicResourceDefinition

A building block for a `ResourceFieldsDefinitionRetrievedAction`.

A DynamicResourceDefinition is a building block for a `ResourceFieldsDefinitionRetrievedAction`, it can contain one or more numbers of `ResourceField` to dynamically define the number of output variables provided by a step in Google Workspace Studio.

Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addResourceField(resourceField)

`addResourceField(resourceField: ResourceField): DynamicResourceDefinition`

Adds a resource field to the dynamic resource definition.

### setResourceId(resourceId)

`setResourceId(resourceId: String): DynamicResourceDefinition`

Sets the ID for the dynamic resource definition, this ID corresponds to the `workflowResourceDefinitionId` in the manifest.

## Code Sample

```javascript
let dynamicResourceDefinition = AddOnsResponseService.newDynamicResourceDefinition()
   .setResourceId("resource_definition_1")
   .addResourceField(
     AddOnsResponseService.newResourceField()
       .setSelector("question_1")
       .setDisplayText("Question 1")
   );
```
