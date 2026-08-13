# PhoneField

A phone number field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A phone number field in a Contact. Requires authorization scope `https://www.google.com/m8/feeds`.

## Methods

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Retrieves the label for this field, which may be a Field, ExtendedField, or a custom String value.

### isPrimary()

**Signature:** `isPrimary(): Boolean`

**Description:** Determines whether this represents the primary field value for the contact.

### setAsPrimary()

**Signature:** `setAsPrimary(): PhoneField`

**Description:** Marks this field as the primary phone number field. Returns the PhoneField instance for method chaining.

### setLabel(field)

**Signature:** `setLabel(field: Field): PhoneField`

**Description:** Updates the label using a standard Field constant. Supports chaining.

### setLabel(label)

**Signature:** `setLabel(label: String): PhoneField`

**Description:** Updates the label with a custom string value. Supports chaining.

### deletePhoneField() (Deprecated)

**Signature:** `deletePhoneField(): void`

**Description:** Removes this phone number field. Do not use in new scripts.

### getPhoneNumber() (Deprecated)

**Signature:** `getPhoneNumber(): String`

**Description:** Retrieves the phone number value as a string. Do not use in new scripts.

### setPhoneNumber(number) (Deprecated)

**Signature:** `setPhoneNumber(number: String): PhoneField`

**Description:** Modifies the phone number value. Supports chaining. Do not use in new scripts.
