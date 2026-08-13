# ContainerElement

A generic element that may contain other elements.

A generic element that may contain other elements. All elements that may contain child elements, such as `Paragraph`, inherit from `ContainerElement`.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `asBody()` | `Body` | Returns the current element as a `Body` |
| `asEquation()` | `Equation` | Returns the current element as an `Equation` |
| `asFooterSection()` | `FooterSection` | Returns the current element as a `FooterSection` |
| `asFootnoteSection()` | `FootnoteSection` | Returns the current element as a `FootnoteSection` |
| `asHeaderSection()` | `HeaderSection` | Returns the current element as a `HeaderSection` |
| `asListItem()` | `ListItem` | Returns the current element as a `ListItem` |
| `asParagraph()` | `Paragraph` | Returns the current element as a `Paragraph` |
| `asTable()` | `Table` | Returns the current element as a `Table` |
| `asTableCell()` | `TableCell` | Returns the current element as a `TableCell` |
| `asTableOfContents()` | `TableOfContents` | Returns the current element as a `TableOfContents` |
| `asTableRow()` | `TableRow` | Returns the current element as a `TableRow` |
| `clear()` | `ContainerElement` | Clears the contents of the element |
| `copy()` | `ContainerElement` | Returns a detached, deep copy of the current element |
| `editAsText()` | `Text` | Obtains a `Text` version of the current element, for editing |
| `findElement(elementType)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type |
| `findElement(elementType, from)` | `RangeElement\|null` | Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement` |
| `findText(searchPattern)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern using regular expressions |
| `findText(searchPattern, from)` | `RangeElement\|null` | Searches the contents of the element for the specified text pattern, starting from a given search result |
| `getAttributes()` | `Object` | Retrieves the element's attributes |
| `getChild(childIndex)` | `Element` | Retrieves the child element at the specified child index |
| `getChildIndex(child)` | `Integer` | Retrieves the child index for the specified child element |
| `getLinkUrl()` | `String\|null` | Retrieves the link url |
| `getNextSibling()` | `Element\|null` | Retrieves the element's next sibling element |
| `getNumChildren()` | `Integer` | Retrieves the number of children |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element |
| `getPreviousSibling()` | `Element\|null` | Retrieves the element's previous sibling element |
| `getText()` | `String` | Retrieves the contents of the element as a text string |
| `getTextAlignment()` | `TextAlignment\|null` | Gets the text alignment |
| `getType()` | `ElementType` | Retrieves the element's `ElementType` |
| `isAtDocumentEnd()` | `Boolean` | Determines whether the element is at the end of the `Document` |
| `merge()` | `ContainerElement\|null` | Merges the element with the preceding sibling of the same type |
| `removeFromParent()` | `ContainerElement\|null` | Removes the element from its parent |
| `replaceText(searchPattern, replacement)` | `Element` | Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions |
| `setAttributes(attributes)` | `ContainerElement` | Sets the element's attributes |
| `setLinkUrl(url)` | `ContainerElement` | Sets the link url |
| `setTextAlignment(textAlignment)` | `ContainerElement` | Sets the text alignment |

### asBody()

Returns: Body

Returns the current element as a `Body`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asEquation()

Returns: Equation

Returns the current element as an `Equation`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asFooterSection()

Returns: FooterSection

Returns the current element as a `FooterSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asFootnoteSection()

Returns: FootnoteSection

Returns the current element as a `FootnoteSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asHeaderSection()

Returns: HeaderSection

Returns the current element as a `HeaderSection`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asListItem()

Returns: ListItem

Returns the current element as a `ListItem`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asParagraph()

Returns: Paragraph

Returns the current element as a `Paragraph`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTable()

Returns: Table

Returns the current element as a `Table`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableCell()

Returns: TableCell

Returns the current element as a `TableCell`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableOfContents()

Returns: TableOfContents

Returns the current element as a `TableOfContents`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### asTableRow()

Returns: TableRow

Returns the current element as a `TableRow`. Use this method to aid auto-complete whenever a given element is known to be of a specific type.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### clear()

Returns: ContainerElement — The current element.

Clears the contents of the element.

### copy()

Returns: ContainerElement

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### editAsText()

Returns: Text

Obtains a `Text` version of the current element, for editing. Use `editAsText` for manipulating the elements contents as rich text. The `editAsText` mode ignores non-text elements (such as `InlineImage` and `HorizontalRule`). Child elements fully contained within a deleted text range are removed from the element.

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Insert two paragraphs separated by a paragraph containing an
// horizontal rule.
body.insertParagraph(0, 'An editAsText sample.');
body.insertHorizontalRule(0);
body.insertParagraph(0, 'An example.');

// Delete " sample.\n\n An" removing the horizontal rule in the process.
body.editAsText().deleteText(14, 25);
```

### findElement(elementType)

Returns: RangeElement|null — A search result indicating the position of the search element.

Searches the contents of the element for a descendant of the specified type.

