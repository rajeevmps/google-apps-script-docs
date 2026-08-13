# Fields

Contains a set of Fields for a community connector.

Contains a set of `Field`s for a community connector. This set of fields define which dimensions and metrics can be used in Data Studio.

## Methods

### asArray()

**Signature:** `asArray(): Field[]`

**Description:** Returns a view of this object as an array.

**Code Sample:**
```javascript
const fields = DataStudioApp.createCommunityConnector().getFields();
fields.newDimension().setId('field1_id');
fields.newDimension().setId('field2_id');
fields.newDimension().setId('field3_id');

fields.asArray().map((field) => {
  Logger.log(field.getId());
});
```

### build()

**Signature:** `build(): Object[]`

**Description:** Validates this object and returns it in the format needed by Data Studio. Throws an error if a valid object cannot be constructed.

### forIds(ids)

**Signature:** `forIds(ids: String[]): Fields`

**Description:** Returns a new `Fields` object filtered to `Field`s with an ID in `ids`.

**Code Sample:**
```javascript
const fields = DataStudioApp.createCommunityConnector().getFields();
fields.newDimension().setId('field1_id');
fields.newDimension().setId('field2_id');
fields.newDimension().setId('field3_id');

const subsetFields = fields.forIds(['field1_id', 'field3_id']);
```

### getDefaultDimension()

**Signature:** `getDefaultDimension(): Field`

**Description:** Returns the default dimension to be used for the set of fields. The default dimension is selected automatically when a new visualization is made.

### getDefaultMetric()

**Signature:** `getDefaultMetric(): Field`

**Description:** Returns the default metric to be used for the set of fields. The default metric is selected automatically when a new visualization is made.

### getFieldById(fieldId)

**Signature:** `getFieldById(fieldId: String): Field`

**Description:** Returns a field with a given ID, or `null` if no field with that ID is in this `Fields` object.

**Code Sample:**
```javascript
const fields = DataStudioApp.createCommunityConnector().getFields();
const field1 = fields.newDimension().setId('field1_id');

const byId = fields.getFieldById('field1_id');
const byId2 = fields.getFieldById('not present id');
```

### newDimension()

**Signature:** `newDimension(): Field`

**Description:** Returns a new dimension `Field`.

### newMetric()

**Signature:** `newMetric(): Field`

**Description:** Returns a new metric `Field`.

### setDefaultDimension(fieldId)

**Signature:** `setDefaultDimension(fieldId: String): void`

**Description:** Sets the default dimension to be used for the set of fields. The default dimension is selected automatically when a new visualization is made.

### setDefaultMetric(fieldId)

**Signature:** `setDefaultMetric(fieldId: String): void`

**Description:** Sets the default metric to be used for the set of fields. The default metric is selected automatically when a new visualization is made.
