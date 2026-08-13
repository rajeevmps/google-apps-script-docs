# Autofit

The autofit settings of a shape.

Describes the autofit settings of a shape. If a change is made that might affect text fitting within its bounding text box:

- Autofit is deactivated and set to `AutofitType.NONE`.
- The font scale is reset to the default value and applied to the font size.
- The line spacing reduction is reset to the default value and applied to the line spacing.

## Methods

### disableAutofit()

`Autofit`

Sets the `AutofitType` of a shape to `AutofitType.NONE`.

**Returns**

`Autofit` — this autofit, for chaining

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getAutofitType()

`AutofitType`

Gets the `AutofitType` of the shape.

**Returns**

`AutofitType` — the autofit type

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getFontScale()

`Number`

Gets the font scale applied to the shape. For shapes with `AutofitType` `NONE` or `SHAPE_AUTOFIT`, this value is the default value of 1. For `TEXT_AUTOFIT`, the value returned is what the original font size is multiplied by to fit within the shape.

**Returns**

`Number` — the font scale

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getLineSpacingReduction()

`Number`

Gets the line spacing reduction applied to the shape. For shapes with `AutofitType` `NONE` or `SHAPE_AUTOFIT`, this value is the default value of 0. For `TEXT_AUTOFIT`, the returned value is the amount of spacing subtracted from the original spacing to make the text fit within the shape.

**Returns**

`Number` — the line spacing reduction

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
