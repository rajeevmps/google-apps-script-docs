# Master

A master in a presentation containing common page elements and properties for a set of layouts.

A master in a presentation contains all common page elements and properties for a set of layouts. Masters serve three key purposes:

1. Placeholder shapes on a master contain the default text styles and shape properties of all placeholder shapes on pages that use that master.
2. The properties of a master page define the common page properties inherited by its layouts.
3. Any other shapes on the master slide appear on all slides using that master, regardless of their layout.

## Methods

### getBackground()

`PageBackground`

Gets the page's background.

**Returns**

`PageBackground` — the page's background.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getColorScheme()

`ColorScheme`

Gets the `ColorScheme` associated with the page.

**Returns**

`ColorScheme` — the color scheme associated with the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getGroups()

`Group[]`

Returns the list of `Group` objects on the page.

**Returns**

`Group[]` — the groups on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getImages()

`Image[]`

Returns the list of `Image` objects on the page.

**Returns**

`Image[]` — the images on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getLayouts()

`Layout[]`

Gets this master's layouts.

**Returns**

`Layout[]` — the layouts belonging to this master.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getLines()

`Line[]`

Returns the list of `Line` objects on the page.

**Returns**

`Line[]` — the lines on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getObjectId()

`String`

Gets the unique ID for the page. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String` — the unique ID for the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPageElementById(id)

`PageElement|null`

Returns the `PageElement` on the page with the given ID, or `null` if none exists.

**Parameters**

- `id` (`String`) — The ID of the page element that is being retrieved.

**Returns**

`PageElement|null` — the page element with the given ID, or null.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPageElements()

`PageElement[]`

Returns the list of `PageElement` objects rendered on the page.

**Returns**

`PageElement[]` — the page elements on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPageType()

`PageType`

Gets the type of the page.

**Returns**

`PageType` — the type of the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPlaceholder(placeholderType)

`PageElement|null`

Returns the placeholder `PageElement` object for a specified `PlaceholderType` or `null` if a matching placeholder is not present. If there are multiple placeholders with the same type, it returns the one with minimal placeholder index. If there are multiple matching placeholders with the same index, it returns the first placeholder from the page's page elements collection.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const placeholder = slide.getPlaceholder(
    SlidesApp.PlaceholderType.CENTERED_TITLE,
);
```

**Parameters**

- `placeholderType` (`PlaceholderType`) — The placeholder type to match.

**Returns**

`PageElement|null` — the matching placeholder, or null.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPlaceholder(placeholderType, placeholderIndex)

`PageElement|null`

Returns the placeholder `PageElement` object for a specified `PlaceholderType` and a placeholder index, or `null` if the placeholder is not present. If there are multiple placeholders with the same type and index, it returns the first placeholder from the page's page elements collection.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const placeholder = slide.getPlaceholder(
    SlidesApp.PlaceholderType.CENTERED_TITLE,
    0,
);
```

**Parameters**

- `placeholderType` (`PlaceholderType`) — The placeholder type to match.
- `placeholderIndex` (`Integer`) — The placeholder index to match.

**Returns**

`PageElement|null` — the matching placeholder, or null.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getPlaceholders()

`PageElement[]`

Returns the list of placeholder `PageElement` objects in the page.

```javascript
const master = SlidesApp.getActivePresentation().getMasters()[0];
Logger.log(
    `Number of placeholders in the master: ${master.getPlaceholders().length}`,
);
```

**Returns**

`PageElement[]` — the placeholder page elements in the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getShapes()

`Shape[]`

Returns the list of `Shape` objects on the page.

**Returns**

`Shape[]` — the shapes on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getSheetsCharts()

`SheetsChart[]`

Returns the list of `SheetsChart` objects on the page.

**Returns**

`SheetsChart[]` — the Sheets charts on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getTables()

`Table[]`

Returns the list of `Table` objects on the page.

**Returns**

`Table[]` — the tables on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getVideos()

`Video[]`

Returns the list of `Video` objects on the page.

**Returns**

`Video[]` — the videos on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getWordArts()

`WordArt[]`

Returns the list of `WordArt` objects on the page.

**Returns**

`WordArt[]` — the word arts on the page.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### group(pageElements)

`Group`

Groups all the specified page elements. There should be at least two page elements on the same page that are not already in another group. Some page elements, such as `Videos`, `Tables` and `placeholder Shapes` cannot be grouped.

**Parameters**

- `pageElements` (`PageElement[]`) — The elements to group together.

**Returns**

`Group` — the new group.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertGroup(group)

`Group`

Inserts a copy of the provided `Group` on the page. The inserted element's position on this page is determined from the source element's position on its respective page. If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element. If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a group between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const group = otherPresentationSlide.getGroups()[0];
```

**Parameters**

- `group` (`Group`) — The group to insert.

**Returns**

`Group` — the inserted group.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertImage(blobSource)

`Image`

Inserts an image at the top left corner of the page with a default size from the specified image blob.

**Parameters**

