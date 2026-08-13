# Size and position page elements

## Page Summary

- Page elements can be sized and positioned using getter/setter functions or by manipulating their affine transform.
- Size and position are measured from the upper left corner of the page to the upper left corner of the element's unrotated bounding box, and lengths are in points.
- You can set the size, position, and rotation of a page element when it's created or update them afterwards using specific setter functions.
- Scaling and reflection along an edge can be achieved using `scaleWidth()` and `scaleHeight()`, including with negative arguments for flipping.
- Lines have their rotation measured by their bounding box rotation, not their visual vertical angle.

There are two different ways you can get and change the size and position of
a page element:

1. Using its getter and setter functions for size and position.
2. Manipulating its affine transform, using its `getTransform()` and
`setTransform()` functions while preserving the inherent size.

## Read page element properties

![Sizing and Rotating](https://developers.google.com/static/apps-script/guides/slides/images/slides-script-rotation.png)

As shown in the figure, size and position are measured with respect to the
bounding box of a rendered page element when it has no rotation:

- **Left** and **Top**: measured from the upper left corner of the page to the
upper left corner of the unrotated bounding box. Use `getLeft()` and
`getTop()` to
read the values.
- **Width** and **Height**: the width and height of the unrotated bounding box.
Use `getWidth()` and `getHeight()` to read the values.
- **Rotation**: the clockwise rotation with respect to the vertical line around
the center of the bounding box. Use `getRotation()` to read the value.

All lengths are measured in points (pt). The rotation is measured in degrees
(°).

## Set page element properties

Set the size and position of a page element when you create it using
an insert method such as `insertShape()`. For an existing shape, you can set
the size, position, and rotation; you can also set an element's scaling to
resize or to reflect it along one of its edges.

### At creation

Provide position and size information when creating a page element.

```javascript
var slide = SlidesApp.getActivePresentation().getSlides()[0];
var shape = slide.insertShape(SlidesApp.ShapeType.TEXT_BOX, 100, 200, 300, 60);
Logger.log('Left: ' + shape.getLeft() + 'pt; Top: '
                    + shape.getTop() + 'pt; Width: '
                    + shape.getWidth() + 'pt; Height: '
                    + shape.getHeight() + 'pt; Rotation: '
                    + shape.getRotation() + ' degrees.');
```

The preceding script creates a shape on the first slide of the active presentation
with the specified position and size and reads the position and size information
of the shape. The expected log is:

```
Left: 100pt; Top: 200pt; Width: 300pt; Height: 60pt; Rotation: 0 degrees.
```

### Size, position, and rotation

Update the size and position of a page element after creation:

- Use `setLeft()` and `setTop()` to set the position of the upper left corner of the
unrotated bounding box.
- Use `setWidth()` and `setHeight()` to set the rendered width and height of the bounding
box.
- Use `setRotation()` to set the clockwise rotation of the bounding box around its
center.

The following script creates a shape on the first slide of the active
presentation,
uses setters to update its position, size, and rotation, and reads the position
and size information of the shape.

```javascript
var slide = SlidesApp.getActivePresentation().getSlides()[0];
var shape = slide.insertShape(SlidesApp.ShapeType.RECTANGLE);
shape.setLeft(100).setTop(200).setWidth(50).setHeight(60).setRotation(90);
Logger.log('Left: ' + shape.getLeft()
                    + 'pt; Top: ' + shape.getTop()
                    + 'pt; Width: ' + shape.getWidth()
                    + 'pt; Height: ' + shape.getHeight()
                    + 'pt; Rotation: ' + shape.getRotation() + '\u00B0.');
```

The expected log is:

```
Left: 100pt; Top: 200pt; Width: 50pt; Height: 60pt; Rotation: 90°.
```

The size, position, and rotation setters can be used in any order or
combination.
Replacing the third line in the preceding script with the following script
produces the same result:

```javascript
shape.setWidth(55);
shape.setRotation(90).setHeight(60).setLeft(100);
shape.setWidth(50).setTop(200);
```

### Scale a page element

Instead of using `setWidth()` and `setHeight()` to set the size of the
shape
to an absolute value, `scaleWidth()` and `scaleHeight()` can be used to stretch
or squeeze a page element with a relative scaling factor.

```javascript
shape.scaleHeight(0.5).scaleWidth(2);
```

The following figure depicts how the preceding code works on a 45°-rotated
square shape. Note that the upper left corner of the bounding box is fixed
during scaling.

![Slides Scaling](https://developers.google.com/static/apps-script/guides/slides/images/slides-script-scaling.png)

### Reflect a page element

The argument in `scaleWidth()` and `scaleHeight()` can be negative so that they
can be used to flip a page element horizontally or vertically.

```javascript
// Flip horizontally along the left edge of the bounding box.
shape.scaleWidth(-1);
// Flip vertically along the top edge of the bounding box.
shape.scaleHeight(-1);
```

The following figure depicts how the preceding code works on a 45°-rotated
shape. Note that the page element is flipped along one of the edges of its
bounding box but not its center.

![Slides Reflection](https://developers.google.com/static/apps-script/guides/slides/images/slides-script-reflection.png)

## Line rotation

Like other page elements, a line's rotation isn't the vertical angle of
the line, but the rotation of its bounding box. When you create a line with
specified start and end points, its rotation is always 0°. Dragging
the endpoints of the line in Slides UI changes its vertical
angle as well as the size and position of its bounding box, but doesn't change
its rotation. Using `setRotation()` rotates the bounding box of the line,
which effectively changes its vertical angle. So two lines can have the same
visual vertical angle, but different bounding boxes and therefore different
size, position, and rotation values.

## Limitations

Some sizing and positioning methods are incompatible with some types of page
elements. The following table summarizes the methods which are not compatible
with certain types of page elements.

| Methods | Shape | Video | Table |
|---|---|---|---|
| **getHeight(), getWidth()** | ✔ | ✔ | NO (returns null) |
| **setHeight(), setWidth()** | ✔ | ✔ | NO |
| **setRotation()** | ✔ | NO | NO |
| **scaleHeight(), scaleWidth()** | ✔ | ✔ | NO |

All sizing and positioning methods may give unexpected results if the page
element has shearing. All limitations are subject to change. Check reference for
up-to-date information.

## Use affine transforms

For advanced control, the size and position of a page element can also be
calculated and adjusted through its inherent (native) size and *affine
transform*.

Google Apps Script provides an interface similar to the Google Slides API
for using affine transforms.

- To read properties, you can use an affine transform, which describes how an
element is scaled, rotated, sheared, and positioned. To learn how to use
an element's transform and inherent (native) size to calculate its
visual size on a slide, see
[Transforms](https://developers.google.com/slides/concepts/transforms). In
Apps Script, use:
    - `getInherentWidth()` and `getInherentHeight()` for the inherent (native)
  size of page elements;
    - `getTransform()` for the affine transform of the page elements.
- To change properties, you can use affine transforms to perform scaling,
rotation, reflection, and more. To learn how to size and position page
elements using affine transforms, see
[Sizing and Positioning](https://developers.google.com/slides/how-tos/transform).
In Apps Script, use:
    - `setTransform()` to set the affine transform of page elements (similar to
  ABSOLUTE mode);
    - `preconcatenateTransform()` to pre-concatenate an affine transform to the
  current transform of page elements (similar to RELATIVE mode).

The following script creates a shape, sets its transform, reads its inherent
size,
and reads its affine transform.

```javascript
var slide = SlidesApp.getActivePresentation().getSlides()[0];
var shape = slide.insertShape(SlidesApp.ShapeType.RECTANGLE);
shape.setTransform(SlidesApp.newAffineTransformBuilder()
                   .setScaleX(2)
                   .setScaleY(1)
                   .setTranslateX(100)
                   .setTranslateY(200)
                   .build());
Logger.log('Inherent width: ' + shape.getInherentWidth()
                              + 'pt; Inherent height: '
                              + shape.getInherentHeight() + 'pt.');
```

The expected log output is:

```
Inherent width: 236.2pt; Inherent height: 236.2pt.
```

The resulting shape has the following transform, rendered size, and position:

```
AffineTransform{scaleX=2.0, scaleY=1.0, shearX=0.0, shearY=0.0, translateX=100.0, translateY=200.0}
Left: 100pt; Top: 200pt; Width: 472.4pt; Height: 236.2pt; Rotation: 0°.
```
