# AffineTransformBuilder

A builder for AffineTransform objects.

AffineTransformBuilder is used to build AffineTransform objects and defaults to the identity transform. Call the `build()` method to get the AffineTransform object. Methods are available to set scaling, shearing, and translation elements for both X and Y coordinates.

```javascript
const transform =
    SlidesApp.newAffineTransformBuilder().setScaleX(2.0).setShearY(1.1).build();

// The resulting transform matrix is
//  [ 2.0   0.0   0.0 ]
//  [ 1.1   1.0   0.0 ]
//  [  0     0     1  ]
```

## Methods

### build()

`AffineTransform`

Creates an `AffineTransform` object initialized with the elements set in the builder.

**Returns**

`AffineTransform` — the constructed transform

### setScaleX(scaleX)

`AffineTransformBuilder`

Sets the X coordinate scaling element and returns the builder.

**Parameters**

- `scaleX` (`Number`) — The X scaling.

**Returns**

`AffineTransformBuilder` — this builder, for chaining

### setScaleY(scaleY)

`AffineTransformBuilder`

Sets the Y coordinate scaling element and returns the builder.

**Parameters**

- `scaleY` (`Number`) — The Y scaling.

**Returns**

`AffineTransformBuilder` — this builder, for chaining

### setShearX(shearX)

`AffineTransformBuilder`

Sets the X coordinate shearing element and returns the builder.

**Parameters**

- `shearX` (`Number`) — The X shearing.

**Returns**

`AffineTransformBuilder` — this builder, for chaining

### setShearY(shearY)

`AffineTransformBuilder`

Sets the Y coordinate shearing element and returns the builder.

**Parameters**

- `shearY` (`Number`) — The Y shearing.

**Returns**

`AffineTransformBuilder` — this builder, for chaining

### setTranslateX(translateX)

`AffineTransformBuilder`

Sets the X coordinate translation element in points, and returns the builder.

**Parameters**

- `translateX` (`Number`) — The X translation in points.

**Returns**

`AffineTransformBuilder` — this builder, for chaining

### setTranslateY(translateY)

`AffineTransformBuilder`

Sets the Y coordinate translation element in points, and returns the builder.

**Parameters**

- `translateY` (`Number`) — The Y translation in points.

**Returns**

`AffineTransformBuilder` — this builder, for chaining
