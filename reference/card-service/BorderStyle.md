# BorderStyle

Represents a complete border style applied to widgets.

BorderStyle is a class representing a complete border style for widgets. BorderStyle enums are accessed through the parent class, name, and property. The BorderStyle class includes methods to set the corner radius, stroke color, and type of the border.

## Methods

### setCornerRadius(radius: Integer): BorderStyle

Sets the corner radius of the border, for example 8.

Parameters:
- `radius` (Integer): The corner radius to be applied to the border.

Returns: This object, for chaining.

### setStrokeColor(color: String): BorderStyle

Sets the color of the border.

Parameters:
- `color` (String): The color in #RGB format to be applied to the border.

Returns: This object, for chaining.

### setType(type: BorderType): BorderStyle

Sets the type of the border.

Parameters:
- `type` (BorderType): The border type.

Returns: This object, for chaining.
