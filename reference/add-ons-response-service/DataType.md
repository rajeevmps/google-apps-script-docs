# DataType

A DataType is used to set the type of a variable.

A DataType is used to set the type of a variable. The type can be one of the basic data type or a Workspace Studio-specific resource type. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setBasicDataType(basicDataType)

`setBasicDataType(basicDataType: BasicDataType): DataType`

Sets the data type to one of the supported BasicDataTypes.

### setResourceType(resourceType)

`setResourceType(resourceType: ResourceType): DataType`

Sets the data type to a custom defined ResourceType.

### setValueMetadata(valueMetadata)

`setValueMetadata(valueMetadata: ValueMetadata): DataType`

Sets the ValueMetadata, which contains type-related information related to the variable.

## Code Sample

```javascript
const dataType = AddOnsResponseService.newDataType()
    .setBasicDataType(
      AddOnsResponseService.BasicDataType.STRING
    )
    .setValueMetadata(
      AddOnsResponseService.newValueMetadata()
        .addEnumValue("sample_enum_value")
    );

let resourceField = AddOnsResponseService.newResourceField()
    .setSelector("question_1")
    .setDisplayText("Question 1")
    .setDataType(dataType);
```
