# UrlField

A URL field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A URL field in a Contact.

## Methods

### getAddress()

**Signature:** `getAddress(): String`

**Description:** Retrieves the address for this field as a string value.

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Obtains the label for this field, which may be a Field, ExtendedField, or custom String.

### isPrimary()

**Signature:** `isPrimary(): Boolean`

**Description:** Determines whether this represents the primary field value.

### setAddress(address)

**Signature:** `setAddress(address: String): UrlField`

**Description:** Assigns a new address to this field. Returns the field for method chaining.

### setAsPrimary()

**Signature:** `setAsPrimary(): UrlField`

**Description:** Designates this field as primary. Returns the field for chaining operations.

### setLabel(field)

**Signature:** `setLabel(field: Field): UrlField`

**Description:** Sets the label using a standard Field constant. Returns the field for chaining.

### setLabel(label)

**Signature:** `setLabel(label: String): UrlField`

**Description:** Assigns a custom label string to this field. Returns the field for chaining.

### deleteUrlField() (Deprecated)

**Signature:** `deleteUrlField(): void`

**Description:** Removes this URL field. This method is deprecated and should not be used in new scripts.
