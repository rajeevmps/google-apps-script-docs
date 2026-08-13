# DocumentTab

A document tab, containing rich text and elements such as tables and lists.

A document tab, containing rich text and elements such as tables and lists. Retrieve a document tab using `Document.getTabs()[tabIndex].asDocumentTab()`.

## Methods

### addBookmark(position)

Returns: Bookmark

Adds a `Bookmark` at the given `Position`.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const paragraph = documentTab.getBody().appendParagraph('My new paragraph.');
const position = documentTab.newPosition(paragraph.getChild(0), 0);
const bookmark = documentTab.addBookmark(position);
console.log(bookmark.getId());
```

### addFooter()

Returns: FooterSection

Adds a tab footer section, if none exists.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const footer = documentTab.addFooter();
footer.setText('This is a footer');
```

### addHeader()

Returns: HeaderSection

Adds a tab header section, if none exists.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const header = documentTab.addHeader();
header.setText('This is a header');
```

### addNamedRange(name, range)

Returns: NamedRange

Adds a `NamedRange`, which is a `Range` that has a name and ID to use for later retrieval. Names aren't necessarily unique, even across tabs; several different ranges in the same document can share the same name, much like a class in HTML. By contrast, IDs are unique within the document, like an ID in HTML. After you add a `NamedRange` you can't modify it, you can only remove it. Any script that accesses the tab can access a `NamedRange`. To avoid unintended conflicts between scripts, consider prefixing range names with a unique string.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const rangeBuilder = documentTab.newRange();
const tables = documentTab.getBody().getTables();
for (let i = 0; i < tables.length; i++) {
  rangeBuilder.addElement(tables[i]);
}
documentTab.addNamedRange('Tab t.0 tables', rangeBuilder.build());
```

### getBody()

Returns: Body

Retrieves the tab's `Body`. Tabs may contain different types of sections (for example, `HeaderSection`, `FooterSection`). The active section for a tab is the `Body`. Element methods in `DocumentTab` delegate to the `Body`.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const body = documentTab.getBody();
console.log(body.getText());
```

### getBookmark(id)

Returns: Bookmark|null

Gets the `Bookmark` with the given ID. This method returns `null` if no such `Bookmark` exists within this tab.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const bookmark = documentTab.getBookmark('id.xyz654321');
if (bookmark) {
  console.log(bookmark.getPosition().getOffset());
} else {
  console.log('No bookmark exists with the given ID.');
}
```

### getBookmarks()

Returns: Bookmark[]

Gets all `Bookmark` objects in the tab.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const bookmarks = documentTab.getBookmarks();
console.log(bookmarks.length);
```

### getFooter()

Returns: FooterSection|null

Retrieves the tab's footer section, if one exists.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
console.log(documentTab.getFooter().getText());
```

### getFootnotes()

Returns: Footnote[]|null

Retrieves all the `Footnote` elements in the tab's body. Calls to `getFootnotes` cause an iteration over the tab's elements. For large tabs, avoid unnecessary calls to this method.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
const footnote = documentTab.getFootnotes()[0];
console.log(footnote.getFootnoteContents().getText());
```

### getHeader()

Returns: HeaderSection|null

Retrieves the tab's header section, if one exists.

```javascript
const documentTab = DocumentApp.openById('123abc').getTab('123abc').asDocumentTab();
console.log(documentTab.getHeader().getText());
```

### getNamedRangeById(id)

Returns: NamedRange|null

Gets the `NamedRange` with the given ID. This method returns `null` if no such `NamedRange` exists in the tab. Names are not necessarily unique, even across tabs; several different ranges in the same document may share the same name, much like a class in HTML. By contrast, IDs are unique within the tab, like an ID in HTML.

### getNamedRanges()

Returns: NamedRange[]

Gets all `NamedRange` objects in the tab. A `NamedRange` can be accessed by any script that accesses the tab. To avoid unintended conflicts between scripts, consider prefixing range names with a unique string.

### getNamedRanges(name)

Returns: NamedRange[]

Gets all `NamedRange` objects in the tab with the given name. Names are not necessarily unique, even across tabs; several different ranges in the same document may share the same name, much like a class in HTML. By contrast, IDs are unique within the tab, like an ID in HTML. A `NamedRange` can be accessed by any script that accesses the tab. To avoid unintended conflicts between scripts, consider prefixing range names with a unique string.

### newPosition(element, offset)

Returns: Position

Creates a new `Position`, which is a reference to a location in the tab, relative to a specific element. The user's cursor is represented as a `Position`, among other uses.

```javascript
const doc = DocumentApp.openById('123abc');
const documentTab = doc.getTab('123abc').asDocumentTab();
const paragraph = documentTab.getBody().appendParagraph('My new paragraph.');
const position = documentTab.newPosition(paragraph.getChild(0), 2);
doc.setCursor(position);
```

### newRange()

Returns: RangeBuilder

Creates a builder used to construct `Range` objects from tab elements.

```javascript
const doc = DocumentApp.openById('123abc');
const documentTab = doc.getTab('123abc').asDocumentTab();
const rangeBuilder = documentTab.newRange();
const tables = documentTab.getBody().getTables();
for (let i = 0; i < tables.length; i++) {
  rangeBuilder.addElement(tables[i]);
}
doc.setSelection(rangeBuilder.build());
```
