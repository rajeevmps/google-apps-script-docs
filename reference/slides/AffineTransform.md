# AffineTransform

A 3x3 matrix used to transform source coordinates (x1,y1) into destination coordinates (x2,y2).

A 3x3 matrix used to transform source coordinates (x1, y1) into destination coordinates (x2, y2) according to matrix multiplication, using the formula:

- x2 = scaleX * x1 + shearX * y1 + translateX
- y2 = scaleY * y1 + shearY * x1 + translateY

## Methods

### getScaleX()

`Number`

Gets the X coordinate scaling element.

**Returns**

`Number` — the X coordinate scaling element

### getScaleY()

`Number`

Gets the Y coordinate scaling element.

**Returns**

`Number` — the Y coordinate scaling element

### getShearX()

`Number`

Gets the X coordinate shearing element.

**Returns**

`Number` — the X coordinate shearing element

### getShearY()

`Number`

Gets the Y coordinate shearing element.

**Returns**

`Number` — the Y coordinate shearing element

### getTranslateX()

`Number`

Gets the X coordinate translation element in points.

**Returns**

`Number` — the X coordinate translation element in points

### getTranslateY()

`Number`

Gets the Y coordinate translation element in points.

**Returns**

`Number` — the Y coordinate translation element in points

### toBuilder()

`AffineTransformBuilder`

Returns a new AffineTransformBuilder based on this transform.

**Returns**

`AffineTransformBuilder` — a new builder based on this transform's elements