Parameters:
- `elementType` (`ElementType`): The type of element to search for.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findElement(elementType, from)

Returns: RangeElement|null — A search result indicating the next position of the search element.

Searches the contents of the element for a descendant of the specified type, starting from the specified `RangeElement`.

Parameters:
- `elementType` (`ElementType`): The type of element to search for.
- `from` (`RangeElement`): The search result to search from.

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Define the search parameters.
let searchResult = null;

// Search until the paragraph is found.
while ((searchResult = body.findElement(DocumentApp.ElementType.PARAGRAPH, searchResult))) {
  const par = searchResult.getElement().asParagraph();
  if (par.getHeading() === DocumentApp.ParagraphHeading.HEADING1) {
    // Found one, update and stop.
    par.setText('This is the first header.');
    break;
  }
}
```

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findText(searchPattern)

Returns: RangeElement|null — a search result indicating the position of the search text, or null if there is no match

Searches the contents of the element for the specified text pattern using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Parameters:
- `searchPattern` (`String`): the pattern to search for

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### findText(searchPattern, from)

Returns: RangeElement|null — a search result indicating the next position of the search text, or null if there is no match

Searches the contents of the element for the specified text pattern, starting from a given search result. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers. The provided regular expression pattern is independently matched against each text block contained in the current element.

Parameters:
- `searchPattern` (`String`): the pattern to search for
- `from` (`RangeElement`): the search result to search from

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getAttributes()

Returns: Object — The element's attributes.

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();

// Append a styled paragraph.
const par = body.appendParagraph('A bold, italicized paragraph.');
par.setBold(true);
par.setItalic(true);

// Retrieve the paragraph's attributes.
const atts = par.getAttributes();

// Log the paragraph attributes.
for (const att in atts) {
  Logger.log(`${att}:${atts[att]}`);
}
```

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getChild(childIndex)

Returns: Element — The child element at the specified index.

Retrieves the child element at the specified child index.

Parameters:
- `childIndex` (`Integer`): The index of the child element to retrieve.

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Obtain the first element in the tab.
const firstChild = body.getChild(0);

// If it's a paragraph, set its contents.
if (firstChild.getType() === DocumentApp.ElementType.PARAGRAPH) {
  firstChild.asParagraph().setText('This is the first paragraph.');
}
```

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getChildIndex(child)

Returns: Integer — The child index.

Retrieves the child index for the specified child element.

Parameters:
- `child` (`Element`): The child element for which to retrieve the index.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getLinkUrl()

Returns: String|null — the link url, or null if the element contains multiple values for this attribute

Retrieves the link url.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getNextSibling()

Returns: Element|null — The next sibling element.

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getNumChildren()

Returns: Integer — The number of children.

Retrieves the number of children.

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();

// Log the number of elements in the tab.
Logger.log(`There are ${body.getNumChildren()} elements in the tab's body.`);
```

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getParent()

Returns: ContainerElement|null — The parent element.

Retrieves the element's parent element. The parent element contains the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getPreviousSibling()

Returns: Element|null — The previous sibling element.

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getText()

Returns: String — The contents of the element as a text string.

Retrieves the contents of the element as a text string.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getTextAlignment()

Returns: TextAlignment|null — The text alignment, or null if the element contains multiple values for this attribute

Gets the text alignment.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getType()

Returns: ElementType — The element's type.

Retrieves the element's `ElementType`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### isAtDocumentEnd()

Returns: Boolean — Whether the element is at the end of the document.

Determines whether the element is at the end of the `Document`.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### merge()

Returns: ContainerElement|null — The merged element, or null if the element cannot be merged.

Merges the element with the preceding sibling of the same type. Only elements of the same ElementType can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### removeFromParent()

Returns: ContainerElement|null — The element that was removed.

Removes the element from its parent. If the element is not an isolated child of its parent, the containing paragraph is split. All children of the current element are moved to the preceding sibling element. The current element itself is removed.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### replaceText(searchPattern, replacement)

Returns: Element — the current element

Replaces all occurrences of a given text pattern with a given replacement string, using regular expressions. A subset of the JavaScript regular expression features are not fully supported, such as capture groups and mode modifiers.

Parameters:
- `searchPattern` (`String`): the pattern to search for
- `replacement` (`String`): the text to use as replacement

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setAttributes(attributes)

Returns: ContainerElement — The current element.

Sets the element's attributes. The `attributes` parameter must be an object where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration and each property value is the desired new value to be applied.

Parameters:
- `attributes` (`Object`): The element's attributes.

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setLinkUrl(url)

Returns: ContainerElement — The current element.

Sets the link url.

Parameters:
- `url` (`String`): the link url

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### setTextAlignment(textAlignment)

Returns: ContainerElement — The current element.

Sets the text alignment.

Parameters:
- `textAlignment` (`TextAlignment`): the text alignment

Authorization: Requires `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

## Properties

None.
