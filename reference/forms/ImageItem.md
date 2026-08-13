# ImageItem

A layout item that displays an image.

A layout item that displays an image. Items can be accessed or created from a `Form`.

## Methods

### duplicate()
`duplicate(): ImageItem`

Creates a copy of this item and appends it to the end of the form.

### getAlignment()
`getAlignment(): Alignment`

Gets the image's horizontal alignment.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getImage()
`getImage(): Blob`

Gets the image that is currently assigned to the item.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### getWidth()
`getWidth(): Integer`

Gets the image's width in pixels.

### setAlignment(alignment)
`setAlignment(alignment: Alignment): ImageItem`

Sets the image's horizontal alignment.

### setHelpText(text)
`setHelpText(text: String): ImageItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setImage(image)
`setImage(image: BlobSource): ImageItem`

Sets the image itself.

### setTitle(title)
`setTitle(title: String): ImageItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### setWidth(width)
`setWidth(width: Integer): ImageItem`

Sets the image's width in pixels. Only the image's width can be set. Height is set automatically to maintain the image's proportions.
