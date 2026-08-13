# ChartOptions

Exposes options currently configured for a Chart, such as height, color, etc.

Exposes options currently configured for a Chart, such as height, color, etc. The options are immutable, and the `get(option)` method returns a configured option or `null` if not set, while `getOrDefault(option)` returns either the configured option or its default value if available.

## Methods

### get(option)

Returns: `Object`

Returns a configured option for this chart. Returns either the value currently set for the specified option or `null` if the option was not set.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The option to retrieve. |

### getOrDefault(option)

Returns: `Object`

Returns a configured option for this chart. If the chart option is not set, returns the default value of this option if available, or returns `null` if the default value is not available.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The option to retrieve. |

## Properties

None.
