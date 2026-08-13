# HorizontalRule

An element representing a horizontal rule.

An element representing an horizontal rule. A `HorizontalRule` can be contained within a `ListItem` or `Paragraph`, but cannot itself contain any other element.

All methods require authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### copy()

Returns: HorizontalRule

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

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

### removeFromParent()

Returns: HorizontalRule|null

Removes the element from its parent.

### setAttributes(attributes Object)

Returns: HorizontalRule

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.
