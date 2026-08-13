# Line

A PageElement representing a line.

A `PageElement` representing a line.

## Methods

### alignOnPage(alignmentPosition)

`Line`

Aligns the element to the specified alignment position on the page.

**Parameters**

- `alignmentPosition` (`AlignmentPosition`)

**Returns**

`Line` — this element, for chaining

### bringForward()

`Line`

Brings the page element forward on the page by one element. The page element must not be in a group.

**Returns**

`Line` — this element, for chaining

### bringToFront()

`Line`

Brings the page element to the front of the page. The page element must not be in a group.

**Returns**

`Line` — this element, for chaining

### duplicate()

`PageElement`

Duplicates the page element. The duplicate page element is placed on the same page at the same position as the original.

**Returns**

`PageElement` — the new duplicate of this page element

### getConnectionSites()

`ConnectionSite[]`

Returns the list of `ConnectionSite`s on the page element, or an empty list if the page element does not have any connection sites.

**Returns**

`ConnectionSite[]` — the connection sites on the page element

### getDashStyle()

`DashStyle`

Gets the `DashStyle` of the line.

**Returns**

`DashStyle` — the dash style of the line

### getDescription()

`String`

Returns the page element's alt text description. The description is combined with the title to display and read alt text.

**Returns**

`String` — the page element's alt text description

### getEnd()

`Point`

Returns the end point of the line, measured from the upper-left corner of the page.

**Returns**

`Point` — the end point of the line

### getEndArrow()

`ArrowStyle`

Gets the `ArrowStyle` of the arrow at the end of the line.

**Returns**

`ArrowStyle` — the arrow style at the end of the line

### getEndConnection()

`ConnectionSite`

Returns the connection at the end of the line, or `null` if there is no connection.

**Returns**

`ConnectionSite` — the connection at the end of the line, or `null`

### getHeight()

`Number`

Gets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Returns**

`Number` — the element's height in points, or `null`

### getInherentHeight()

`Number`

Returns the element's inherent height in points. The page element's transform is relative to its inherent size. Use the inherent size in conjunction with the element's transform to determine the element's final visual appearance.

**Returns**

`Number` — the element's inherent height in points, or `null`

### getInherentWidth()

`Number`

Returns the element's inherent width in points. The page element's transform is relative to its inherent size. Use the inherent size in conjunction with the element's transform to determine the element's final visual appearance.

**Returns**

`Number` — the element's inherent width in points, or `null`

### getLeft()

`Number`

Returns the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's horizontal position in points

### getLineCategory()

`LineCategory`

Gets the `LineCategory` of the line.

**Returns**

`LineCategory` — the line category

### getLineFill()

`LineFill`

Gets the `LineFill` of the line.

**Returns**

`LineFill` — the fill of the line

### getLineType()

`LineType`

Gets the `LineType` of the line.

**Returns**

`LineType` — the line type

### getLink()

`Link`

Returns the `Link` or `null` if there is no link.

**Returns**

`Link` — the link, or `null`

### getObjectId()

`String`

Returns the unique ID for this object. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for this object

### getPageElementType()

`PageElementType`

Returns the page element's type, represented as a `PageElementType` enum.

**Returns**

`PageElementType` — the page element's type

### getParentGroup()

`Group`

Returns the group this page element belongs to, or `null` if the element is not in a group.

**Returns**

`Group` — the group this page element belongs to, or `null`

### getParentPage()

`Page`

Returns the page this page element is on.

**Returns**

`Page` — the page this element resides on

### getRotation()

`Number`

Returns the element's clockwise rotation angle around its center in degrees, where zero degrees means no rotation.

**Returns**

`Number` — the rotation angle in degrees

### getStart()

`Point`

Returns the start point of the line, measured from the upper-left corner of the page.

**Returns**

`Point` — the start point of the line

### getStartArrow()

`ArrowStyle`

Gets the `ArrowStyle` of the arrow at the beginning of the line.

**Returns**

`ArrowStyle` — the arrow style at the start of the line

### getStartConnection()

`ConnectionSite`

Returns the connection at the beginning of the line, or `null` if there is no connection.

**Returns**

`ConnectionSite` — the connection at the start of the line, or `null`

### getTitle()

`String`

Returns the page element's alt text title. The title is combined with the description to display and read alt text.

**Returns**

`String` — the page element's alt text title

### getTop()

`Number`

Gets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's vertical position in points

### getTransform()

`AffineTransform`

Returns the page element's transform.

**Returns**

`AffineTransform` — the page element's transform

### getWeight()

`Number`

Returns the thickness of the line in points.

**Returns**

`Number` — the thickness of the line in points

### getWidth()

`Number`

Returns the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Returns**

`Number` — the element's width in points, or `null`

### isConnector()

`Boolean`

Returns `true` if the line is a connector, or `false` if not.

**Returns**

`Boolean` — whether the line is a connector

### preconcatenateTransform(transform)

`Line`

