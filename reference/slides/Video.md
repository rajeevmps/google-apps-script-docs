# Video

A `PageElement` representing a video.

## Methods

### alignOnPage(alignmentPosition)

`Video`

Aligns the element to the specified alignment position on the page.

**Parameters**

- `alignmentPosition` (`AlignmentPosition`) — the position to align this page element to on the page.

**Returns**

`Video` — this element, for chaining.

### bringForward()

`Video`

Brings the page element forward on the page by one element. The page element must not be in a group.

**Returns**

`Video` — this element, for chaining.

### bringToFront()

`Video`

Brings the page element to the front of the page. The page element must not be in a group.

**Returns**

`Video` — this element, for chaining.

### duplicate()

`PageElement`

Duplicates the page element.

The duplicate page element is placed on the same page at the same position as the original.

**Returns**

`PageElement` — the new duplicate of this page element.

### getBorder()

`Border`

Returns the `Border` of the video.

**Returns**

`Border` — the border of this video.

### getConnectionSites()

`ConnectionSite[]`

Returns the list of `ConnectionSite`s on the page element, or an empty list if the page element does not have any connection sites.

**Returns**

`ConnectionSite[]` — the connection sites, if any.

### getDescription()

`String`

Returns the page element's alt text description. The description is combined with the title to display and read alt text.

**Returns**

`String` — the page element's alt text description.

### getHeight()

`Number|null`

Gets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Returns**

`Number|null` — the element's height in points, or `null` if the element does not have a height.

### getInherentHeight()

`Number|null`

Returns the element's inherent height in points.

The page element's transform is relative to its inherent size. Use the inherent size together with the element's transform to determine the element's final visual appearance.

**Returns**

`Number|null` — the element's inherent height in points, or `null` if the element does not have a height.

### getInherentWidth()

`Number|null`

Returns the element's inherent width in points.

The page element's transform is relative to its inherent size. Use the inherent size together with the element's transform to determine the element's final visual appearance.

**Returns**

`Number|null` — the element's inherent width in points, or `null` if the element does not have a width.

### getLeft()

`Number`

Returns the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's horizontal position in points, from the upper-left corner of the page.

### getObjectId()

`String`

Returns the unique ID for this object. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for this object.

### getPageElementType()

`PageElementType`

Returns the page element's type, represented as a `PageElementType` enum.

**Returns**

`PageElementType` — the page element's type.

### getParentGroup()

`Group|null`

Returns the group this page element belongs to, or `null` if the element is not in a group.

**Returns**

`Group|null` — the group this page element belongs to, or `null`.

### getParentPage()

`Page`

Returns the page this page element is on.

**Returns**

`Page` — the page this element resides on.

### getRotation()

`Number`

Returns the element's clockwise rotation angle around its center in degrees, where zero degrees means no rotation.

**Returns**

`Number` — the rotation angle in degrees between 0 (inclusive) and 360 (exclusive).

### getSource()

`VideoSourceType`

Gets the video source.

**Returns**

`VideoSourceType` — the video source.

### getThumbnailUrl()

`String`

Gets an URL to the video thumbnail. This URL is tagged with the account of the requester. Anyone with the URL effectively accesses the thumbnail as the original requester. Access to the thumbnail may be lost if the presentation's sharing settings change. The URL expires after a short period of time.

**Returns**

`String` — an URL to the video thumbnail.

### getTitle()

`String`

Returns the page element's alt text title. The title is combined with the description to display and read alt text.

**Returns**

`String` — the page element's alt text title.

### getTop()

`Number`

Gets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's vertical position in points, from the upper-left corner of the page.

### getTransform()

`AffineTransform`

Returns the page element's transform.

The visual appearance of the page element is determined by its absolute transform. To compute the absolute transform, preconcatenate a page element's transform with the transforms of all of its parent groups. If the page element is not in a group, its absolute transform is the same as the value in this field.

**Returns**

`AffineTransform` — the page element's transform.

### getUrl()

`String|null`

