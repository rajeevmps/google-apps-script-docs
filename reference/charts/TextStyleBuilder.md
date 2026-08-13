# TextStyleBuilder

A builder used to create TextStyle objects.

A builder used to create TextStyle objects. It allows configuration of the text's properties such as name, color, and size.

## Methods

### build()

Returns: `TextStyle`

Builds and returns a text style configuration object that was built using this builder.

### setColor(cssValue)

Returns: `TextStyleBuilder`

Sets the color of the text style. The parameter accepts the CSS value for the color (such as `"blue"` or `"#00f"`).

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValue | String | the CSS value for the color |

### setFontName(fontName)

Returns: `TextStyleBuilder`

Sets the font name of the text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| fontName | String | the font name |

### setFontSize(fontSize)

Returns: `TextStyleBuilder`

Sets the font size of the text style. The parameter specifies the font size in pixels to use for the text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| fontSize | Number | the font size in pixels |

## Properties

None.

All setter methods return `TextStyleBuilder`, enabling method chaining for configuration workflows.
