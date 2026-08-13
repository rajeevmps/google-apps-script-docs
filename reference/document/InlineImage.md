# InlineImage

An element representing an embedded image.

An element representing an embedded image. An `InlineImage` can be contained within a `ListItem` or `Paragraph`, unless the `ListItem` or `Paragraph` is within a `FootnoteSection`. An `InlineImage` cannot itself contain any other element.

## Methods

### copy()

Returns: InlineImage

Returns a detached, deep copy of the current element. Any child elements present in the element are also copied. The new element doesn't have a parent.

Requires authorization with one of the following scopes: `https://www.googleapis.com/auth/documents.currentonly` or `https://www.googleapis.com/auth/documents`.

### getAltDescription()

Returns: String|null

Returns the image's alternate description. Returns the alternate description, or `null` if the element does not have an alternate description.

### getAltTitle()

Returns: String|null

Returns the image's alternate title. Returns the alternate title, or `null` if the element does not have an alternate title.

### getAs(contentType String)

Returns: Blob

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes "ShoppingList.12.25.pdf".

Parameters:
- `contentType` (String) - The MIME type to convert to. For most blobs, `'application/pdf'` is the only valid option. For images in BMP, GIF, JPEG, or PNG format, any of `'image/bmp'`, `'image/gif'`, `'image/jpeg'`, or `'image/png'` are also valid.

### getAttributes()

Returns: Object

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

### getBlob()

Returns: Blob

Return the data inside this object as a blob.

### getHeight()

Returns: Integer

Retrieves the image's height, in pixels. Returns the image's height, in pixels.

### getLinkUrl()

Returns: String|null

Retrieves the link URL. Returns the link URL, or `null` if the element contains multiple values for this attribute.

### getNextSibling()

Returns: Element|null

Retrieves the element's next sibling element. The next sibling has the same parent and follows the current element.

### getParent()

Returns: ContainerElement|null

Retrieves the element's parent element. The parent element contains the current element.

### getPreviousSibling()

Returns: Element|null

Retrieves the element's previous sibling element. The previous sibling has the same parent and precedes the current element.

### getType()

Returns: ElementType

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

### getWidth()

Returns: Integer

Retrieves the image's width, in pixels. Returns the image's width, in pixels.

### isAtDocumentEnd()

Returns: Boolean

Determines whether the element is at the end of the `Document`. Returns whether the element is at the end of the tab.

### merge()

Returns: InlineImage|null

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

Returns: InlineImage|null

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

### setAltDescription(description String)

Returns: InlineImage

Sets the image's alternate description. If the given description is `null`, sets the description to the empty string.

Parameters:
- `description` (String) - The alternate description.

### setAltTitle(title String)

Returns: InlineImage

Sets the image's alternate title. If the given title is `null`, sets the title to the empty string.

Parameters:
- `title` (String) - The alternate title.

### setAttributes(attributes Object)

Returns: InlineImage

Sets the element's attributes. The specified attributes parameter must be an object where each property name is an item in the `DocumentApp.Attribute` enumeration and each property value is the new value to be applied.

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

### setHeight(height Integer)

Returns: InlineImage

Sets the image's height, in pixels.

Parameters:
- `height` (Integer) - the image's height, in pixels

Returns: the current object

### setLinkUrl(url String)

Returns: InlineImage

Sets the link URL. When the given URL is `null` or an empty string, this method creates a link with an empty URL that may display as "Invalid link" in Google Docs.

Parameters:
- `url` (String) - The link URL.

### setWidth(width Integer)

Returns: InlineImage

Sets the image's width, in pixels.

Parameters:
- `width` (Integer) - the image's width, in pixels

Returns: the current object
