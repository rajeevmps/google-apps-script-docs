# InlineDrawing

An element representing an embedded drawing.

An element representing an embedded drawing. An `InlineDrawing` can be contained within a `ListItem` or `Paragraph`, unless the `ListItem` or `Paragraph` is within a `FootnoteSection`. An `InlineDrawing` cannot itself contain any other element.

All methods require authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### copy()

Returns: InlineDrawing

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### getAltDescription()

Returns: String|null

Returns the drawing's alternate description. Returns null if the element lacks an alternate description.

### getAltTitle()

Returns: String|null

Returns the drawing's alternate title. Returns null if the element lacks an alternate title.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getType()

Returns: ElementType

Retrieves the element's `ElementType`. Use `getType()` to determine the exact type of a given element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the `Document`.

### merge()

Returns: InlineDrawing|null

Merges the element with the preceding sibling of the same type. Only elements of the same `ElementType` can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeFromParent()

Returns: InlineDrawing|null

Removes the element from its parent.

### setAltDescription(description String)

Returns: InlineDrawing

Sets the drawing's alternate description. If the given description is `null`, sets the description to the empty string.

### setAltTitle(title String)

Returns: InlineDrawing

Sets the drawing's alternate title. If the given title is `null`, sets the title to the empty string.

### setAttributes(attributes Object)

Returns: InlineDrawing

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.
