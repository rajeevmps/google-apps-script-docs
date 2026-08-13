# Layout

A layout in a presentation.

A layout in a presentation. Each layout serves as a template for slides that inherit from it, determining how content on those slides is arranged and styled.

## Methods

### getBackground()

`PageBackground`

Gets the page's background.

**Returns**

`PageBackground` — this page's background

### getColorScheme()

`ColorScheme`

Gets the ColorScheme associated with the page.

**Returns**

`ColorScheme` — the color scheme of this page

### getGroups()

`Group[]`

Returns the list of Group objects on the page.

**Returns**

`Group[]` — the groups on this page

### getImages()

`Image[]`

Returns the list of Image objects on the page.

**Returns**

`Image[]` — the images on this page

### getLayoutName()

`String`

Gets the name of the layout.

**Returns**

`String` — the layout's name

### getLines()

`Line[]`

Returns the list of Line objects on the page.

**Returns**

`Line[]` — the lines on this page

### getMaster()

`Master`

Gets the master that the layout is based on.

**Returns**

`Master` — the master of this layout

### getObjectId()

`String`

Gets the unique ID for the page. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for this page

### getPageElementById(id)

`PageElement`

Returns the PageElement on the page with the given ID, or null if none exists.

**Parameters**

- `id` (`String`) — The ID of the page element that is being retrieved.

**Returns**

`PageElement` — the page element with the given ID, or `null`

### getPageElements()

`PageElement[]`

Returns the list of PageElement objects rendered on the page.

**Returns**

`PageElement[]` — the page elements on this page

### getPageType()

`PageType`

Gets the type of the page.

**Returns**

`PageType` — this page's type

### getPlaceholder(placeholderType)

`PageElement`

Returns the placeholder PageElement object for a specified PlaceholderType or null if matching placeholder is not present.

**Parameters**

- `placeholderType` (`PlaceholderType`) — The placeholder type to match.

**Returns**

`PageElement` — the placeholder, or `null`

### getPlaceholder(placeholderType, placeholderIndex)

`PageElement`

Returns the placeholder PageElement object for specified PlaceholderType and placeholder index, or null if not present.

**Parameters**

- `placeholderType` (`PlaceholderType`) — The placeholder type to match.
- `placeholderIndex` (`Integer`) — The placeholder index to match.

**Returns**

`PageElement` — the placeholder, or `null`

### getPlaceholders()

`PageElement[]`

Returns the list of placeholder PageElement objects in the page.

**Returns**

`PageElement[]` — the placeholders on this page

### getShapes()

`Shape[]`

Returns the list of Shape objects on the page.

**Returns**

`Shape[]` — the shapes on this page

### getSheetsCharts()

`SheetsChart[]`

Returns the list of SheetsChart objects on the page.

**Returns**

`SheetsChart[]` — the Sheets charts on this page

### getTables()

`Table[]`

Returns the list of Table objects on the page.

**Returns**

`Table[]` — the tables on this page

### getVideos()

`Video[]`

Returns the list of Video objects on the page.

**Returns**

`Video[]` — the videos on this page

### getWordArts()

`WordArt[]`

Returns the list of WordArt objects on the page.

**Returns**

`WordArt[]` — the word arts on this page

### group(pageElements)

`Group`

Groups all the specified page elements. There should be at least two page elements on the same page that are not already in another group.

**Parameters**

- `pageElements` (`PageElement[]`) — The elements to group together.

**Returns**

`Group` — the new group

### insertGroup(group)

`Group`

Inserts a copy of the provided Group on the page. The inserted element's position on this page is determined from the source element's position on its respective page.

**Parameters**

- `group` (`Group`)

**Returns**

`Group` — the inserted group

### insertImage(blobSource)

`Image`

Inserts an image at the top left corner of the page with a default size from the specified image blob.

**Parameters**

- `blobSource` (`BlobSource`)

**Returns**

`Image` — the inserted image

### insertImage(blobSource, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the specified image blob.

**Parameters**

