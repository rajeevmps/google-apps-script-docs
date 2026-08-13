# Color

A Color object which represents a color in the RGBA color space.

A Color object which represents a color in the RGBA color space. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setRed(red)

`setRed(red: Number): Color`

Sets the red component of the color.

**Parameters**
- `red` (Number) — The red component of the color.

**Returns**
- `Color` — This object, for chaining.

### setGreen(green)

`setGreen(green: Number): Color`

Sets the green component of the color.

**Parameters**
- `green` (Number) — The green component of the color.

**Returns**
- `Color` — This object, for chaining.

### setBlue(blue)

`setBlue(blue: Number): Color`

Sets the blue component of the color.

**Parameters**
- `blue` (Number) — The blue component of the color.

**Returns**
- `Color` — This object, for chaining.

### setAlpha(alpha)

`setAlpha(alpha: Number): Color`

Sets the alpha component of the color.

**Parameters**
- `alpha` (Number) — The alpha component of the color.

**Returns**
- `Color` — This object, for chaining.

## Code Sample

```javascript
const errorStyledText = AddOnsResponseService.newStyledText()
  .setText("Styled Text!")
  .addStyle(AddOnsResponseService.TextStyle.UNDERLINE)
  .setColor(
    AddOnsResponseService.newColor()
      .setRed(0.1)
      .setBlue(1.0)
      .setGreen(1.0)
      .setAlpha(0.78)
  )
```
