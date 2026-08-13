# Fill

Describes the page element's background.

Describes the page element's background. The Fill class provides methods to manage background properties of page elements in Google Slides, including retrieving solid fill and fill type information, setting fills using Color objects, RGB values, hex strings, or theme colors, managing transparency through alpha values, and setting transparent backgrounds.

## Methods

### getSolidFill()

`SolidFill`

Get the solid fill of this background, or `null` if the fill type is not `FillType.SOLID`.

**Returns**

`SolidFill` — the solid fill of this background, or `null`

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getType()

`FillType`

Get the type of this fill.

**Returns**

`FillType` — the type of this fill

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### isVisible()

`Boolean`

Whether the background is visible.

**Returns**

`Boolean` — `true` if background is visible; `false` otherwise

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(color)

`void`

Sets the solid fill to the given `Color`.

**Parameters**

- `color` (`Color`) — the color to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(color, alpha)

`void`

Sets the solid fill to the given alpha and `Color`.

**Parameters**

- `color` (`Color`) — the color to set
- `alpha` (`Number`) — the alpha to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(red, green, blue)

`void`

Sets the solid fill to the given RGB values.

**Parameters**

- `red` (`Integer`) — the red value
- `green` (`Integer`) — the green value
- `blue` (`Integer`) — the blue value

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(red, green, blue, alpha)

`void`

Sets the solid fill to the given alpha and RGB values.

**Parameters**

- `red` (`Integer`) — the red value
- `green` (`Integer`) — the green value
- `blue` (`Integer`) — the blue value
- `alpha` (`Number`) — the alpha to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(hexString)

`void`

Sets the solid fill to the given hex color string.

**Parameters**

- `hexString` (`String`) — the hex color string to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(hexString, alpha)

`void`

Sets the solid fill to the given alpha and hex color string.

**Parameters**

- `hexString` (`String`) — the hex color string to set
- `alpha` (`Number`) — the alpha to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(color)

`void`

Sets the solid fill to the given `ThemeColorType`.

**Parameters**

- `color` (`ThemeColorType`) — the theme color type to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setSolidFill(color, alpha)

`void`

Sets the solid fill to the given alpha and `ThemeColorType`.

**Parameters**

- `color` (`ThemeColorType`) — the theme color type to set
- `alpha` (`Number`) — the alpha to set

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setTransparent()

`void`

Sets the background to transparent.

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