- `blobSource` (`BlobSource`) — The image source.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertImage(blobSource, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the specified image blob.

**Parameters**

- `blobSource` (`BlobSource`) — The image source.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Image width.
- `height` (`Number`) — Image height.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertImage(image)

`Image`

Inserts a copy of the provided `Image` on the page.

**Parameters**

- `image` (`Image`) — The image to insert.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertImage(imageUrl)

`Image`

Inserts an image at the top left corner of the page with a default size from the provided URL.

**Parameters**

- `imageUrl` (`String`) — The image URL.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertImage(imageUrl, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the provided URL.

**Parameters**

- `imageUrl` (`String`) — The image URL.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Image width.
- `height` (`Number`) — Image height.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertLine(line)

`Line`

Inserts a copy of the provided `Line` on the page.

**Parameters**

- `line` (`Line`) — The line to insert.

**Returns**

`Line` — the inserted line.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertLine(lineCategory, startConnectionSite, endConnectionSite)

`Line`

Inserts a line on the page connecting two connection sites.

**Parameters**

- `lineCategory` (`LineCategory`) — Line type.
- `startConnectionSite` (`ConnectionSite`) — Starting connection point.
- `endConnectionSite` (`ConnectionSite`) — Ending connection point.

**Returns**

`Line` — the inserted line.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertLine(lineCategory, startLeft, startTop, endLeft, endTop)

`Line`

Inserts a line on the page.

**Parameters**

- `lineCategory` (`LineCategory`) — Line type.
- `startLeft` (`Number`) — Starting horizontal position.
- `startTop` (`Number`) — Starting vertical position.
- `endLeft` (`Number`) — Ending horizontal position.
- `endTop` (`Number`) — Ending vertical position.

**Returns**

`Line` — the inserted line.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertPageElement(pageElement)

`PageElement`

Inserts a copy of the provided `PageElement` on the page.

**Parameters**

- `pageElement` (`PageElement`) — The element to insert.

**Returns**

`PageElement` — the inserted page element.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertShape(shape)

`Shape`

Inserts a copy of the provided `Shape` on the page.

**Parameters**

- `shape` (`Shape`) — The shape to insert.

**Returns**

`Shape` — the inserted shape.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertShape(shapeType)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`) — The shape type.

**Returns**

`Shape` — the inserted shape.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertShape(shapeType, left, top, width, height)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`) — The shape type.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Shape width.
- `height` (`Number`) — Shape height.

**Returns**

`Shape` — the inserted shape.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sourceChart)

`SheetsChart`

Inserts a Google Sheets chart on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The source chart from Sheets.

**Returns**

`SheetsChart` — the inserted chart.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sourceChart, left, top, width, height)

`SheetsChart`

Inserts a Google Sheets chart on the page with the provided position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The source chart from Sheets.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Chart width.
- `height` (`Number`) — Chart height.

**Returns**

`SheetsChart` — the inserted chart.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sheetsChart)

`SheetsChart`

Inserts a copy of the provided `SheetsChart` on the page.

**Parameters**

- `sheetsChart` (`SheetsChart`) — The chart to insert.

**Returns**

`SheetsChart` — the inserted chart.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertSheetsChartAsImage(sourceChart)

`Image`

Inserts a Google Sheets chart as an `Image` on the page.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The source chart from Sheets.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertSheetsChartAsImage(sourceChart, left, top, width, height)

`Image`

Inserts a Google Sheets chart as an `Image` on the page with the provided position and size.

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The source chart from Sheets.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Image width.
- `height` (`Number`) — Image height.

**Returns**

`Image` — the inserted image.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertTable(numRows, numColumns)

`Table`

Inserts a table on the page.

**Parameters**

- `numRows` (`Integer`) — Number of rows.
- `numColumns` (`Integer`) — Number of columns.

**Returns**

`Table` — the inserted table.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertTable(numRows, numColumns, left, top, width, height)

`Table`

Inserts a table on the page with the provided position and size.

**Parameters**

- `numRows` (`Integer`) — Number of rows.
- `numColumns` (`Integer`) — Number of columns.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Table width.
- `height` (`Number`) — Table height.

**Returns**

`Table` — the inserted table.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertTable(table)

`Table`

Inserts a copy of the provided `Table` on the page.

**Parameters**

- `table` (`Table`) — The table to insert.

**Returns**

`Table` — the inserted table.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertTextBox(text)

`Shape`

Inserts a text box `Shape` containing the provided string on the page.

**Parameters**

- `text` (`String`) — The text content.

**Returns**

`Shape` — the inserted text box shape.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertTextBox(text, left, top, width, height)

`Shape`

Inserts a text box `Shape` containing the provided string on the page.

**Parameters**

- `text` (`String`) — The text content.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Box width.
- `height` (`Number`) — Box height.

**Returns**

`Shape` — the inserted text box shape.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertVideo(videoUrl)

`Video`

Inserts a video at the top left corner of the page with a default size.

**Parameters**

- `videoUrl` (`String`) — The video URL.

**Returns**

`Video` — the inserted video.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertVideo(videoUrl, left, top, width, height)

`Video`

Inserts a video on the page with the provided position and size.

**Parameters**

- `videoUrl` (`String`) — The video URL.
- `left` (`Number`) — Horizontal position.
- `top` (`Number`) — Vertical position.
- `width` (`Number`) — Video width.
- `height` (`Number`) — Video height.

**Returns**

`Video` — the inserted video.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertVideo(video)

`Video`

Inserts a copy of the provided `Video` on the page.

**Parameters**

- `video` (`Video`) — The video to insert.

**Returns**

`Video` — the inserted video.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### insertWordArt(wordArt)

`WordArt`

Inserts a copy of the provided `WordArt` on the page.

**Parameters**

- `wordArt` (`WordArt`) — The WordArt to insert.

**Returns**

`WordArt` — the inserted word art.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### remove()

`void`

Removes the page.

**Returns**

`void`

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — Text to find.
- `replaceText` (`String`) — Replacement text.

**Returns**

`Integer` — the number of occurrences changed.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — Text to find.
- `replaceText` (`String`) — Replacement text.
- `matchCase` (`Boolean`) — Whether to match case.

**Returns**

`Integer` — the number of occurrences changed.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### selectAsCurrentPage()

`void`

Selects the `Page` in the active presentation as the current page selection and removes any previous selection.

**Returns**

`void`

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

## Properties

None.
