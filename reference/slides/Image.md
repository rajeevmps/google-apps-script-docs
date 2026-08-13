# Image

A PageElement representing an image.

A `PageElement` representing an image.

## Methods

### alignOnPage(alignmentPosition)

`Image`

Aligns the element to the specified alignment position on the page.

**Parameters**

- `alignmentPosition` (`AlignmentPosition`)

**Returns**

`Image` — this element, for chaining

### bringForward()

`Image`

Brings the page element forward on the page by one element. The page element must not be in a group.

**Returns**

`Image` — this element, for chaining

### bringToFront()

`Image`

Brings the page element to the front of the page. The page element must not be in a group.

**Returns**

`Image` — this element, for chaining

### duplicate()

`PageElement`

Duplicates the page element. The duplicate page element is placed on the same page at the same position as the original.

**Returns**

`PageElement` — the new duplicate of this page element

### getAs(contentType)

`Blob`

Return the data inside this object as a blob converted to the specified content type.

**Parameters**

- `contentType` (`String`) — the MIME type to convert to

**Returns**

`Blob` — the data as a blob

### getBlob()

`Blob`

Return the data inside this image as a blob.

**Returns**

`Blob` — the image data as a blob

### getBorder()

`Border`

Returns the `Border` of the image.

**Returns**

`Border` — the border of this image

### getConnectionSites()

`ConnectionSite[]`

Returns the list of `ConnectionSite`s on the page element, or an empty list if the page element does not have any connection sites.

**Returns**

`ConnectionSite[]` — the connection sites on the page element

### getContentUrl()

`String`

Gets a URL to the image. This URL is tagged with the account of the requester, so anyone with the URL effectively accesses the image as the original requester. Access to the image may be lost if the presentation's sharing settings change. The returned URL expires after a short period of time.

**Returns**

`String` — a URL to the image

### getDescription()

`String`

Returns the page element's alt text description. The description is combined with the title to display and read alt text.

**Returns**

`String` — the page element's alt text description

### getHeight()

`Number`

Gets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Returns**

`Number` — the element's height in points, or `null`

### getInherentHeight()

`Number`

Returns the element's inherent height in points. The page element's transform is relative to its inherent size.

**Returns**

`Number` — the element's inherent height in points, or `null`

### getInherentWidth()

`Number`

Returns the element's inherent width in points. The page element's transform is relative to its inherent size.

**Returns**

`Number` — the element's inherent width in points, or `null`

### getLeft()

`Number`

Returns the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Returns**

`Number` — this element's horizontal position in points

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

### getParentPlaceholder()

`PageElement`

Returns the parent page element of the placeholder. Returns `null` if the image is not a placeholder or has no parent.

**Returns**

`PageElement` — the parent page element of the placeholder, or `null`

### getPlaceholderIndex()

`Integer`

Returns the index of the placeholder image. If two or more placeholder images on the same page are the same type, they each have a unique index value. Returns `null` if the image isn't a placeholder.

**Returns**

`Integer` — the index of the placeholder image, or `null`

### getPlaceholderType()

`PlaceholderType`

Returns the placeholder type of the image, or `PlaceholderType.NONE` if the shape is not a placeholder.

**Returns**

`PlaceholderType` — the placeholder type of this image

### getRotation()

`Number`

Returns the element's clockwise rotation angle around its center in degrees, where zero degrees means no rotation.

**Returns**

`Number` — the rotation angle in degrees

### getSourceUrl()

`String`

Gets the image's source URL, if available. When an image is inserted by URL, returns the URL provided during image insertion.

**Returns**

`String` — the image URL, or `null` if the image doesn't have a source URL

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

Returns the page element's transform. The visual appearance of the page element is determined by its absolute transform.

**Returns**

`AffineTransform` — the page element's transform

### getWidth()

`Number`

Returns the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Returns**

`Number` — the element's width in points, or `null`

### preconcatenateTransform(transform)

`Image`

Preconcatenates the provided transform to the existing transform of the page element.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Image` — this element, for chaining

### remove()

`void`

Removes the page element.

### removeLink()

`void`

Removes a `Link`.

### replace(blobSource)

`Image`

Replaces this image with an image described by a `BlobSource` object.

**Parameters**

- `blobSource` (`BlobSource`)

**Returns**

`Image` — this element, for chaining

### replace(blobSource, crop)

`Image`

Replaces this image with an image described by an `Image` object, optionally cropping the image to fit.

**Parameters**

- `blobSource` (`BlobSource`)
- `crop` (`Boolean`)

**Returns**

`Image` — this element, for chaining

### replace(imageUrl)

`Image`

Replaces this image with another image downloaded from the provided URL.

**Parameters**

- `imageUrl` (`String`)

**Returns**

`Image` — this element, for chaining

### replace(imageUrl, crop)

`Image`

Replaces this image with another image downloaded from the provided URL, optionally cropping the image to fit.

**Parameters**

- `imageUrl` (`String`)
- `crop` (`Boolean`)

**Returns**

`Image` — this element, for chaining

### scaleHeight(ratio)

`Image`

Scales the element's height by the specified ratio.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Image` — this element, for chaining

### scaleWidth(ratio)

`Image`

Scales the element's width by the specified ratio.

**Parameters**

- `ratio` (`Number`)

**Returns**

`Image` — this element, for chaining

### select()

`void`

Selects only the `PageElement` in the active presentation and removes any previous selection.

### select(replace)

`void`

Selects the `PageElement` in the active presentation.

**Parameters**

- `replace` (`Boolean`)

### sendBackward()

`Image`

Sends the page element backward on the page by one element.

**Returns**

`Image` — this element, for chaining

### sendToBack()

`Image`

Sends the page element to the back of the page.

**Returns**

`Image` — this element, for chaining

### setDescription(description)

`Image`

Sets the page element's alt text description.

**Parameters**

- `description` (`String`)

**Returns**

`Image` — this element, for chaining

### setHeight(height)

`Image`

Sets the element's height in points, which is the height of the element's bounding box when the element has no rotation.

**Parameters**

- `height` (`Number`)

**Returns**

`Image` — this element, for chaining

### setLeft(left)

`Image`

Sets the element's horizontal position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `left` (`Number`)

**Returns**

`Image` — this element, for chaining

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

`Image`

Sets the element's clockwise rotation angle around its center in degrees.

**Parameters**

- `angle` (`Number`)

**Returns**

`Image` — this element, for chaining

### setTitle(title)

`Image`

Sets the page element's alt text title.

**Parameters**

- `title` (`String`)

**Returns**

`Image` — this element, for chaining

### setTop(top)

`Image`

Sets the element's vertical position in points, measured from the upper-left corner of the page when the element has no rotation.

**Parameters**

- `top` (`Number`)

**Returns**

`Image` — this element, for chaining

### setTransform(transform)

`Image`

Sets the transform of the page element with the provided transform.

**Parameters**

- `transform` (`AffineTransform`)

**Returns**

`Image` — this element, for chaining

### setWidth(width)

`Image`

Sets the element's width in points, which is the width of the element's bounding box when the element has no rotation.

**Parameters**

- `width` (`Number`)

**Returns**

`Image` — this element, for chaining
