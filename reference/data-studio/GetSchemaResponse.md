# GetSchemaResponse

Builder to create a getSchema() response for your script project.

Builder to create a `getSchema()` response for your script project. This class is used within Google Data Studio connectors to define the schema for data returned by custom connectors.

## Methods

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio.

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setFields(fields)

**Signature:** `setFields(fields: Fields): GetSchemaResponse`

**Description:** Sets the `Fields` of the builder. Returns this builder, for chaining.

## Code Sample

```javascript
function getSchema() {
  const cc = DataStudioApp.createCommunityConnector();
  const fields = cc.getFields();

  fields.newDimension()
      .setId('Created')
      .setName('Date Created')
      .setDescription('The date that this was created')
      .setType(cc.FieldType.YEAR_MONTH_DAY);

  fields.newMetric()
      .setId('Amount')
      .setName('Amount (USD)')
      .setDescription('The cost in US dollars')
      .setType(cc.FieldType.CURRENCY_USD);

  return cc.newGetSchemaResponse().setFields(fields).build();
}
```
