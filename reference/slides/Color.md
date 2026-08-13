# Color

An opaque color.

The Color class represents an opaque color. It provides methods to convert between different color representations and determine the color type.

## Methods

### asRgbColor()

`RgbColor`

Converts this color to an `RgbColor`.

**Returns**

`RgbColor` — the converted color

Throws: Error if the color is not an RgbColor

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### asThemeColor()

`ThemeColor`

Converts this color to a `ThemeColor`.

**Returns**

`ThemeColor` — the converted color

Throws: Error if the color is not a ThemeColor

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getColorType()

`ColorType`

Get the type of this color.

**Returns**

`ColorType` — the color type

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
