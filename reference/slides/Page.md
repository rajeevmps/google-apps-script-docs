# Page

A page in a presentation.

"A page in a presentation."

## Methods

### asLayout()

`Layout`

Returns the page as a layout.

**Returns**

`Layout` — this page as a layout.

### asMaster()

`Master`

Returns the page as a master.

**Returns**

`Master` — this page as a master.

### asSlide()

`Slide`

Returns the page as a slide.

**Returns**

`Slide` — this page as a slide.

### getBackground()

`PageBackground`

Gets the page's background.

**Returns**

`PageBackground` — the page's background.

### getColorScheme()

`ColorScheme`

Gets the ColorScheme associated with the page.

**Returns**

`ColorScheme` — the color scheme associated with the page.

### getGroups()

`Group[]`

Returns the list of Group objects on the page.

**Returns**

`Group[]` — the groups on the page.

### getImages()

`Image[]`

Returns the list of Image objects on the page.

**Returns**

`Image[]` — the images on the page.

### getLines()

`Line[]`

Returns the list of Line objects on the page.

**Returns**

`Line[]` — the lines on the page.

### getObjectId()

`String`

Gets the unique ID for the page. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for the page.

### getPageElementById(id)

`PageElement|null`

Returns the PageElement on the page with the given ID, or null if none exists.

**Parameters**

- `id` (`String`) — the ID of the page element that is being retrieved.

**Returns**

`PageElement|null` — the page element with the given ID, or null.

### getPageElements()

`PageElement[]`

Returns the list of PageElement objects rendered on the page.

**Returns**

`PageElement[]` — the page elements on the page.

### getPageType()

`PageType`

Gets the type of the page.

**Returns**

`PageType` — the type of the page.

### getPlaceholder(placeholderType)

`PageElement|null`

Returns the placeholder PageElement object for a specified PlaceholderType or null if a matching placeholder is not present.

**Parameters**

- `placeholderType` (`PlaceholderType`) — the placeholder type to match.

**Returns**

`PageElement|null` — the matching placeholder, or null.

### getPlaceholder(placeholderType, placeholderIndex)

`PageElement|null`

Returns the placeholder PageElement object for a specified PlaceholderType and placeholder index, or null if not present.

**Parameters**

- `placeholderType` (`PlaceholderType`) — the placeholder type to match.
- `placeholderIndex` (`Integer`) — the placeholder index to match.

**Returns**

`PageElement|null` — the matching placeholder, or null.

### getPlaceholders()

`PageElement[]`

Returns the list of placeholder PageElement objects in the page.

**Returns**

`PageElement[]` — the placeholder page elements in the page.

### getShapes()

`Shape[]`

Returns the list of Shape objects on the page.

**Returns**

`Shape[]` — the shapes on the page.

### getSheetsCharts()

`SheetsChart[]`

Returns the list of SheetsChart objects on the page.

**Returns**

`SheetsChart[]` — the Sheets charts on the page.

### getTables()

`Table[]`

Returns the list of Table objects on the page.

**Returns**

`Table[]` — the tables on the page.

### getVideos()

`Video[]`

Returns the list of Video objects on the page.

**Returns**

`Video[]` — the videos on the page.

### getWordArts()

`WordArt[]`

Returns the list of WordArt objects on the page.

**Returns**

`WordArt[]` — the word arts on the page.

### group(pageElements)

`Group`

Groups all the specified page elements.

**Parameters**

- `pageElements` (`PageElement[]`) — the elements to group together.

**Returns**

`Group` — the new group.

### insertGroup(group)

`Group`

Inserts a copy of the provided Group on the page.

**Parameters**

- `group` (`Group`) — the group to insert.

**Returns**

`Group` — the inserted group.

### insertImage(blobSource)

`Image`

Inserts an image at the top left corner with a default size from the blob.

**Parameters**

- `blobSource` (`BlobSource`) — the image source.

**Returns**

`Image` — the inserted image.

### insertImage(blobSource, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size.

**Parameters**

- `blobSource` (`BlobSource`) — the image source.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — image width.
- `height` (`Number`) — image height.

**Returns**

`Image` — the inserted image.

### insertImage(image)

`Image`

Inserts a copy of the provided Image on the page.

**Parameters**

- `image` (`Image`) — the image to insert.

**Returns**

`Image` — the inserted image.

### insertImage(imageUrl)

`Image`

Inserts an image at the top left corner with a default size from URL.

**Parameters**

- `imageUrl` (`String`) — the image URL.

**Returns**

`Image` — the inserted image.

### insertImage(imageUrl, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from URL.

**Parameters**

- `imageUrl` (`String`) — the image URL.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — image width.
- `height` (`Number`) — image height.

**Returns**

`Image` — the inserted image.

### insertLine(line)

`Line`

Inserts a copy of the provided Line on the page.

**Parameters**

- `line` (`Line`) — the line to insert.

**Returns**

`Line` — the inserted line.

### insertLine(lineCategory, startConnectionSite, endConnectionSite)

`Line`

Inserts a line on the page connecting two connection sites.

**Parameters**

- `lineCategory` (`LineCategory`) — line type.
- `startConnectionSite` (`ConnectionSite`) — starting connection point.
- `endConnectionSite` (`ConnectionSite`) — ending connection point.

