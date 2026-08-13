# CustomField

A custom field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

The CustomField class represents custom data entries for contacts. Requires authorization scope `https://www.google.com/m8/feeds`.

## Methods

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Gets the label for this field. This may be a Field, ExtendedField, or a String. Code example provided on the page demonstrates logging labels for address fields of contact "John Doe".

### setLabel(label)

**Signature:** `setLabel(label: String): CustomField`

**Description:** Sets the label of this field. Code example provided on the page shows setting label to "Apartment" for the first address field.

### deleteCustomField() (Deprecated)

**Signature:** `deleteCustomField(): void`

**Description:** Deletes this field. Code example provided iterates through custom fields and deletes one with label "foo".

### getValue() (Deprecated)

**Signature:** `getValue(): Object`

**Description:** Gets the value of the field. Code example provided logs values of all custom fields for "John Doe".

### setLabel(field) (Deprecated)

**Signature:** `setLabel(field: ExtendedField): CustomField`

**Description:** Sets the label of this field, using an ExtendedField standard label.

### setValue(value) (Deprecated)

**Signature:** `setValue(value: Object): CustomField`

**Description:** Sets the value of this field.
