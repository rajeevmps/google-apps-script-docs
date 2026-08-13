# TableOfContents

An element containing a table of contents.

A `TableOfContents` may contain `ListItem`, `Paragraph`, and `Table` elements, although the contents of a `TableOfContents` are usually generated automatically by Google Docs.

Scripts that use these methods require authorization with one or more of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

## Methods

### clear()

Returns: TableOfContents

Clears the contents of the element.

### copy()

Returns: TableOfContents

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: Text

Obtains a Text version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as InlineImage and HorizontalRule). Child elements fully contained within a deleted text range are removed from the element.

### findElement(elementType ElementType)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType ElementType, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for a descendant of the specified type, starting from the specified RangeElement.

### findText(searchPattern String)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern using regular expressions. A subset of JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### findText(searchPattern String, from RangeElement)

Returns: RangeElement | null

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### getAttributes()

Returns: Object

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getChild(childIndex Integer)

Returns: Element

Retrieves the child element at the specified child index.

### getChildIndex(child Element)

Returns: Integer

Retrieves the child index for the specified child element.

### getLinkUrl()

Returns: String | null

Retrieves the link url.

### getNextSibling()

Returns: Element | null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumChildren()

Returns: Integer

Retrieves the number of children.

### getParent()

Returns: ContainerElement | null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element | null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getText()

Returns: String

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: TextAlignment | null

Gets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.

### getType()

Returns: ElementType

Retrieves the element's ElementType. Use `getType()` to determine the exact type of a given element.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the Document.

### removeFromParent()

Returns: TableOfContents | null

Removes the element from its parent.

### replaceText(searchPattern String, replacement String)

Returns: Element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions. The search pattern is passed as a string, not a JavaScript regular expression object. Because of this you'll need to escape any backslashes in the pattern. This method uses Google's RE2 regular expression library, which limits the supported syntax. The provided regular expression pattern is independently matched against each text block contained in the current element.

### setAttributes(attributes Object)

Returns: TableOfContents

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

### setLinkUrl(url String)

Returns: TableOfContents

Sets the link url.

### setTextAlignment(textAlignment TextAlignment)

Returns: TableOfContents

Sets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`.
