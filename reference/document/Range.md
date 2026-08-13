# Range

A range of elements in a document.

A range of elements in a document. The user's selection is represented as a `Range`, among other uses.

Scripts can only access the selection of the user who is running the script, and only if the script is bound to the document.

## Example

```javascript
// Bold all selected text.
const selection = DocumentApp.getActiveDocument().getSelection();
if (selection) {
  const elements = selection.getRangeElements();
  for (let i = 0; i < elements.length; i++) {
    const element = elements[i];

    // Only modify elements that can be edited as text; skip images and other
    // non-text elements.
    if (element.getElement().editAsText) {
      const text = element.getElement().editAsText();

      // Bold the selected part of the element, or the full element if it's
      // completely selected.
      if (element.isPartial()) {
        text.setBold(
            element.getStartOffset(),
            element.getEndOffsetInclusive(),
            true,
        );
      } else {
        text.setBold(true);
      }
    }
  }
}
```

## Methods

### getRangeElements()

Returns: RangeElement[]

Gets all elements in this `Range`, including any partial `Text` elements (for example, in the case of a selection that includes only part of a `Text` element).

**Return:** an array of elements, in the order they appear in the document

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`

### getSelectedElements()

*Deprecated. Renamed to `getRangeElements()`.*

Returns: RangeElement[]

Gets all elements that the user has selected in the open instance of the document, including any partially selected `Text` elements.

**Return:** an array of selected or partially selected elements, in the order they appear in the document

**Authorization Required:** `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`
