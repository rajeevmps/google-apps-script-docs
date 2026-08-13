# RichLink

An element representing a link to a Google resource, such as a Drive file or a YouTube video.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### copy()

Returns: RichLink

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getMimeType()

Returns: String | null

Returns the MIME type of the linked resource for a Google Drive file, or `null` otherwise.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getTitle()

Returns: String

Returns the link's displayed title.

### getType()

Returns: ElementType

Retrieves the element's ElementType. Use `getType()` to determine the exact type of a given element.

### getUrl()

Returns: String

Returns the URL of the resource.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### merge()

Returns: RichLink | null

Merges the element with the preceding sibling of the same type. Only elements of the same ElementType can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeFromParent()

Returns: RichLink | null

Removes the element from its parent.

### setAttributes(attributes Object)

Returns: RichLink

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.