Gets an URL to the video. The URL is valid as long as the source video exists and sharing settings do not change. Returns `null` when the video source is not supported.

**Returns**

`String|null` — an URL to the video, or `null` if the source is not supported.

### getVideoId()

`String`

Gets the video source's unique identifier for this video.

**Returns**

`String` — the video source's unique identifier.

### getWidth()

`Number|null`

Returns the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Returns**

`Number|null` — the element's width in points, or `null` if the element does not have a width.

### preconcatenateTransform(transform)

`Video`

Preconcatenates the provided transform to the existing transform of the page element.

**Parameters**

- `transform` (`AffineTransform`) — the transform to preconcatenate onto this page element's transform.

**Returns**

`Video` — this element, for chaining.

### remove()

`void`

Removes the page element.

If after a remove operation, a `Group` contains only one or no page elements, the group itself is also removed.

If the page element is not in a group, and if the page element is removed from a placeholder that inherits properties from a placeholder on the layout or master, then the placeholder itself is removed.

### scaleHeight(ratio)

`Video`

Scales the element's height by the specified ratio. The element's height is the height of its bounding box when the element has no rotation.

**Parameters**

- `ratio` (`Number`) — the ratio to scale this element's height by.

**Returns**

`Video` — this element, for chaining.

### scaleWidth(ratio)

`Video`

Scales the element's width by the specified ratio. The element's width is the width of its bounding box when the element has no rotation.

**Parameters**

- `ratio` (`Number`) — the ratio to scale this element's width by.

**Returns**

`Video` — this element, for chaining.

### select()

`void`

Selects only the `PageElement` in the active presentation and removes any previous selection. This is same as calling `select(true)`.

A script can only access the selection of the user who is running the script, and only if the script is bound to the presentation.

### select(replace)

`void`

Selects the `PageElement` in the active presentation.

**Parameters**

- `replace` (`Boolean`) — if `true`, the selection replaces any previous selection; otherwise the selection is added to any previous selection.

### sendBackward()

`Video`

Sends the page element backward on the page by one element.

**Returns**

`Video` — this element, for chaining.

### sendToBack()

`Video`

Sends the page element to the back of the page.

**Returns**

`Video` — this element, for chaining.

### setDescription(description)

`Video`

Sets the page element's alt text description.

**Parameters**

- `description` (`String`) — the string to set the alt text description to.

**Returns**

`Video` — this element, for chaining.

### setHeight(height)

`Video`

Sets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Parameters**

- `height` (`Number`) — the new height of this element to set, in points.

**Returns**

`Video` — this element, for chaining.

### setLeft(left)

`Video`

Sets the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `left` (`Number`) — the new horizontal position to set, in points.

**Returns**

`Video` — this element, for chaining.

### setRotation(angle)

`Video`

Sets the element's clockwise rotation angle around its center in degrees.

**Parameters**

- `angle` (`Number`) — the new clockwise rotation angle to set, in degrees.

**Returns**

`Video` — this element, for chaining.

### setTitle(title)

`Video`

Sets the page element's alt text title.

**Parameters**

- `title` (`String`) — the string to set the alt text title to.

**Returns**

`Video` — this element, for chaining.

### setTop(top)

`Video`

Sets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `top` (`Number`) — the new vertical position to set, in points.

**Returns**

`Video` — this element, for chaining.

### setTransform(transform)

`Video`

Sets the transform of the page element with the provided transform.

Updating the transform of a group changes the absolute transform of the page elements in that group, which changes their visual appearance.

Updating the transform of a page element that is in a group only changes the transform of that page element; it doesn't affect the transforms of the group or other page elements in the group.

**Parameters**

- `transform` (`AffineTransform`) — the transform to set for this page element.

**Returns**

`Video` — this element, for chaining.

### setWidth(width)

`Video`

Sets the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Parameters**

- `width` (`Number`) — the new width of this element to set, in points.

**Returns**

`Video` — this element, for chaining.

## Properties

None.
