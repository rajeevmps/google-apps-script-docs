# Checkbox

Contains checkbox information for the config.

Contains checkbox information for the config. Its properties determine how the checkbox is displayed in Data Studio.

## Code Sample

```javascript
const config = DataStudioApp.createCommunityConnector().getConfig();
const checkbox = config.newCheckbox()
                     .setId('use_https')
                     .setName('Use Https?')
                     .setHelpText('Whether or not https should be used.')
                     .setAllowOverride(true);
```

## Methods

### setAllowOverride(allowOverride)

**Signature:** `setAllowOverride(allowOverride: Boolean): Checkbox`

**Description:** Enables overriding for this config entry. If set to `true`, data source creators have the option to enable this for report editors. Returns this builder, for chaining.

### setHelpText(helpText)

**Signature:** `setHelpText(helpText: String): Checkbox`

**Description:** Sets the help text for this configuration entry. Returns this builder, for chaining.

### setId(id)

**Signature:** `setId(id: String): Checkbox`

**Description:** Sets the unique ID for this configuration entry. Returns this builder, for chaining.

### setIsDynamic(isDynamic)

**Signature:** `setIsDynamic(isDynamic: Boolean): Checkbox`

**Description:** Sets the dynamic status for this configuration entry. If a dynamic configuration entry is modified, subsequent configuration entries are cleared. Returns this builder, for chaining.

### setName(name)

**Signature:** `setName(name: String): Checkbox`

**Description:** Sets the display name for this configuration entry. Returns this builder, for chaining.
