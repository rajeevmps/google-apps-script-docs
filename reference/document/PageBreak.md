# PageBreak

An element representing a page break.

An element representing a page break. A `PageBreak` can be contained within a `ListItem` or `Paragraph`, unless the `ListItem` or `Paragraph` is within a `Table`, `HeaderSection`, `FooterSection`, or `FootnoteSection`. A `PageBreak` cannot itself contain any other element.

## Methods

### copy()

Returns: PageBreak

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

Returns: PageBreak|null

Removes the element from its parent.

### setAttributes(attributes Object)

Returns: PageBreak

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.
