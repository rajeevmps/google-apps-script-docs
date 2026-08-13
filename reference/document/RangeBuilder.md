# RangeBuilder

A builder used to construct Range objects from document elements.

A builder used to construct `Range` objects from document elements. The class provides methods to add entire or partial elements, elements between two points, or contents of another range, with a `build()` method to construct the final `Range` object.

## Example

```javascript
const doc = DocumentApp.getActiveDocument();
const documentTab = doc.getActiveTab().asDocumentTab();
const rangeBuilder = documentTab.newRange();
const tables = documentTab.getBody().getTables();
for (let i = 0; i < tables.length; i++) {
  rangeBuilder.addElement(tables[i]);
}
doc.setSelection(rangeBuilder.build());
```

## Methods

### addElement(element)

Returns: RangeBuilder

Adds an entire `Element` to this `RangeBuilder`.

**Parameters:**
- `element` (Element)

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### addElement(textElement, startOffset, endOffsetInclusive)

Returns: RangeBuilder

Adds a partial `Text` element to this `RangeBuilder`.

**Parameters:**
- `textElement` (Text)
- `startOffset` (Integer) — the number of characters before the first character to be included (that is, the index of the first character in the range)
- `endOffsetInclusive` (Integer) — the number of characters before the last character to be included (that is, the index of the last character in the range)

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### addElementsBetween(startElement, endElementInclusive)

Returns: RangeBuilder

Adds two entire elements, and all elements between them, to this `RangeBuilder`.

**Parameters:**
- `startElement` (Element)
- `endElementInclusive` (Element)

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### addElementsBetween(startTextElement, startOffset, endTextElementInclusive, endOffsetInclusive)

Returns: RangeBuilder

Adds two partial `Text` elements, and all elements between them, to the `RangeBuilder`.

**Parameters:**
- `startTextElement` (Text)
- `startOffset` (Integer) — the number of characters before the first character of `startTextElement` to be included (that is, the index of the first character in the range)
- `endTextElementInclusive` (Text)
- `endOffsetInclusive` (Integer) — the number of characters before the last character of `endTextElementInclusive` to be included (that is, the index of the last character in the range)

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### addRange(range)

Returns: RangeBuilder

Adds the contents of another `Range` to this `RangeBuilder`.

**Parameters:**
- `range` (Range)

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### build()

Returns: Range

Constructs a `Range` from the settings applied to the builder.

### getRangeElements()

Returns: RangeElement[]

Gets all elements in this `Range`, including any partial `Text` elements (for example, in the case of a selection that includes only part of a `Text` element).

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getSelectedElements()

*Deprecated. Renamed to `getRangeElements()`.*

Returns: RangeElement[]

Gets all elements that the user has selected in the open instance of the document, including any partially selected `Text` elements.

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`
