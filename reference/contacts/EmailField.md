# EmailField

An email field within a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

EmailField represents an email field within a Contact. EmailField provides methods to get and set the email address and its label, and to check or set if it is the primary email field. Requires authorization scope `https://www.google.com/m8/feeds`.

## Methods

### getAddress()

**Signature:** `getAddress(): String`

**Description:** Returns the email address as a string.

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Retrieves the label (Field, ExtendedField, or String).

### isPrimary()

**Signature:** `isPrimary(): Boolean`

**Description:** Checks if this is the primary field value.

### setAddress(address)

**Signature:** `setAddress(address: String): EmailField`

**Description:** Updates the email address.

### setAsPrimary()

**Signature:** `setAsPrimary(): EmailField`

**Description:** Designates this field as primary.

### setLabel(field)

**Signature:** `setLabel(field: Field): EmailField`

**Description:** Sets label using a Field parameter.

### setLabel(label)

**Signature:** `setLabel(label: String): EmailField`

**Description:** Sets label using a String parameter.

### deleteEmailField() (Deprecated)

**Signature:** `deleteEmailField(): void`

**Description:** Removes the email from the Contact.

### getDisplayName() (Deprecated)

**Signature:** `getDisplayName(): String`

**Description:** Returns the display name for the email.

### setDisplayName(name) (Deprecated)

**Signature:** `setDisplayName(name: String): EmailField`

**Description:** Sets the display name.
