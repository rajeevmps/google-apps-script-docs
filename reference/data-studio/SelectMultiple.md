# SelectMultiple

Contains select multiple information for the config.

Contains select multiple information for the config. Its properties determine how the select multiple is displayed in Data Studio.

## Methods

### addOption(optionBuilder)

**Signature:** `addOption(optionBuilder: OptionBuilder): SelectMultiple`

**Description:** Adds a new select option. Returns this builder, for chaining.

### setAllowOverride(allowOverride)

**Signature:** `setAllowOverride(allowOverride: Boolean): SelectMultiple`

**Description:** Enables overriding for this config entry. If set to `true`, data source creators have the option to enable this for report editors. Returns this builder, for chaining.

### setHelpText(helpText)

**Signature:** `setHelpText(helpText: String): SelectMultiple`

**Description:** Sets the help text for this configuration entry. Returns this builder, for chaining.

### setId(id)

**Signature:** `setId(id: String): SelectMultiple`

**Description:** Sets the unique ID for this configuration entry. Returns this builder, for chaining.

### setIsDynamic(isDynamic)

**Signature:** `setIsDynamic(isDynamic: Boolean): SelectMultiple`

**Description:** Sets the dynamic status for this configuration entry. If a dynamic configuration entry is modified, subsequent configuration entries are cleared. Returns this builder, for chaining.

### setName(name)

**Signature:** `setName(name: String): SelectMultiple`

**Description:** Sets the display name for this configuration entry. Returns this builder, for chaining.
