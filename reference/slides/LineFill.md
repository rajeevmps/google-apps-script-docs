# LineFill

The fill of a line or outline.

LineFill describes the fill of a line or outline. You can get the type of line fill using `getFillType()`. You can retrieve the solid fill of a line using `getSolidFill()`, which returns `null` if the fill type is not `LineFillType.SOLID`. The solid fill can be set using various methods that accept different color representations and an optional alpha value.

## Methods

### getFillType()

`LineFillType`

Gets the type of the line fill.

**Returns**

`LineFillType` — the type of the line fill

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getSolidFill()

`SolidFill`

Gets the solid fill of the line, or `null` if the fill type is not `LineFillType.SOLID`.

**Returns**

`SolidFill` — the solid fill of the line, or `null`

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
