# Date

An element representing a formatted date.

An element representing a formatted date. A Date element represents a formatted date and includes methods to retrieve and set its attributes, display text, locale, and timestamp. The element provides methods for document structure manipulation like getting siblings and parent, checking if it's at the document end, merging with a preceding sibling, and removing itself from its parent. The element can be copied to create a detached, deep copy including any child elements.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `copy()` | `Date` | Returns a detached, deep copy of the current element |
| `getAttributes()` | `Object` | Retrieves the element's attributes |
| `getDisplayText()` | `String` | Returns the display value rendered in the document |
| `getLocale()` | `String` | Returns the date's locale used for the display value |
| `getNextSibling()` | `Element\|null` | Retrieves the element's next sibling element |
| `getParent()` | `ContainerElement\|null` | Retrieves the element's parent element |
| `getPreviousSibling()` | `Element\|null` | Retrieves the element's previous sibling element |
| `getTimestamp()` | `Date` | Returns the timestamp associated with the date |
| `getType()` | `ElementType` | Retrieves the element's ElementType |
| `isAtDocumentEnd()` | `Boolean` | Determines whether element is at document end |
| `merge()` | `Date\|null` | Merges the element with preceding sibling of same type |
| `removeFromParent()` | `Date\|null` | Removes the element from its parent |
| `setAttributes(attributes)` | `Date` | Sets the element's attributes |

### copy()

Returns: Date — The new copy.

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

### getAttributes()

Returns: Object — The element's attributes.

Retrieves the element's attributes. The result is an object containing a property for each valid element attribute where each property name corresponds to an item in the `DocumentApp.Attribute` enumeration.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
const par = body.appendParagraph('A bold, italicized paragraph.');
par.setBold(true);
par.setItalic(true);
const atts = par.getAttributes();
for (const att in atts) {
  Logger.log(`${att}:${atts[att]}`);
}
```

### getDisplayText()

Returns: String — The display value.

Returns the display value that's rendered in the document. The display value uses the UTC timezone and the date's locale. For example, `Jul 16, 2021`.

### getLocale()

Returns: String — The locale of the date.

Returns the date's locale used for the display value. For example, `en`.

### getNextSibling()

Returns: Element|null — The next sibling element.

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement|null — The parent element.

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element|null — The previous sibling element.

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getTimestamp()

Returns: Date — The timestamp.

Returns the timestamp associated with the date.

### getType()

Returns: ElementType — The element type.

Retrieves the element's `ElementType`. Use `getType()` to determine the exact type of a given element.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
const firstChild = body.getChild(0);
if (firstChild.getType() === DocumentApp.ElementType.PARAGRAPH) {
  Logger.log('The first element is a paragraph.');
} else {
  Logger.log('The first element is not a paragraph.');
}
```

### isAtDocumentEnd()

Returns: Boolean — Whether the element is at the end of the tab.

Determines whether the element is at the end of the `Document`.

### merge()

Returns: Date|null — The merged element.

Merges the element with the preceding sibling of the same type. Only elements of the same `ElementType` can be merged. Any child elements contained in the current element are moved to the preceding sibling element. The current element is removed from the document.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
const par1 = body.appendParagraph('Paragraph 1.');
const par2 = body.appendParagraph('Paragraph 2.');
par2.merge();
const cells = [
  ['Row 1, Cell 1', 'Row 1, Cell 2'],
  ['Row 2, Cell 1', 'Row 2, Cell 2'],
];
const table = body.appendTable(cells);
const row = table.getRow(0);
const cell1 = row.getCell(0);
const cell2 = row.getCell(1);
const merged = cell2.merge();
```

### removeFromParent()

Returns: Date|null — The removed element.

Removes the element from its parent.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
const imgs = body.getImages();
for (let i = 0; i < imgs.length; i++) {
  imgs[i].removeFromParent();
}
```

### setAttributes(attributes)

Returns: Date — The current element.

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

Parameters:
- `attributes` (`Object`): The element's attributes.

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const body = documentTab.getBody();
const style = {};
style[DocumentApp.Attribute.HORIZONTAL_ALIGNMENT] =
    DocumentApp.HorizontalAlignment.RIGHT;
style[DocumentApp.Attribute.FONT_FAMILY] = 'Calibri';
style[DocumentApp.Attribute.FONT_SIZE] = 18;
style[DocumentApp.Attribute.BOLD] = true;
const par = body.appendParagraph('A paragraph with custom style.');
par.setAttributes(style);
```

## Properties

None.
