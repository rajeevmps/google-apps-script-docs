# Selection

The user's selection in the active presentation.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const currentPage = selection.getCurrentPage();
const selectionType = selection.getSelectionType();
```

## Methods

### getCurrentPage()

`Page|null`

Returns the currently active Page or null if there is no active page.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const currentPage = selection.getCurrentPage();
if (currentPage != null) {
  Logger.log(`Selected current active page ID: ${currentPage.getObjectId()}`);
}
```

**Returns**

`Page|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageElementRange()

`PageElementRange|null`

Returns the PageElementRange collection of PageElement instances that are selected or null if there are no PageElement instances selected.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
if (selectionType === SlidesApp.SelectionType.PAGE_ELEMENT) {
  const currentPage = selection.getCurrentPage();
  const pageElements = selection.getPageElementRange().getPageElements();
  Logger.log(`Number of page elements selected: ${pageElements.length}`);
}
```

**Returns**

`PageElementRange|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageRange()

`PageRange|null`

Returns the PageRange a collection of Page instances in the flimstrip that are selected or null if the selection is not of type SelectionType.PAGE.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
if (selectionType === SlidesApp.SelectionType.PAGE) {
  const pageRange = selection.getPageRange();
  Logger.log(
      `Number of pages in the flimstrip selected: ${
          pageRange.getPages().length}`,
  );
}
```

**Returns**

`PageRange|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSelectionType()

`SelectionType`

Returns the SelectionType.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
if (selectionType === SlidesApp.SelectionType.CURRENT_PAGE) {
  const currentPage = selection.getCurrentPage();
  Logger.log(`Selected current active page ID: ${currentPage.getObjectId()}`);
}
```

**Returns**

`SelectionType`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getTableCellRange()

`TableCellRange|null`

Returns the TableCellRange collection of TableCell instances that are selected or null if there are no TableCell instances selected.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
if (selectionType === SlidesApp.SelectionType.TABLE_CELL) {
  const currentPage = selection.getCurrentPage();
  const tableCells = selection.getTableCellRange().getTableCells();
  const table = tableCells[0].getParentTable();
  Logger.log(`Number of table cells selected: ${tableCells.length}`);
}
```

**Returns**

`TableCellRange|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getTextRange()

`TextRange|null`

Returns the TextRange that is selected or null if the selection is not of type SelectionType.TEXT.

The TextRange represents two scenarios:

1. Range of text selected. For example if a shape has text "Hello", and "He" is selected, the returned range has TextRange.getStartIndex() = 0, and TextRange.getEndIndex() = 2.

2. Cursor position. For example if a shape has text "Hello", and cursor is after "H", ("H|ello"), the returned range has TextRange.getStartIndex() = 1 and TextRange.getEndIndex() = 1.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
if (selectionType === SlidesApp.SelectionType.TEXT) {
  const currentPage = selection.getCurrentPage();
  const pageElement = selection.getPageElementRange().getPageElements()[0];
  const textRange = selection.getTextRange();
  Logger.log(`Text selected: ${textRange.asString()}`);
}
```

**Returns**

`TextRange|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
