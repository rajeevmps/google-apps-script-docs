# Group

A collection of page elements joined as a single unit.

A Group is a collection of PageElements joined as a single unit. Groups can be aligned, duplicated, and have their children retrieved. You can get and set properties such as height, width, left, top, rotation, title, and description. Methods exist to change layering (bring forward, bring to front, send backward, send to back). Groups can be removed or ungrouped.

## Methods

### alignOnPage(alignmentPosition)

`Group`

Aligns the element to the specified alignment position on the page.

**Parameters**

- `alignmentPosition` (`AlignmentPosition`)

**Returns**

`Group` — this element, for chaining

### bringForward()

`Group`

Brings the page element forward on the page by one element. The page element must not be in a group.

**Returns**

`Group` — this element, for chaining

### bringToFront()

`Group`

Brings the page element to the front of the page. The page element must not be in a group.

**Returns**

`Group` — this element, for chaining

### duplicate()

`PageElement`

Duplicates the page element. The duplicate page element is placed on the same page at the same position as the original.

**Returns**

`PageElement` — the new duplicate of this page element

### getChildren()

`PageElement[]`

Gets the collection of page elements in the group. The minimum size of a group is 2.

**Returns**

`PageElement[]` — the list of page elements in the group

### getConnectionSites()

`ConnectionSite[]`

Returns the list of ConnectionSites on the page element, or an empty list if the page element does not have any connection sites.

**Returns**

`ConnectionSite[]` — the connection sites on the page element

### getDescription()

`String`

Returns the page element's alt text description. The description is combined with the title to display and read alt text.

**Returns**

`String` — the page element's alt text description

### getHeight()

`Number`

Gets the element's height in points, which is the height of the element's bounding box when the element has no rotation. This method isn't compatible with all page elements.

**Returns**

`Number` — the element's height in points, or `null` if the element does not have a height

### getInherentHeight()

`Number`

Returns the element's inherent height in points. The page element's transform is relative to its inherent size.

**Returns**

`Number` — the element's inherent height in points, or `null` if the element does not have a height

### getInherentWidth()

`Number`

Returns the element's inherent width in points. The page element's transform is relative to its inherent size.

**Returns**

`Number` — the element's inherent width in points, or `null` if the element does not have a width

### getLeft()

`Number`

Returns the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's horizontal position in points

### getObjectId()

`String`

Returns the unique ID for this object. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for this object

### getPageElementType()

`PageElementType`

Returns the page element's type, represented as a PageElementType enum.

**Returns**

`PageElementType` — the page element's type

### getParentGroup()

`Group`

Returns the group this page element belongs to, or null if the element is not in a group.

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

Gets the page element's transform. The initial transform for a newly created Group is always the identity transform: 1.0 scale parameters, and 0.0 shear and translate parameters.

**Returns**

`AffineTransform` — the page element's transform

### getWidth()

`Number`

Returns the element's width in points, which is the width of the element's bounding box when the element has no rotation. This method isn't compatible with all page elements.

**Returns**

`Number` — the element's width in points, or `null` if the element does not have a width

### preconcatenateTransform(transform)

`Group`

Preconcatenates the provided transform to the existing transform of the page element. newTransform = argument * existingTransform.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Group` — this element, for chaining

### remove()

`void`

Removes the page element. If after a remove operation, a Group contains only one or no page elements, the group itself is also removed.

### scaleHeight(ratio)

`Group`

Scales the element's height by the specified ratio. The element's height is the height of its bounding box when the element has no rotation.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Group` — this element, for chaining

### scaleWidth(ratio)

`Group`

Scales the element's width by the specified ratio. The element's width is the width of its bounding box when the element has no rotation.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Group` — this element, for chaining

### select()

`void`

Selects only the PageElement in the active presentation and removes any previous selection. This is the same as calling select(replace) with true.

### select(replace)

`void`

Selects the PageElement in the active presentation. Pass true to select only the PageElement and remove any previous selection. Pass false to select multiple PageElement objects on the same Page.

**Parameters**

- `replace` (`Boolean`)

### sendBackward()

`Group`

Sends the page element backward on the page by one element.

**Returns**

`Group` — this element, for chaining

### sendToBack()

`Group`

Sends the page element to the back of the page.

**Returns**

`Group` — this element, for chaining

### setDescription(description)

`Group`

Sets the page element's alt text description.

**Parameters**

- `description` (`String`)

**Returns**

`Group` — this element, for chaining

### setHeight(height)

`Group`

Sets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Parameters**

- `height` (`Number`)

**Returns**

`Group` — this element, for chaining

### setLeft(left)

`Group`

Sets the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `left` (`Number`)

**Returns**

`Group` — this element, for chaining

### setRotation(angle)

`Group`

Sets the element's clockwise rotation angle around its center in degrees.

**Parameters**

- `angle` (`Number`)

**Returns**

`Group` — this element, for chaining

### setTitle(title)

`Group`

Sets the page element's alt text title.

**Parameters**

- `title` (`String`)

**Returns**

`Group` — this element, for chaining

### setTop(top)

`Group`

Sets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `top` (`Number`)

**Returns**

`Group` — this element, for chaining

### setTransform(transform)

`Group`

Sets the transform of the page element with the provided transform.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Group` — this element, for chaining

### setWidth(width)

`Group`

Sets the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Parameters**

- `width` (`Number`)

**Returns**

`Group` — this element, for chaining

### ungroup()

`void`

Ungroups the elements of the group.
