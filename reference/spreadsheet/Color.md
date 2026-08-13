# Color

Represents a color.

The Color object represents a color and can be converted to an `RgbColor` or a `ThemeColor`. You can retrieve the color type using the `getColorType()` method. Converting to `RgbColor` or `ThemeColor` may throw an error if the color is not of that type. Using these methods requires specific spreadsheet authorization scopes.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `asRgbColor()` | `RgbColor` | Converts this color to an RgbColor. Throws `Error` if the color is not an `RgbColor`. |
| `asThemeColor()` | `ThemeColor` | Converts this color to a ThemeColor. Throws `Error` if the color is not a `ThemeColor`. |
| `getColorType()` | `ColorType` | Get the type of this color. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
