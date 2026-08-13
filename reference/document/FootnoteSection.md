# FootnoteSection

An element representing a footnote section.

A `FootnoteSection` contains the text that corresponds to a `Footnote`. The `FootnoteSection` may contain `ListItem` or `Paragraph` elements.

## Methods

### appendParagraph(paragraph)

Parameters: `paragraph: Paragraph` — The paragraph to append.

Returns: `Paragraph`

Appends the given `Paragraph`. Use this version of `appendParagraph` when appending a copy of an existing `Paragraph`.

### appendParagraph(text)

Parameters: `text: String` — The paragraph's text contents.

Returns: `Paragraph`

Creates and appends a new `Paragraph` containing the specified text contents.

### clear()

Returns: `FootnoteSection`

Clears the contents of the element.

### copy()

Returns: `FootnoteSection`

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### editAsText()

Returns: `Text`

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as `InlineImage` and `HorizontalRule`). Child elements fully contained within a deleted text range are removed from the element.

### findElement(elementType)

Parameters: `elementType: ElementType` — The type of element to search for.

Returns: `RangeElement|null`

Searches the contents of the element for a descendant of the specified type.

### findElement(elementType, from)

Parameters:
- `elementType: ElementType` — The type of element to search for
- `from: RangeElement` — The search result to search from

Returns: `RangeElement|null`

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

### findText(searchPattern)

Parameters: `searchPattern: String` — the pattern to search for

Returns: `RangeElement|null`

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### findText(searchPattern, from)

Parameters:
- `searchPattern: String` — the pattern to search for
- `from: RangeElement` — the search result to search from

Returns: `RangeElement|null`

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

### getAttributes()

Returns: `Object`

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

### getChild(childIndex)

Parameters: `childIndex: Integer` — The index of the child element to retrieve.

Returns: `Element`

Retrieves the child element at the specified child index.

### getChildIndex(child)

Parameters: `child: Element` — The child element for which to retrieve the index.

Returns: `Integer`

Retrieves the child index for the specified child element.

### getNextSibling()

Returns: `Element|null`

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getNumChildren()

Returns: `Integer`

Retrieves the number of children.

### getParagraphs()

Returns: `Paragraph[]|null`

Retrieves all the `Paragraphs` contained in the section (including `ListItems`).

### getParent()

Returns: `ContainerElement|null`

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: `Element|null`

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getText()

Returns: `String`

Retrieves the contents of the element as a text string.

### getTextAlignment()

Returns: `TextAlignment|null`

Gets the text alignment. The available types of alignment are `DocumentApp.TextAlignment.NORMAL`, `DocumentApp.TextAlignment.SUBSCRIPT`, and `DocumentApp.TextAlignment.SUPERSCRIPT`. Returns null if the text contains multiple types of alignments or if the alignment has never been set.

### getType()

Returns: `ElementType`

Retrieves the element's `ElementType`. Use `getType()` to determine the exact type of a given element.

### insertParagraph(childIndex, paragraph)

Parameters:
- `childIndex: Integer` — The index at which to insert
- `paragraph: Paragraph` — The paragraph to insert

Returns: `Paragraph`

Inserts the given `Paragraph` at the specified index.

### insertParagraph(childIndex, text)

Parameters:
- `childIndex: Integer` — The index at which to insert
- `text: String` — The paragraph's text contents

Returns: `Paragraph`

Creates and inserts a new `Paragraph` at the specified index, containing the specified text contents.

### removeChild(child)

Parameters: `child: Element` — The child element to remove.

Returns: `FootnoteSection`

Removes the specified child element.

### removeFromParent()

Returns: `FootnoteSection|null`

Removes the element from its parent.

### replaceText(searchPattern, replacement)

Parameters:
- `searchPattern: String` — The pattern to search for
- `replacement: String` — The replacement string

Returns: `Element`

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions.

### setAttributes(attributes)

Parameters: `attributes: Object` — An object representing element attributes from `DocumentApp.Attribute`

Returns: `FootnoteSection`

Sets the element's attributes.

### setText(text)

Parameters: `text: String` — The element contents

Returns: `FootnoteSection`

Sets the contents as plain text.

### setTextAlignment(textAlignment)

Parameters: `textAlignment: TextAlignment` — The alignment type

Returns: `FootnoteSection`

Sets the text alignment.

## Deprecated Methods

### getFootnotes()

Returns: `Footnote[]|null`

Retrieves all the `Footnotes` contained in the section.

### getLinkUrl()

Returns: `String|null`

Retrieves the link url.

### isAtDocumentEnd()

Returns: `Boolean`

Determines whether the element is at the end of the `Document`.

### setLinkUrl(url)

Parameters: `url: String` — The link URL

Returns: `FootnoteSection`

Sets the link url.

## Properties

None.
