# Config

Contains the configuration entries for a connector.

Contains the configuration entries for a connector. These configuration entries define what questions are asked when adding a new connector.

## Methods

### build()

**Signature:** `build(): Object`

**Description:** Validates this object and returns it in the format needed by Data Studio.

### newCheckbox()

**Signature:** `newCheckbox(): Checkbox`

**Description:** Returns a new checkbox configuration entry.

### newInfo()

**Signature:** `newInfo(): Info`

**Description:** Returns a new info configuration entry.

### newOptionBuilder()

**Signature:** `newOptionBuilder(): OptionBuilder`

**Description:** Returns a new options builder.

### newSelectMultiple()

**Signature:** `newSelectMultiple(): SelectMultiple`

**Description:** Returns a new select multiple configuration entry.

### newSelectSingle()

**Signature:** `newSelectSingle(): SelectSingle`

**Description:** Returns a new select single configuration entry.

### newTextArea()

**Signature:** `newTextArea(): TextArea`

**Description:** Returns a new text area configuration entry.

### newTextInput()

**Signature:** `newTextInput(): TextInput`

**Description:** Returns a new text input configuration entry.

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

### setDateRangeRequired(dateRangeRequired)

**Signature:** `setDateRangeRequired(dateRangeRequired: Boolean): Config`

**Description:** If `true`, a date range is provided for getData() requests.

### setIsSteppedConfig(isSteppedConfig)

**Signature:** `setIsSteppedConfig(isSteppedConfig: Boolean): Config`

**Description:** If `true`, `getConfig()` is called again with the current user configuration.
