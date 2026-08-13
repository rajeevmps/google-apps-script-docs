# TextArea

Contains text area information for the config.

Contains text area information for the config. Its properties determine how the text input is displayed in Data Studio.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
const config = cc.getConfig();

const textArea1 = config.newTextArea()
                      .setId('textArea1')
                      .setName('Search')
                      .setHelpText('for example, Coldplay')
                      .setAllowOverride(true)
                      .setPlaceholder('Search for an artist for all songs.');
```

## Methods

### setAllowOverride(allowOverride)

**Signature:** `setAllowOverride(allowOverride: Boolean): TextArea`

**Description:** Enables overriding for this config entry. If set to `true`, data source creators have the option to enable this for report editors. Returns this builder, for chaining.

### setHelpText(helpText)

**Signature:** `setHelpText(helpText: String): TextArea`

**Description:** Sets the help text for this configuration entry. Returns this builder, for chaining.

### setId(id)

**Signature:** `setId(id: String): TextArea`

**Description:** Sets the unique ID for this configuration entry. Returns this builder, for chaining.

### setIsDynamic(isDynamic)

**Signature:** `setIsDynamic(isDynamic: Boolean): TextArea`

**Description:** Sets the dynamic status for this configuration entry. If a dynamic configuration entry is modified, subsequent configuration entries are cleared. Returns this builder, for chaining.

### setName(name)

**Signature:** `setName(name: String): TextArea`

**Description:** Sets the display name for this configuration entry. Returns this builder, for chaining.

### setPlaceholder(placeholder)

**Signature:** `setPlaceholder(placeholder: String): TextArea`

**Description:** Sets the placeholder text for this configuration entry. Returns this builder, for chaining.
