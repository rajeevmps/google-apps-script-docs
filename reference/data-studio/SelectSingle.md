# SelectSingle

Contains configuration information for how a select single is displayed in Data Studio.

SelectSingle contains configuration information for how a select single is displayed in Data Studio. You can add select options, enable overriding, set help text, ID, dynamic status, and display name for a SelectSingle config entry.

## Methods

### addOption(optionBuilder)

**Signature:** `addOption(optionBuilder: OptionBuilder): SelectSingle`

**Description:** Adds a new select option. Returns this builder, for chaining.

### setAllowOverride(allowOverride)

**Signature:** `setAllowOverride(allowOverride: Boolean): SelectSingle`

**Description:** Enables overriding for this config entry. If set to `true`, data source creators have the option to enable this for report editors. Returns this builder, for chaining.

### setHelpText(helpText)

**Signature:** `setHelpText(helpText: String): SelectSingle`

**Description:** Sets the help text for this configuration entry. Returns this builder, for chaining.

### setId(id)

**Signature:** `setId(id: String): SelectSingle`

**Description:** Sets the unique ID for this configuration entry. Returns this builder, for chaining.

### setIsDynamic(isDynamic)

**Signature:** `setIsDynamic(isDynamic: Boolean): SelectSingle`

**Description:** Sets the dynamic status for this configuration entry. If a dynamic configuration entry is modified, subsequent configuration entries are cleared. Returns this builder, for chaining.

### setName(name)

**Signature:** `setName(name: String): SelectSingle`

**Description:** Sets the display name for this configuration entry. Returns this builder, for chaining.
