# SpreadsheetTheme

Access and modify existing themes.

Access and modify existing themes. To set a theme on a spreadsheet, use Spreadsheet.setSpreadsheetTheme(theme) .

## Methods

### `getConcreteColor(themeColorType)`

Returns the concrete Color for a valid theme color type. Throws exception if the theme
color type is not set in the current theme.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| theme Color Type | Theme Color Type | Theme color type. |

**Returns:** Color — Concrete color.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getFontFamily()`

Returns the font family of the theme, or null if it's a null theme.

**Returns:** String|null — The theme font family.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `getThemeColors()`

Returns a list of all possible theme color types for the current theme.

**Returns:** ThemeColorType[] — A list of theme colors.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setConcreteColor(themeColorType, color)`

Sets the concrete color associated with the ThemeColorType in this color scheme to the
given color.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| theme Color Type | Theme Color Type | The theme color type. |
| color | Color | The color. |

**Returns:** SpreadsheetTheme — The theme, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setConcreteColor(themeColorType, red, green, blue)`

Sets the concrete color associated with the ThemeColorType in this color scheme to the
given color in RGB format.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| theme Color Type | Theme Color Type | The theme color type. |
| red | Integer | The value of red channel. |
| green | Integer | The value of green channel. |
| blue | Integer | The value of blue channel. |

**Returns:** SpreadsheetTheme — The theme, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

### `setFontFamily(fontFamily)`

Sets the font family for the theme.

**Parameters:**

| Name | Type | Description |
|---|---|---|
| font Family | String | The new theme font family. |

**Returns:** SpreadsheetTheme — This theme, for chaining.

**Authorization:** Requires one or more of the following scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`

