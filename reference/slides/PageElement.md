# PageElement

A visual element rendered on a page.

"A visual element rendered on a page."

PageElement represents a visual element rendered on a page. It provides methods to align, duplicate, remove, and manage position, size, rotation, title, description, and transform of elements on the page. It also provides methods to cast the element to its more specific type (Group, Image, Line, Shape, SheetsChart, SpeakerSpotlight, Table, Video, WordArt).

## Methods

### alignOnPage(alignmentPosition)

`PageElement`

Aligns the element to the specified alignment position on the page.

**Parameters**

- `alignmentPosition` (`AlignmentPosition`) — the position to align this page element to on the page.

**Returns**

`PageElement` — this element, for chaining.

### asGroup()

`Group`

Returns the page element as a group.

**Returns**

`Group` — this page element as a group.

### asImage()

`Image`

Returns the page element as an image.

**Returns**

`Image` — this page element as an image.

### asLine()

`Line`

Returns the page element as a line.

**Returns**

`Line` — this page element as a line.

### asShape()

`Shape`

Returns the page element as a shape.

**Returns**

`Shape` — this page element as a shape.

### asSheetsChart()

`SheetsChart`

Returns the page element as a linked chart embedded from Google Sheets.

**Returns**

`SheetsChart` — this page element as a Sheets chart.

### asSpeakerSpotlight()

`SpeakerSpotlight`

Returns the page element as a speaker spotlight.

**Returns**

`SpeakerSpotlight` — this page element as a speaker spotlight.

### asTable()

`Table`

Returns the page element as a table.

**Returns**

`Table` — this page element as a table.

### asVideo()

`Video`

Returns the page element as a video.

**Returns**

`Video` — this page element as a video.

### asWordArt()

`WordArt`

Returns the page element as word art.

**Returns**

`WordArt` — this page element as word art.

### bringForward()

`PageElement`

Brings the page element forward on the page by one element.

**Returns**

`PageElement` — this element, for chaining.

### bringToFront()

`PageElement`

Brings the page element to the front of the page.

**Returns**

`PageElement` — this element, for chaining.

### duplicate()

`PageElement`

Duplicates the page element. The duplicate page element is placed on the same page at the same position as the original.

**Returns**

`PageElement` — the new duplicate of this page element.

### getConnectionSites()

`ConnectionSite[]`

Returns the list of ConnectionSites on the page element, or an empty list if the page element does not have any connection sites.

**Returns**

`ConnectionSite[]` — the connection sites on this page element.

### getDescription()

`String`

Returns the page element's alt text description.

**Returns**

`String` — the page element's alt text description.

### getHeight()

`Number|null`

Gets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Returns**

`Number|null` — the element's height in points, or null if the element does not have a height.

### getInherentHeight()

`Number|null`

Returns the element's inherent height in points.

**Returns**

`Number|null` — the element's inherent height in points, or null if the element does not have a height.

### getInherentWidth()

`Number|null`

Returns the element's inherent width in points.

**Returns**

`Number|null` — the element's inherent width in points, or null if the element does not have a width.

### getLeft()

`Number`

Returns the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's horizontal position in points.

### getObjectId()

`String`

Returns the unique ID for this object.

**Returns**

`String` — the unique ID for this object.

### getPageElementType()

`PageElementType`

Returns the page element's type, represented as a PageElementType enum.

**Returns**

`PageElementType` — the page element's type.

### getParentGroup()

`Group|null`

Returns the group this page element belongs to, or null if the element is not in a group.

**Returns**

`Group|null` — the group this page element belongs to, or null.

### getParentPage()

`Page`

Returns the page this page element is on.

**Returns**

`Page` — the page this page element is on.

### getRotation()

`Number`

Returns the element's clockwise rotation angle around its center in degrees, where zero degrees means no rotation.

**Returns**

`Number` — the rotation angle in degrees.

### getTitle()

`String`

Returns the page element's alt text title.

**Returns**

`String` — the page element's alt text title.

### getTop()

`Number`

Gets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's vertical position in points.

### getTransform()

`AffineTransform`

Returns the page element's transform.

**Returns**

`AffineTransform` — the page element's transform.

### getWidth()

`Number|null`

Returns the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Returns**

`Number|null` — the element's width in points, or null if the element does not have a width.

### preconcatenateTransform(transform)

`PageElement`

Preconcatenates the provided transform to the existing transform of the page element.

**Parameters**

- `transform` (`AffineTransform`) — the transform to preconcatenate onto this page element's transform.

**Returns**

`PageElement` — this element, for chaining.

### remove()

`void`

Removes the page element.

**Returns**

`void`

### scaleHeight(ratio)

`PageElement`

Scales the element's height by the specified ratio.

**Parameters**

- `ratio` (`Number`) — the ratio to scale the height by.

**Returns**

`PageElement` — this element, for chaining.

### scaleWidth(ratio)

`PageElement`

Scales the element's width by the specified ratio.

**Parameters**

- `ratio` (`Number`) — the ratio to scale the width by.

**Returns**

`PageElement` — this element, for chaining.

### select()

`void`

Selects only the PageElement in the active presentation and removes any previous selection.

**Returns**

`void`

### select(replace)

`void`

Selects the PageElement in the active presentation.

**Parameters**

- `replace` (`Boolean`) — whether to replace the existing selection.

**Returns**

`void`

### sendBackward()

`PageElement`

Sends the page element backward on the page by one element.

**Returns**

`PageElement` — this element, for chaining.

### sendToBack()

`PageElement`

Sends the page element to the back of the page.

**Returns**

`PageElement` — this element, for chaining.

### setDescription(description)

`PageElement`

Sets the page element's alt text description.

**Parameters**

- `description` (`String`) — the string to set the alt text description to.

**Returns**

`PageElement` — this element, for chaining.

### setHeight(height)

`PageElement`

Sets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Parameters**

- `height` (`Number`) — the height to set, in points.

**Returns**

`PageElement` — this element, for chaining.

### setLeft(left)

`PageElement`

Sets the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `left` (`Number`) — the horizontal position to set, in points.

**Returns**

`PageElement` — this element, for chaining.

### setRotation(angle)

`PageElement`

Sets the element's clockwise rotation angle around its center in degrees.

**Parameters**

- `angle` (`Number`) — the rotation angle to set, in degrees.

**Returns**

`PageElement` — this element, for chaining.

### setTitle(title)

`PageElement`

Sets the page element's alt text title.

**Parameters**

- `title` (`String`) — the string to set the alt text title to.

**Returns**

`PageElement` — this element, for chaining.

### setTop(top)

`PageElement`

Sets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `top` (`Number`) — the vertical position to set, in points.

**Returns**

`PageElement` — this element, for chaining.

### setTransform(transform)

`PageElement`

Sets the transform of the page element with the provided transform.

**Parameters**

- `transform` (`AffineTransform`) — the transform to set for this page element.

**Returns**

`PageElement` — this element, for chaining.

### setWidth(width)

`PageElement`

Sets the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Parameters**

- `width` (`Number`) — the width to set, in points.

**Returns**

`PageElement` — this element, for chaining.

**Authorization**

All methods require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
