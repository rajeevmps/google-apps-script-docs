# ColorBuilder

Builder for Color.

ColorBuilder is a builder for creating color objects in Apps Script spreadsheets. A new ColorBuilder is created using `SpreadsheetApp.newColor()`. The builder allows setting a color as either an RGB color using a CSS string or as a theme color using a ThemeColorType. Once configured, the `build()` method creates the final Color object. You can also convert a built color object to its RgbColor or ThemeColor representation and get its ColorType.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `asRgbColor()` | `RgbColor` | Converts this color to an `RgbColor`. Throws `Error` if the color is not an `RgbColor`. |
| `asThemeColor()` | `ThemeColor` | Converts this color to a `ThemeColor`. Throws `Error` if the color is not a `ThemeColor`. |
| `build()` | `Color` | Creates a color object from the settings supplied to the builder. |
| `getColorType()` | `ColorType` | Get the type of this color. |
| `setRgbColor(cssString: String)` | `ColorBuilder` | Sets as RGB color. `cssString` is the RGB color in CSS notation (such as '#ffffff'). Returns this builder, for chaining. |
| `setThemeColor(themeColorType: ThemeColorType)` | `ColorBuilder` | Sets as theme color. `themeColorType` is the theme color type. Returns this builder, for chaining. |

## Authorization

Several methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
