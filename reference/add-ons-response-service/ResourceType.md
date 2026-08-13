# ResourceType

An application specific resource type.

An application specific resource type, the unique identifier of the resource type should have a corresponding WorkflowResourceDefinition. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setWorkflowResourceDefinitionId(resourceType)

`setWorkflowResourceDefinitionId(resourceType: String): ResourceType`

Sets the workflow resource definition id.

**Parameters**
- `resourceType` (String) — The workflow resource definition id.

**Returns**
- `ResourceType` — This ResourceType object.

## Code Sample

```javascript
const customResourceType = AddOnsResponseService.newResourceType()
   .setWorkflowResourceDefinitionId("sample_resource_type_1");
```
