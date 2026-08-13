# PositionedImage

Fixed position image anchored to a Paragraph.

Unlike an InlineImage, a PositionedImage is not an Element. It does not have a parent or sibling Element. Instead, it is anchored to a Paragraph or ListItem, and is placed via offsets from that anchor. A PositionedImage has an ID that can be used to reference it.

## Example

```javascript
const body = DocumentApp.getActiveDocument().getActiveTab().asDocumentTab().getBody();
const paragraph = body.appendParagraph('New paragraph to anchor the image to.');
const image = DriveApp.getFileById('ENTER_IMAGE_FILE_ID_HERE').getBlob();
const posImage = paragraph.addPositionedImage(image).setTopOffset(60).setLeftOffset(40);
```

## Methods

### getAs(contentType String)

Returns: Blob

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes "ShoppingList.12.25.pdf".

### getBlob()

Returns: Blob

Return the data inside this object as a blob.

### getHeight()

Returns: Integer

Retrieves the image's height, in pixels.

### getId()

Returns: String

Gets the image's ID.

### getLayout()

Returns: PositionedLayout

Gets an enum value that represents how the image is laid out.

### getLeftOffset()

Returns: Number

Gets the image's offset, in points, from the paragraph's left.

### getParagraph()

Returns: Paragraph

Gets the Paragraph the image is anchored to.

### getTopOffset()

Returns: Number

Gets the image's offset, in points, from the paragraph's top.

### getWidth()

Returns: Integer

Retrieves the image's width, in pixels.

### setHeight(height Integer)

Returns: PositionedImage

Sets the image's height, in pixels.

### setLayout(layout PositionedLayout)

Returns: PositionedImage

Sets the definition of how the image is laid out.

### setLeftOffset(offset Number)

Returns: PositionedImage

Sets the image's offset, in points, from the paragraph's left.

### setTopOffset(offset Number)

Returns: PositionedImage

Sets the image's offset, in points, from the paragraph's top.

### setWidth(width Integer)

Returns: PositionedImage

Sets the image's width, in pixels.
