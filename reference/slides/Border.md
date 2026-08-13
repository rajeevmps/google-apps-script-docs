# Border

The border around an element.

The Border class describes the border around an element. Methods enable getting and setting dash style, line fill, and weight of the border, plus checking visibility and setting transparency.

## Methods

### getDashStyle()

`DashStyle`

Gets the `DashStyle` of the border.

**Returns**

`DashStyle` — the dash style of the border, or `null` if the element does not have a border

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getLineFill()

`LineFill`

Gets the `LineFill` of the border.

**Returns**

`LineFill` — the line fill of the border

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getWeight()

`Number`

Gets the thickness of the border in points. Returns `null` if the element does not have a border.

**Returns**

`Number` — the thickness of the border in points, or `null` if the element does not have a border

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### isVisible()

`Boolean`

Gets whether the border is visible or not.

**Returns**

`Boolean` — whether the border is visible or not

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setDashStyle(style)

`Border`

Sets the `DashStyle` of the border. Setting a `DashStyle` on a transparent border makes it visible.

**Parameters**

- `style` (`DashStyle`) — the dash style to set

**Returns**

`Border` — this border, for chaining

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setTransparent()

`Border`

Sets the border to be transparent.

**Returns**

`Border` — this border, for chaining

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### setWeight(points)

`Border`

Sets the thickness of the border in points. Setting a weight on a transparent border makes it visible.

**Parameters**

- `points` (`Number`) — the thickness, in points, to set

**Returns**

`Border` — this border, for chaining

Requires authorization scope: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`
