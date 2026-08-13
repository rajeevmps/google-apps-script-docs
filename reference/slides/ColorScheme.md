# ColorScheme

The color scheme for a page.

A color scheme defines a mapping from members of `ThemeColorType` to the actual colors used to render them.

## Methods

### getConcreteColor(theme)

`Color`

Returns the concrete `Color` associated with the `ThemeColorType` in this color scheme. The returned color is guaranteed to not be an instance of `ThemeColor`.

**Parameters**

- `theme` (`ThemeColorType`) — The theme color to derive the concrete color from.

**Returns**

`Color` — The concrete color corresponding the theme color type in this scheme.

### getThemeColors()

`ThemeColorType[]`

Returns a list of all possible theme color types in a color scheme.

**Returns**

`ThemeColorType[]` — The possible theme color types in this scheme.

### setConcreteColor(type, color)

`ColorScheme`

Sets the concrete color associated with the `ThemeColorType` in this color scheme to the given color.

**Parameters**

- `type` (`ThemeColorType`) — The theme color type.
- `color` (`Color`) — The color to set the theme color type to.

**Returns**

`ColorScheme` — This color scheme, for chaining.

### setConcreteColor(type, red, green, blue)

`ColorScheme`

Sets the concrete color associated with the `ThemeColorType` in this color scheme to the given color in RGB format.

**Parameters**

- `type` (`ThemeColorType`) — The theme color type.
- `red` (`Integer`) — The red value of the color to set the theme color type to (between 0 and 255).
- `green` (`Integer`) — The green value of the color to set the theme color type to (between 0 and 255).
- `blue` (`Integer`) — The blue value of the color to set the theme color type to (between 0 and 255).

**Returns**

`ColorScheme` — This color scheme, for chaining.

### setConcreteColor(type, hexColor)

`ColorScheme`

Sets the concrete color associated with the `ThemeColorType` in this color scheme to the given color in HEX format. The hex string must be in the format '#RRGGBB'.

**Parameters**

- `type` (`ThemeColorType`) — The theme color type.
- `hexColor` (`String`) — The hex color to set the theme color type to, such as '#F304a7'.

**Returns**

`ColorScheme` — This color scheme, for chaining.
