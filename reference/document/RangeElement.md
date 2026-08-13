# RangeElement

A wrapper around an Element with a possible start and end offset.

A wrapper around an Element with a possible start and end offset. These offsets allow a range of characters within a Text element to be represented in search results, document selections, and named ranges.

## Methods

### getElement()

Returns: Element

Gets the Element that corresponds to this RangeElement.

```javascript
const rangeElement = DocumentApp.getActiveDocument()
    .getSelection().getRangeElements()[0];
Logger.log(`Element type: ${rangeElement.getElement().getType()}`);
if (rangeElement.isPartial()) {
  Logger.log(
      `The character range begins at ${rangeElement.getStartOffset()}`);
  Logger.log(
      `The character range ends at ${rangeElement.getEndOffsetInclusive()}`);
} else {
  Logger.log('The entire range element is included.');
}
```

### getEndOffsetInclusive()

Returns: Integer

Gets the position of the end of a partial range within the range element. If the element is a Text element and isPartial() returns true, the offset is the number of characters before the last character in the range (that is, the index of the last character in the range); in any other case, this method returns -1.

### getStartOffset()

Returns: Integer

Gets the position of the start of a partial range within the range element. If the element is a Text element and isPartial() returns true, the offset is the number of characters before the start of the range (that is, the index of the first character in the range); in any other case, this method returns -1.

### isPartial()

Returns: Boolean

Determines whether this range element covers the entire element or a partial selection of the element's characters.
