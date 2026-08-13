# PageBackground

Describes a slide's background properties.

The `PageBackground` class describes a slide's background properties in Google Slides presentations.

## Methods

### getPictureFill()

`PictureFill|null`

Get the stretched picture fill of this background, or `null` if the background fill type is not `PageBackgroundType.PICTURE`.

**Returns**

`PictureFill|null` — the picture fill, or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSolidFill()

`SolidFill|null`

Get the solid fill of this background, or `null` if the background fill type is not `PageBackgroundType.SOLID`.

**Returns**

`SolidFill|null` — the solid fill, or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getType()

`PageBackgroundType`

Get the type of this page background.

**Returns**

`PageBackgroundType` — the type of this page background.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isVisible()

`Boolean`

Whether the background is visible.

**Returns**

`Boolean` — whether the background is visible.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setPictureFill(blobSource)

`void`

Sets an image from the specified image blob as the page background. The image is stretched to match the dimensions of the page. Inserting the image fetches it from the `BlobSource` once and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format.

**Parameters**

- `blobSource` (`BlobSource`) — the image data.

**Returns**

`void`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setPictureFill(imageUrl)

`void`

Sets the image at the provided URL as the page background. The image is stretched to match the dimensions of the page. Inserting the image fetches it from the URL once and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format. The provided URL must be publicly accessible and no larger than 2kB. The URL itself is saved with the image and exposed via `PictureFill.getSourceUrl()`.

**Parameters**

- `imageUrl` (`String`) — the image URL.

**Returns**

`void`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setSolidFill(color)

`void`

Sets the solid fill to the given `Color`.

**Parameters**

- `color` (`Color`) — the color to set.

**Returns**

`void`

### setSolidFill(color, alpha)

`void`

Sets the solid fill to the given alpha and `Color`.

**Parameters**

- `color` (`Color`) — the color to set.
- `alpha` (`Number`) — the alpha to set.

**Returns**

`void`

### setSolidFill(red, green, blue)

`void`

Sets the solid fill to the given RGB values.

**Parameters**

- `red` (`Integer`) — the red value.
- `green` (`Integer`) — the green value.
- `blue` (`Integer`) — the blue value.

**Returns**

`void`

### setSolidFill(red, green, blue, alpha)

`void`

Sets the solid fill to the given alpha and RGB values.

**Parameters**

- `red` (`Integer`) — the red value.
- `green` (`Integer`) — the green value.
- `blue` (`Integer`) — the blue value.
- `alpha` (`Number`) — the alpha to set.

**Returns**

`void`

### setSolidFill(hexString)

`void`

Sets the solid fill to the given hex color string.

**Parameters**

- `hexString` (`String`) — the hex color string.

**Returns**

`void`

### setSolidFill(hexString, alpha)

`void`

Sets the solid fill to the given alpha and hex color string.

**Parameters**

- `hexString` (`String`) — the hex color string.
- `alpha` (`Number`) — the alpha to set.

**Returns**

`void`

### setSolidFill(color) [ThemeColorType]

`void`

Sets the solid fill to the given `ThemeColorType`.

**Parameters**

- `color` (`ThemeColorType`) — the theme color type.

**Returns**

`void`

### setSolidFill(color, alpha) [ThemeColorType]

`void`

Sets the solid fill to the given alpha and `ThemeColorType`.

**Parameters**

- `color` (`ThemeColorType`) — the theme color type.
- `alpha` (`Number`) — the alpha to set.

**Returns**

`void`

All `setSolidFill` overloads require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setTransparent()

`void`

Sets the background to transparent.

**Returns**

`void`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
