# UnsupportedElement

An element representing a region that is unknown or cannot be affected by a script, such as a page number.

UnsupportedElement represents a region in a document that cannot be affected by a script. You can copy, get attributes, get siblings, get the parent, get the type, and determine if an UnsupportedElement is at the document end. You can also merge an UnsupportedElement with a preceding sibling of the same type or remove it from its parent. The `setAttributes` method allows you to apply a set of attributes to an UnsupportedElement.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### copy()

Returns: UnsupportedElement

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getType()

Returns: ElementType

Retrieves the element's ElementType. Use `getType()` to determine the exact type of a given element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### merge()

Returns: UnsupportedElement | null

Merges the element with the preceding sibling of the same type. Only elements of the same ElementType can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

### removeFromParent()

Returns: UnsupportedElement | null

Removes the element from its parent.

### setAttributes(attributes Object)

Returns: UnsupportedElement

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.
