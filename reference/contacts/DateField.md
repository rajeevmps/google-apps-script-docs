# DateField

A date field in a Contact. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

A date field in a Contact. This class is only used by the Contacts service, and dates used elsewhere in Apps Script use JavaScript's standard Date object.

## Methods

### getLabel()

**Signature:** `getLabel(): Object`

**Description:** Gets the label for this field.

### setLabel(label)

**Signature:** `setLabel(label: String): DateField`

**Description:** Sets the label of this field, such as "Birthday" or "Anniversary".

### deleteDateField() (Deprecated)

**Signature:** `deleteDateField(): void`

**Description:** Deletes this date.

### getDay() (Deprecated)

**Signature:** `getDay(): Integer`

**Description:** Gets the day of the month for this date.

### getMonth() (Deprecated)

**Signature:** `getMonth(): Month`

**Description:** Gets the month for this date.

### getYear() (Deprecated)

**Signature:** `getYear(): Integer`

**Description:** Gets the year for this date.

### setDate(month, day) (Deprecated)

**Signature:** `setDate(month: Month, day: Integer): void`

**Description:** Sets the date to this day, without a year.

### setDate(month, day, year) (Deprecated)

**Signature:** `setDate(month: Month, day: Integer, year: Integer): void`

**Description:** Sets the date to this day.
