# Info

Contains info entry data for the config.

The `Info` object contains data for the configuration and determines how it is displayed in Data Studio. You can create a new `Info` object using `config.newInfo()`.

## Code Sample

```javascript
const cc = DataStudioApp.createCommunityConnector();
const config = cc.getConfig();

const info1 = config.newInfo().setId('info1').setText(
    'This text gives some context on the configuration.');
```

## Methods

### setId(id)

**Signature:** `setId(id: String): Info`

**Description:** Sets the unique ID for this configuration entry. Returns the builder for method chaining.

### setText(text)

**Signature:** `setText(text: String): Info`

**Description:** Sets the text for this configuration entry. Returns the builder for method chaining.