**Returns**

`Line` — the inserted line.

### insertLine(lineCategory, startLeft, startTop, endLeft, endTop)

`Line`

Inserts a line on the page.

**Parameters**

- `lineCategory` (`LineCategory`) — line type.
- `startLeft` (`Number`) — starting horizontal position.
- `startTop` (`Number`) — starting vertical position.
- `endLeft` (`Number`) — ending horizontal position.
- `endTop` (`Number`) — ending vertical position.

**Returns**

`Line` — the inserted line.

### insertPageElement(pageElement)

`PageElement`

Inserts a copy of the provided PageElement on the page.

**Parameters**

- `pageElement` (`PageElement`) — the element to insert.

**Returns**

`PageElement` — the inserted page element.

### insertShape(shape)

`Shape`

Inserts a copy of the provided Shape on the page.

**Parameters**

- `shape` (`Shape`) — the shape to insert.

**Returns**

`Shape` — the inserted shape.

### insertShape(shapeType)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`) — the shape type.

**Returns**

`Shape` — the inserted shape.

### insertShape(shapeType, left, top, width, height)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`) — the shape type.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — shape width.
- `height` (`Number`) — shape height.

**Returns**

`Shape` — the inserted shape.

### insertSheetsChart(sourceChart)

`SheetsChart`

Inserts a Google Sheets chart on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — the source chart from Sheets.

**Returns**

`SheetsChart` — the inserted chart.

### insertSheetsChart(sourceChart, left, top, width, height)

`SheetsChart`

Inserts a Google Sheets chart with the provided position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — the source chart from Sheets.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — chart width.
- `height` (`Number`) — chart height.

**Returns**

`SheetsChart` — the inserted chart.

### insertSheetsChart(sheetsChart)

`SheetsChart`

Inserts a copy of the provided SheetsChart on the page.

**Parameters**

- `sheetsChart` (`SheetsChart`) — the chart to insert.

**Returns**

`SheetsChart` — the inserted chart.

### insertSheetsChartAsImage(sourceChart)

`Image`

Inserts a Google Sheets chart as an Image on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — the source chart from Sheets.

**Returns**

`Image` — the inserted image.

### insertSheetsChartAsImage(sourceChart, left, top, width, height)

`Image`

Inserts a Google Sheets chart as an Image with position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — the source chart from Sheets.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — image width.
- `height` (`Number`) — image height.

**Returns**

`Image` — the inserted image.

### insertTable(numRows, numColumns)

`Table`

Inserts a table on the page.

**Parameters**

- `numRows` (`Integer`) — number of rows.
- `numColumns` (`Integer`) — number of columns.

**Returns**

`Table` — the inserted table.

### insertTable(numRows, numColumns, left, top, width, height)

`Table`

Inserts a table on the page with provided position and size.

**Parameters**

- `numRows` (`Integer`) — number of rows.
- `numColumns` (`Integer`) — number of columns.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — table width.
- `height` (`Number`) — table height.

**Returns**

`Table` — the inserted table.

### insertTable(table)

`Table`

Inserts a copy of the provided Table on the page.

**Parameters**

- `table` (`Table`) — the table to insert.

**Returns**

`Table` — the inserted table.

### insertTextBox(text)

`Shape`

Inserts a text box Shape containing the provided string on the page.

**Parameters**

- `text` (`String`) — the text content.

**Returns**

`Shape` — the inserted text box shape.

### insertTextBox(text, left, top, width, height)

`Shape`

Inserts a text box Shape containing the provided string on the page.

**Parameters**

- `text` (`String`) — the text content.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — box width.
- `height` (`Number`) — box height.

**Returns**

`Shape` — the inserted text box shape.

### insertVideo(videoUrl)

`Video`

Inserts a video at the top left corner with a default size.

**Parameters**

- `videoUrl` (`String`) — the video URL.

**Returns**

`Video` — the inserted video.

### insertVideo(videoUrl, left, top, width, height)

`Video`

Inserts a video on the page with the provided position and size.

**Parameters**

- `videoUrl` (`String`) — the video URL.
- `left` (`Number`) — horizontal position.
- `top` (`Number`) — vertical position.
- `width` (`Number`) — video width.
- `height` (`Number`) — video height.

**Returns**

`Video` — the inserted video.

### insertVideo(video)

`Video`

Inserts a copy of the provided Video on the page.

**Parameters**

- `video` (`Video`) — the video to insert.

**Returns**

`Video` — the inserted video.

### insertWordArt(wordArt)

`WordArt`

Inserts a copy of the provided WordArt on the page.

**Parameters**

- `wordArt` (`WordArt`) — the WordArt to insert.

**Returns**

`WordArt` — the inserted word art.

### remove()

`void`

Removes the page.

**Returns**

`void`

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — text to find.
- `replaceText` (`String`) — replacement text.

**Returns**

`Integer` — the number of occurrences changed.

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — text to find.
- `replaceText` (`String`) — replacement text.
- `matchCase` (`Boolean`) — whether to match case.

**Returns**

`Integer` — the number of occurrences changed.

### selectAsCurrentPage()

`void`

Selects the Page in the active presentation as the current page selection.

**Returns**

`void`

**Authorization**

All methods require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
