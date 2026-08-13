# IMField

An instant messaging field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

An instant messaging field in a Contact. Requires authorization scope `https://www.google.com/m8/feeds`.

## Methods

### getAddress()

**Signature:** `getAddress(): String`

**Description:** Get the address for this field.

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Gets the label for this field. This may be a Field, ExtendedField, or a String.

### isPrimary()

**Signature:** `isPrimary(): Boolean`

**Description:** Gets whether this is the primary field value.

### setAddress(address)

**Signature:** `setAddress(address: String): IMField`

**Description:** Sets the address of this field.

### setAsPrimary()

**Signature:** `setAsPrimary(): IMField`

**Description:** Sets this field to primary.

### setLabel(field)

**Signature:** `setLabel(field: Field): IMField`

**Description:** Sets the label of this field.

### setLabel(label)

**Signature:** `setLabel(label: String): IMField`

**Description:** Sets the label of this field.

### deleteIMField() (Deprecated)

**Signature:** `deleteIMField(): void`

**Description:** Deletes this instant messaging field.