Preconcatenates the provided transform to the existing transform of the page element.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Line` — this element, for chaining

### remove()

`void`

Removes the page element.

### removeLink()

`void`

Removes a `Link`.

### reroute()

`Line`

Reroutes the start and end of the line to the closest two connection sites on the connected page elements.

**Returns**

`Line` — this element, for chaining

### scaleHeight(ratio)

`Line`

Scales the element's height by the specified ratio.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Line` — this element, for chaining

### scaleWidth(ratio)

`Line`

Scales the element's width by the specified ratio.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Line` — this element, for chaining

### select()

`void`

Selects only the `PageElement` in the active presentation and removes any previous selection.

### select(replace)

`void`

Selects the `PageElement` in the active presentation.

**Parameters**

- `replace` (`Boolean`)

### sendBackward()

`Line`

Sends the page element backward on the page by one element.

**Returns**

`Line` — this element, for chaining

### sendToBack()

`Line`

Sends the page element to the back of the page.

**Returns**

`Line` — this element, for chaining

### setDashStyle(style)

`Line`

Sets the `DashStyle` of the line.

**Parameters**

- `style` (`DashStyle`)

**Returns**

`Line` — this element, for chaining

### setDescription(description)

`Line`

Sets the page element's alt text description.

**Parameters**

- `description` (`String`)

**Returns**

`Line` — this element, for chaining

### setEnd(left, top)

`Line`

Sets the position of the end point of the line.

**Parameters**

- `left` (`Number`)
- `top` (`Number`)

**Returns**

`Line` — this element, for chaining

### setEnd(point)

`Line`

Sets the position of the end point of the line.

**Parameters**

- `point` (`Point`)

**Returns**

`Line` — this element, for chaining

### setEndArrow(style)

`Line`

Sets the `ArrowStyle` of the arrow at the end of the line.

**Parameters**

- `style` (`ArrowStyle`)

**Returns**

`Line` — this element, for chaining

### setEndConnection(connectionSite)

`Line`

Sets the connection at the end of the line.

**Parameters**

- `connectionSite` (`ConnectionSite`)

**Returns**

`Line` — this element, for chaining

### setHeight(height)

`Line`

Sets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Parameters**

- `height` (`Number`)

**Returns**

`Line` — this element, for chaining

### setLeft(left)

`Line`

Sets the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `left` (`Number`)

**Returns**

`Line` — this element, for chaining

### setLineCategory(lineCategory)

`Line`

Sets the `LineCategory` of the line.

**Parameters**

- `lineCategory` (`LineCategory`)

**Returns**

`Line` — this element, for chaining

### setLinkSlide(slideIndex)

`Link`

Sets a `Link` to the given `Slide` using the zero-based index of the slide.

**Parameters**

- `slideIndex` (`Integer`)

**Returns**

`Link` — the link that was set

### setLinkSlide(slide)

`Link`

Sets a `Link` to the given `Slide`, the link is set by the given slide ID.

**Parameters**

- `slide` (`Slide`)

**Returns**

`Link` — the link that was set

### setLinkSlide(slidePosition)

`Link`

Sets a `Link` to the given `Slide` using the relative position of the slide.

**Parameters**

- `slidePosition` (`SlidePosition`)

**Returns**

`Link` — the link that was set

### setLinkUrl(url)

`Link`

Sets a `Link` to the given non-empty URL string.

**Parameters**

- `url` (`String`)

**Returns**

`Link` — the link that was set

### setRotation(angle)

`Line`

Sets the element's clockwise rotation angle around its center in degrees.

**Parameters**

- `angle` (`Number`)

**Returns**

`Line` — this element, for chaining

### setStart(left, top)

`Line`

Sets the position of the start point of the line.

**Parameters**

- `left` (`Number`)
- `top` (`Number`)

**Returns**

`Line` — this element, for chaining

### setStart(point)

`Line`

Sets the position of the start point of the line.

**Parameters**

- `point` (`Point`)

**Returns**

`Line` — this element, for chaining

### setStartArrow(style)

`Line`

Sets the `ArrowStyle` of the arrow at the beginning of the line.

**Parameters**

- `style` (`ArrowStyle`)

**Returns**

`Line` — this element, for chaining

### setStartConnection(connectionSite)

`Line`

Sets the connection at the beginning of the line.

**Parameters**

- `connectionSite` (`ConnectionSite`)

**Returns**

`Line` — this element, for chaining

### setTitle(title)

`Line`

Sets the page element's alt text title.

**Parameters**

- `title` (`String`)

**Returns**

`Line` — this element, for chaining

### setTop(top)

`Line`

Sets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `top` (`Number`)

**Returns**

`Line` — this element, for chaining

### setTransform(transform)

`Line`

Sets the transform of the page element with the provided transform.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Line` — this element, for chaining

### setWeight(points)

`Line`

Sets the thickness of the line in points.

**Parameters**

- `points` (`Number`)

**Returns**

`Line` — this element, for chaining

### setWidth(width)

`Line`

Sets the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Parameters**

- `width` (`Number`)

**Returns**

`Line` — this element, for chaining
