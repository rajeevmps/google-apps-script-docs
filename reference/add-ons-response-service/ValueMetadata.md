# ValueMetadata

Contains information about the potential values of a variable.

A valueMetadata contains information about the potential values of a variable. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addCastableType(dataType)

`addCastableType(dataType: BasicDataType): ValueMetadata`

Adds a optional allowed types that can be dynamically casted for a variable data to this value metadata.

### addEnumValue(enumValue)

`addEnumValue(enumValue: String): ValueMetadata`

Adds an optional string value to the allowed enum values of a variable, this field can only be set if the DataType is set to String type.

### setDefaultValue(defaultValue)

`setDefaultValue(defaultValue: String): ValueMetadata`

Sets the optional default value of the variable, example, if the variable type is boolean, defaultValue may be set to "true" or "false".

## Code Sample

```javascript
let allowedValue1 = "001";
let allowedValue2 = "002";

const valueMetadata = AddOnsResponseService.newValueMetadata()
   .addEnumValue(allowedValue1)
   .addEnumValue(allowedValue2)
   .setDefaultValue(allowedValue1)
   .addCastableType(AddOnsResponseService.BasicDataType.STRING)
   .addCastableType(AddOnsResponseService.BasicDataType.INTEGER);
```
