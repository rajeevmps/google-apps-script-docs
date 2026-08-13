# Select items in a presentation

## Page Summary

- The selection is what is currently selected in an open presentation page, such as text or a table.
- Scripts can only access the selection of the user running the script, and the selection is a snapshot from when the script started.
- You can read the selection using the `Selection` class and the `SelectionType` enum helps identify the type of selected objects.
- The script can modify the user's selection, and these changes are reflected in subsequent script operations and appear in the user's browser after execution or calling `saveAndClose()`.
- Text within shapes or table cells can be selected, and unselecting can be achieved by selecting a page as the current page or selecting a specific page element.

The *selection* is the content that has focus on an open presentation
page,
such as a span of highlighted text or a table. This guide describes how to get
and set the selection in an active presentation using
Apps Script.

A script can only access the selection of the user running the script.

The selection is a snapshot of what it was when the script started. If the user
clicks and the selection changes while the script is running, those changes
won't be reflected.

## Selections and selection type

Read the selection using the
[Selection](https://developers.google.com/apps-script/reference/slides/selection)
class. The class has various methods to get the selected objects based on the
type of selected object(s).

The [SelectionType](https://developers.google.com/apps-script/reference/slides/selection-type) enum
represents the specific type of selected objects. For example, if the user has
selected some text in a shape, the selection type is **TEXT**. In this case,
you can retrieve the selected range of text using the
`selection.getTextRange()` method.

You can also retrieve the object that contains the selection. For example,
you could retrieve the shape containing the selected text using
`selection.getPageElementRange().getPageElements()[0]`. Similarly, the page that
contains the enclosing shape is the current active page; to
retrieve that page, use `selection.getCurrentPage()`.

## Reading the selection

To read the selection, use the
[Presentation.getSelection()](https://developers.google.com/apps-script/reference/slides/presentation#getselection)
method as shown in the following example:

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
```

### Read the current page

To retrieve the current [Page](https://developers.google.com/apps-script/reference/slides/page) that the
user is viewing, use the
[getSelection()](https://developers.google.com/apps-script/reference/slides/presentation#getselection)
and
[getCurrentPage()](https://developers.google.com/apps-script/reference/slides/selection#getcurrentpage)
methods as follows:

```javascript
const currentPage = SlidesApp.getActivePresentation()
  .getSelection()
  .getCurrentPage();
```

Note that the current page may be any one of the following types:

- [Slide](https://developers.google.com/apps-script/reference/slides/slide)
- [Master](https://developers.google.com/apps-script/reference/slides/master)
- [Layout](https://developers.google.com/apps-script/reference/slides/layout)

The current page can have one or more objects selected, and the SelectionType
determines the type of selection.

### Read the selection based on the selection type

The following example shows how you can use the selection type to read the
current selection in a type-appropriate way.

```javascript
const selection = SlidesApp.getActivePresentation().getSelection();
const selectionType = selection.getSelectionType();
let currentPage;
switch (selectionType) {
  case SlidesApp.SelectionType.NONE:
    console.log("Nothing selected");
    break;
  case SlidesApp.SelectionType.CURRENT_PAGE:
    currentPage = selection.getCurrentPage();
    console.log(`Selection is a page with ID: ${currentPage.getObjectId()}`);
    break;
  case SlidesApp.SelectionType.PAGE_ELEMENT: {
    const pageElements = selection.getPageElementRange().getPageElements();
    console.log(`There are ${pageElements.length} page elements selected.`);
    break;
  }
  case SlidesApp.SelectionType.TEXT: {
    const tableCellRange = selection.getTableCellRange();
    if (tableCellRange !== null) {
      const tableCell = tableCellRange.getTableCells()[0];
      console.log(
        `Selected text is in a table at row ${tableCell.getRowIndex()}, column ${tableCell.getColumnIndex()}`,
      );
    }
    const textRange = selection.getTextRange();
    if (textRange.getStartIndex() === textRange.getEndIndex()) {
      console.log(`Text cursor position: ${textRange.getStartIndex()}`);
    } else {
      console.log(
        `Selection is a text range from: ${textRange.getStartIndex()} to: ${textRange.getEndIndex()} is selected`,
      );
    }
    break;
  }
  case SlidesApp.SelectionType.TABLE_CELL: {
    const tableCells = selection.getTableCellRange().getTableCells();
    const table = tableCells[0].getParentTable();
    console.log(`There are ${tableCells.length} table cells selected.`);
    break;
  }
  case SlidesApp.SelectionType.PAGE: {
    const pages = selection.getPageRange().getPages();
    console.log(`There are ${pages.length} pages selected.`);
    break;
  }
  default:
    break;
}
```

### Read text selections

Read the text selection using the
[Selection.getTextRange()](https://developers.google.com/slides/reference/selection#gettextrange) method.
There are two types of text selection:

- **Range selection**: If a shape contains the text "Hello", and "He" is
selected, the returned range has startIndex=0, and endIndex=2.
- **Cursor selection**: If a shape contains the text "Hello", and cursor is
after "H" ("H|ello"), the returned range is empty range with
startIndex=1 and endIndex=1.

## Modifying the selection

The script can modify the user's selection.
Any selection changes that the script makes to the presentation are reflected
in subsequent selection operations for the duration of the script execution.

The selection changes are reflected on the user's browser only after the script
execution completes, or when `Presentation.saveAndClose()` is called.

### Selecting the current page

A page in the active presentation can be selected as the current page by calling
the
[selectAsCurrentPage()](https://developers.google.com/apps-script/reference/slides/page#selectascurrentpage)
method.
This method removes any previous page element, page, or text selection. So using
this method on the current page lets you unselect any current selections on the
page. For example:

```javascript
// Select the first slide as the current page selection and remove any previous selection.
const selection = SlidesApp.getActivePresentation().getSelection();
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.selectAsCurrentPage();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.CURRENT_PAGE
// selection.getCurrentPage() = slide
//
```

### Select a page element

To select a page element in a page, use the
[PageElement.select()](https://developers.google.com/apps-script/reference/slides/page-element#select)
method.
This also unselects any previously selected page elements.

The `select()` and `select(true)` methods are equivalent.

For example:

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const pageElement = slide.getPageElements()[0];
// Only select this page element and remove any previous selection.
pageElement.select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.PAGE_ELEMENT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = pageElement
//
```

### Select multiple page elements

To append additional page elements to the selection, use the
[PageElement.select(false)](https://developers.google.com/apps-script/reference/slides/page-element#selectreplace)
method.
All the page elements must be in the current page.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
// First select the slide page, as the current page selection.
slide.selectAsCurrentPage();
// Then select all the page elements in the selected slide page.
const pageElements = slide.getPageElements();
for (let i = 0; i < pageElements.length; i++) {
  pageElements[i].select(false);
}
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.PAGE_ELEMENT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements() = pageElements
//
```

### Transform the selection

Edits that your script performs can *transform* the current selection, so that
what's selected changes as a result of the edit.
For example:

1. Suppose you have two shapes A and B selected.
2. Next your script removes shape A.
3. As a result, the selection is transformed against the edit so that only
shape B is selected.

The following example shows how the selection can be transformed by manipulating
selected page elements.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const shape1 = slide.getPageElements()[0].asShape();
const shape2 = slide.getPageElements()[1].asShape();
// Select both the shapes.
shape1.select();
shape2.select(false);
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.PAGE_ELEMENT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements() = [shape1, shape2]
//
// Remove one shape.
shape2.remove();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.PAGE_ELEMENT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements() = [shape1]
//
```

## Select text

Text contained in a shape or in a table cell can be selected using the
[TextRange.select()](https://developers.google.com/apps-script/reference/slides/text-range#select) method.
If the text is contained in a shape, then that shape is also selected.
If the text is contained in a table cell, then that table cell and its enclosing
table are both selected.

This also sets the parent page as the current page.

### Range selection in a shape

The following example shows how to make a range selection within text contained
in a shape.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const shape = slide.getPageElements()[0].asShape();
shape.getText().setText("Hello");
// Range selection: Select the text range 'He'.
shape.getText().getRange(0, 2).select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = shape
// selection.getTextRange().getStartIndex() = 0
// selection.getTextRange().getEndIndex() = 2
//
```

### Cursor selection in a shape

The following example shows how to make a cursor selection within text contained
in a shape.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const shape = slide.getPageElements()[0].asShape();
shape.getText().setText("Hello");
// Cursor selection: Place the cursor after 'H' like 'H|ello'.
shape.getText().getRange(1, 1).select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = shape
// selection.getTextRange().getStartIndex() = 1
// selection.getTextRange().getEndIndex() = 1
//
```

### Range selection in a table cell

The following example shows how to make a range selection within text contained
in a table cell.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const table = slide.getPageElements()[0].asTable();
const tableCell = table.getCell(0, 1);
tableCell.getText().setText("Hello");
// Range selection: Select the text range 'He'.
tableCell.getText().getRange(0, 2).select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = table
// selection.getTableCellRange().getTableCells()[0] = tableCell
// selection.getTextRange().getStartIndex() = 0
// selection.getTextRange().getEndIndex() = 2
//
```

### Cursor selection in TableCell

The following example shows how to make a cursor selection within text contained
in a table cell.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const table = slide.getPageElements()[0].asTable();
const tableCell = table.getCell(0, 1);
tableCell.getText().setText("Hello");
// Cursor selection: Place the cursor after 'H' like 'H|ello'.
tableCell.getText().getRange(1, 1).select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = table
// selection.getTableCellRange().getTableCells()[0] = tableCell
// selection.getTextRange().getStartIndex() = 1
// selection.getTextRange().getEndIndex() = 1
//
```

### Selection transformation with textual edits

The following example shows how the selection can be transformed by editing the
selected text.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const shape = slide.getPageElements()[0].asShape();
const textRange = shape.getText();
textRange.setText("World");
// Select all the text 'World'.
textRange.select();
// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = shape
// selection.getTextRange().getStartIndex() = 0
// selection.getTextRange().getEndIndex() = 6
//
// Add some text to the shape, and the selection will be transformed.
textRange.insertText(0, "Hello ");

// State of selection
//
// selection.getSelectionType() = SlidesApp.SelectionType.TEXT
// selection.getCurrentPage() = slide
// selection.getPageElementRange().getPageElements()[0] = shape
// selection.getTextRange().getStartIndex() = 0
// selection.getTextRange().getEndIndex() = 12
//
```

## Unselect

There are no explicit methods to unselect text or page elements. However, this
result can be achieved using the `Page.selectAsCurrentPage()` or
`pageElement.select()` methods.

### Select a current page

The following example shows how to unselect any current selections on a page
by setting that page as the current page.

```javascript
// Unselect one or more page elements already selected.
//
// In case one or more page elements in the first slide are selected, setting the
// same (or any other) slide page as the current page would do the unselect.
//
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.selectAsCurrentPage();
```

### Select a page element

The following example shows how to unselect any current selections on a page
by selecting one page element, thus removing all other items from the selection.

```javascript
// Unselect one or more page elements already selected.
//
// In case one or more page elements in the first slide are selected,
// selecting any pageElement in the first slide (or any other pageElement) would
// do the unselect and select that pageElement.
//
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.getPageElements()[0].select();
```