- `blobSource` (`BlobSource`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Image` — the inserted image

### insertImage(image)

`Image`

Inserts a copy of the provided Image on the page.

**Parameters**

- `image` (`Image`)

**Returns**

`Image` — the inserted image

### insertImage(imageUrl)

`Image`

Inserts an image at the top left corner of the page with a default size from the provided URL.

**Parameters**

- `imageUrl` (`String`)

**Returns**

`Image` — the inserted image

### insertImage(imageUrl, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the provided URL.

**Parameters**

- `imageUrl` (`String`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Image` — the inserted image

### insertLine(line)

`Line`

Inserts a copy of the provided Line on the page.

**Parameters**

- `line` (`Line`)

**Returns**

`Line` — the inserted line

### insertLine(lineCategory, startConnectionSite, endConnectionSite)

`Line`

Inserts a line on the page connecting two connection sites.

**Parameters**

- `lineCategory` (`LineCategory`)
- `startConnectionSite` (`ConnectionSite`)
- `endConnectionSite` (`ConnectionSite`)

**Returns**

`Line` — the inserted line

### insertLine(lineCategory, startLeft, startTop, endLeft, endTop)

`Line`

Inserts a line on the page.

**Parameters**

- `lineCategory` (`LineCategory`)
- `startLeft` (`Number`)
- `startTop` (`Number`)
- `endLeft` (`Number`)
- `endTop` (`Number`)

**Returns**

`Line` — the inserted line

### insertPageElement(pageElement)

`PageElement`

Inserts a copy of the provided PageElement on the page.

**Parameters**

- `pageElement` (`PageElement`)

**Returns**

`PageElement` — the inserted page element

### insertShape(shape)

`Shape`

Inserts a copy of the provided Shape on the page.

**Parameters**

- `shape` (`Shape`)

**Returns**

`Shape` — the inserted shape

### insertShape(shapeType)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`)

**Returns**

`Shape` — the inserted shape

### insertShape(shapeType, left, top, width, height)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Shape` — the inserted shape

### insertSheetsChart(sourceChart)

`SheetsChart`

Inserts a Google Sheets chart on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`)

**Returns**

`SheetsChart` — the inserted chart

### insertSheetsChart(sourceChart, left, top, width, height)

`SheetsChart`

Inserts a Google Sheets chart on the page with the provided position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`SheetsChart` — the inserted chart

### insertSheetsChart(sheetsChart)

`SheetsChart`

Inserts a copy of the provided SheetsChart on the page.

**Parameters**

- `sheetsChart` (`SheetsChart`)

**Returns**

`SheetsChart` — the inserted chart

### insertSheetsChartAsImage(sourceChart)

`Image`

Inserts a Google Sheets chart as an Image on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`)

**Returns**

`Image` — the inserted chart as an image

### insertSheetsChartAsImage(sourceChart, left, top, width, height)

`Image`

Inserts a Google Sheets chart as an Image on the page with the provided position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Image` — the inserted chart as an image

### insertTable(numRows, numColumns)

`Table`

Inserts a table on the page.

**Parameters**

- `numRows` (`Integer`)
- `numColumns` (`Integer`)

**Returns**

`Table` — the inserted table

### insertTable(numRows, numColumns, left, top, width, height)

`Table`

Inserts a table on the page with the provided position and size.

**Parameters**

- `numRows` (`Integer`)
- `numColumns` (`Integer`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Table` — the inserted table

### insertTable(table)

`Table`

Inserts a copy of the provided Table on the page.

**Parameters**

- `table` (`Table`)

**Returns**

`Table` — the inserted table

### insertTextBox(text)

`Shape`

Inserts a text box Shape containing the provided string on the page.

**Parameters**

- `text` (`String`)

**Returns**

`Shape` — the inserted text box shape

### insertTextBox(text, left, top, width, height)

`Shape`

Inserts a text box Shape containing the provided string on the page.

**Parameters**

- `text` (`String`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Shape` — the inserted text box shape

### insertVideo(videoUrl)

`Video`

Inserts a video at the top left corner of the page with a default size.

**Parameters**

- `videoUrl` (`String`)

**Returns**

`Video` — the inserted video

### insertVideo(videoUrl, left, top, width, height)

`Video`

Inserts a video on the page with the provided position and size.

**Parameters**

- `videoUrl` (`String`)
- `left` (`Number`)
- `top` (`Number`)
- `width` (`Number`)
- `height` (`Number`)

**Returns**

`Video` — the inserted video

### insertVideo(video)

`Video`

Inserts a copy of the provided Video on the page.

**Parameters**

- `video` (`Video`)

**Returns**

`Video` — the inserted video

### insertWordArt(wordArt)

`WordArt`

Inserts a copy of the provided WordArt on the page.

**Parameters**

- `wordArt` (`WordArt`)

**Returns**

`WordArt` — the inserted word art

### remove()

`void`

Removes the page.

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`)
- `replaceText` (`String`)

**Returns**

`Integer` — the number of occurrences replaced

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`)
- `replaceText` (`String`)
- `matchCase` (`Boolean`)

**Returns**

`Integer` — the number of occurrences replaced

### selectAsCurrentPage()

`void`

Selects the Page in the active presentation as the current page selection and removes any previous selection.

All methods require authorization with `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations` scopes.
