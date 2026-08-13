# ImageCropStyle

A class that represents a crop style that can be applied to image components. You can't set the size of an image or resize it, but you can crop the image.

## Methods

### setAspectRatio(ratio: Number): ImageCropStyle

Sets the aspect ratio to use if the crop type is `RECTANGLE_CUSTOM`. The ratio must be a positive value.

Parameters:
- `ratio` (Number) - The ratio to apply.

Returns: ImageCropStyle object for chaining.

Throws: Error if the input is negative or zero.

### setImageCropType(type: ImageCropType): ImageCropStyle

Sets the crop type for the image. Default is SQUARE.

Parameters:
- `type` (ImageCropType) - The crop type.

Returns: ImageCropStyle object for chaining.
