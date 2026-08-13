# Slide

A slide in a presentation.

A slide in a presentation.

These pages contain the content you are presenting to your audience. Most slides are based on a master and a layout. You can specify which layout to use for each slide when it is created.

## Methods

### duplicate()

`Slide`

Duplicates the slide.

The duplicate slide is created immediately following the original.

**Returns**

`Slide` — The duplicated slide.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getBackground()

`PageBackground`

Gets the page's background.

**Returns**

`PageBackground` — The page's background.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getColorScheme()

`ColorScheme`

Gets the ColorScheme associated with the page.

**Returns**

`ColorScheme` — The page's color scheme.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getGroups()

`Group[]`

Returns the list of Group objects on the page.

**Returns**

`Group[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getImages()

`Image[]`

Returns the list of Image objects on the page.

**Returns**

`Image[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLayout()

`Layout|null`

Gets the layout that the slide is based on or null if the slide is not based on a layout.

**Returns**

`Layout|null`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLines()

`Line[]`

Returns the list of Line objects on the page.

**Returns**

`Line[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNotesPage()

`NotesPage`

Returns the notes page associated with the slide.

**Returns**

`NotesPage`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getObjectId()

`String`

Gets the unique ID for the page. Object IDs used by pages and page elements share the same namespace.

**Returns**

`String`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageElementById(id)

`PageElement|null`

Returns the PageElement on the page with the given ID, or null if none exists.

**Parameters**

- `id` (`String`) — The ID of the page element that is being retrieved.

**Returns**

`PageElement|null` — The page element with the given ID.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageElements()

`PageElement[]`

Returns the list of PageElement objects rendered on the page.

**Returns**

`PageElement[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageType()

`PageType`

Gets the type of the page.

**Returns**

`PageType` — The page type.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPlaceholder(placeholderType)

`PageElement|null`

Returns the placeholder PageElement object for a specified PlaceholderType or null if a matching placeholder is not present.

If there are multiple placeholders with the same type, it returns the one with minimal placeholder index. If there are multiple matching placeholders with the same index, it returns the first placeholder from the page's page elements collection.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const placeholder = slide.getPlaceholder(
    SlidesApp.PlaceholderType.CENTERED_TITLE,
);
```

**Parameters**

- `placeholderType` (`PlaceholderType`) — The placeholder type to match.

**Returns**

`PageElement|null` — The placeholder page element, or null if none is found.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPlaceholder(placeholderType, placeholderIndex)

`PageElement|null`

Returns the placeholder PageElement object for a specified PlaceholderType and a placeholder index, or null if the placeholder is not present.

If there are multiple placeholders with the same type and index, it returns the first placeholder from the page's page elements collection.

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

`PageElement|null` — The placeholder page element, or null if none is found.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPlaceholders()

`PageElement[]`

Returns the list of placeholder PageElement objects in the page.

```javascript
const master = SlidesApp.getActivePresentation().getMasters()[0];
Logger.log(
    `Number of placeholders in the master: ${master.getPlaceholders().length}`,
);
```

**Returns**

`PageElement[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getShapes()

`Shape[]`

Returns the list of Shape objects on the page.

**Returns**

`Shape[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSheetsCharts()

`SheetsChart[]`

Returns the list of SheetsChart objects on the page.

**Returns**

`SheetsChart[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlideLinkingMode()

`SlideLinkingMode`

Returns a SlideLinkingMode indicating if the slide is linked to another slide.

**Returns**

`SlideLinkingMode` — The slide linking mode.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSourcePresentationId()

`String`

Returns the source Presentation ID or null if the slide is not linked.

A slide only has a source Presentation ID when it is linked to a slide within another presentation.

**Returns**

`String` — The source presentation ID or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSourceSlideObjectId()

`String`

Returns the source slide ID or null if the slide is not linked.

A slide only has a source slide ID when it is linked to a slide within another presentation.

**Returns**

`String` — The source slide ID or null.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getTables()

`Table[]`

Returns the list of Table objects on the page.

**Returns**

`Table[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getVideos()

`Video[]`

Returns the list of Video objects on the page.

**Returns**

`Video[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getWordArts()

`WordArt[]`

Returns the list of WordArt objects on the page.

**Returns**

`WordArt[]`

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### group(pageElements)

`Group`

Groups all the specified page elements.

There should be at least two page elements on the same page that are not already in another group. Some page elements, such as Videos, Tables and placeholder Shapes cannot be grouped.

**Parameters**

- `pageElements` (`PageElement[]`) — The elements to group together.

**Returns**

`Group` — The new group.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertGroup(group)

`Group`

Inserts a copy of the provided Group on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a group between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const group = otherPresentationSlide.getGroups()[0];
currentPresentationSlide.insertGroup(
    group);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `group` (`Group`) — The group to be copied and inserted.

**Returns**

`Group` — The inserted group.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertImage(blobSource)

`Image`

Inserts an image at the top left corner of the page with a default size from the specified image blob.

Inserting the image fetches it from the BlobSource once and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
// Get the Drive image file with the given ID.
const image = DriveApp.getFileById('123abc');
slide.insertImage(image);
```

**Parameters**

- `blobSource` (`BlobSource`) — The image data.

**Returns**

`Image` — The inserted image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertImage(blobSource, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the specified image blob.

The image is fetched from the provided BlobSource once at insertion time and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format.

In order to maintain the image's aspect ratio, the image is scaled and centered with respect to the provided size.

```javascript
const slide = SlidesApp.getActivePresentation().getSlides()[0];
// Get the Drive image file with the given ID.
const image = DriveApp.getFileById('123abc');
const position = {
  left: 0,
  top: 0
};
const size = {
  width: 300,
  height: 100
};
slide.insertImage(image, position.left, position.top, size.width, size.height);
```

**Parameters**

- `blobSource` (`BlobSource`) — The image data.
- `left` (`Number`) — The horizontal position of the image in points, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the image in points, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the image in points.
- `height` (`Number`) — The height of the image in points.

**Returns**

`Image` — The inserted image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertImage(image)

`Image`

Inserts a copy of the provided Image on the page.

The inserted images's position on this page is determined from the source image's position on its respective page.

If the provided image is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted image.

If the provided image is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the image from the source presentation. If the copied placeholder image is empty, nothing is inserted in the destination presentation.

```javascript
// Copy an image between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const image = otherPresentationSlide.getImages[0];
currentPresentationSlide.insertImage(image);
```

**Parameters**

- `image` (`Image`) — The image to be copied and inserted.

**Returns**

`Image` — The inserted image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertImage(imageUrl)

`Image`

Inserts an image at the top left corner of the page with a default size from the provided URL.

Inserting the image fetches it from the URL once and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format.

The provided URL must be publicly accessible and no larger than 2kB. The URL itself is saved with the image and exposed via Image.getSourceUrl().

**Parameters**

- `imageUrl` (`String`) — The image URL.

**Returns**

`Image` — The inserted image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertImage(imageUrl, left, top, width, height)

`Image`

Inserts an image on the page with the provided position and size from the provided URL.

Inserting the image fetches it from the URL once and a copy is stored for display inside the presentation. Images must be less than 50MB in size, cannot exceed 25 megapixels, and must be in either in PNG, JPEG, or GIF format.

The provided URL must be publicly accessible and no larger than 2kB. The URL itself is saved with the image and exposed via Image.getSourceUrl().

In order to maintain the image's aspect ratio, the image is scaled and centered with respect to the provided size.

**Parameters**

- `imageUrl` (`String`) — The image URL.
- `left` (`Number`) — The horizontal position of the image in points, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the image in points, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the image in points.
- `height` (`Number`) — The height of the image in points.

**Returns**

`Image` — The inserted image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertLine(line)

`Line`

Inserts a copy of the provided Line on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a line between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const line = otherPresentationSlide.getLines[0];
currentPresentationSlide.insertLine(line);
```

**Parameters**

- `line` (`Line`) — The line to be copied and inserted.

**Returns**

`Line` — The inserted line.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertLine(lineCategory, startConnectionSite, endConnectionSite)

`Line`

Inserts a line on the page connecting two connection sites. The two connection sites must be on this page.

```javascript
// Insert a line in the first slide of the presentation connecting two shapes.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const shape1 = slide.insertShape(SlidesApp.ShapeType.RECTANGLE);
const shape2 = slide.insertShape(SlidesApp.ShapeType.CLOUD);
slide.insertLine(
    SlidesApp.LineCategory.BENT,
    shape1.getConnectionSites()[0],
    shape2.getConnectionSites()[1],
);
```

**Parameters**

- `lineCategory` (`LineCategory`) — The category of the line to insert.
- `startConnectionSite` (`ConnectionSite`) — The connection site where the start of the line is to be connected.
- `endConnectionSite` (`ConnectionSite`) — The connection site where the end of the line is to be connected.

**Returns**

`Line` — The inserted line.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertLine(lineCategory, startLeft, startTop, endLeft, endTop)

`Line`

Inserts a line on the page.

```javascript
// Insert a line in the first slide of the presentation.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const startPoint = {
  left: 10,
  top: 10
};
const endPoint = {
  left: 40,
  top: 40
};
slide.insertLine(
    SlidesApp.LineCategory.STRAIGHT,
    startPoint.left,
    startPoint.top,
    endPoint.left,
    endPoint.top,
);
```

**Parameters**

- `lineCategory` (`LineCategory`) — The category of the line to insert.
- `startLeft` (`Number`) — The horizontal position of the start point of the line, measured in points from the upper left corner of the page.
- `startTop` (`Number`) — The vertical position of the start point of the line, measured in points from the upper left corner of the page.
- `endLeft` (`Number`) — The horizontal position of the end point of the line, measured in points from the upper left corner of the page.
- `endTop` (`Number`) — The vertical position of the end point of the line, measured in points from the upper left corner of the page.

**Returns**

`Line` — The inserted line.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertPageElement(pageElement)

`PageElement`

Inserts a copy of the provided PageElement on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a page element between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const pageElement = otherPresentationSlide.getPageElements()[0];

// Also available for Layout, Master, and Page.
currentPresentationSlide.insertPageElement(pageElement);
```

**Parameters**

- `pageElement` (`PageElement`) — The page element to be copied and inserted.

**Returns**

`PageElement` — The inserted page element.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertShape(shape)

`Shape`

Inserts a copy of the provided Shape on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a shape between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const shape = otherPresentationSlide.getShapes[0];
currentPresentationSlide.insertShape(
    shape);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `shape` (`Shape`) — The shape to be copied and inserted.

**Returns**

`Shape` — The inserted shape.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertShape(shapeType)

`Shape`

Inserts a shape on the page.

The shape is inserted with a default size at the top left corner of the page.

```javascript
// Insert a shape in the first slide of the presentation.
const slide = SlidesApp.getActivePresentation().getSlides()[0];

// Also available for Layout, Master, and Page.
slide.insertShape(SlidesApp.ShapeType.RECTANGLE);
```

**Parameters**

- `shapeType` (`ShapeType`) — The type of shape to insert.

**Returns**

`Shape` — The inserted shape.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertShape(shapeType, left, top, width, height)

`Shape`

Inserts a shape on the page.

**Parameters**

- `shapeType` (`ShapeType`) — The type of shape to insert.
- `left` (`Number`) — The horizontal position of the shape, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the shape, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the shape.
- `height` (`Number`) — The height of the shape.

**Returns**

`Shape` — The inserted shape.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sourceChart)

`SheetsChart`

Inserts a Google Sheets chart on the page.

The chart is inserted with a default size at the top left corner of the page.

The inserted chart is linked with the source Google Sheets chart which allows it to be updated. Other collaborators can see the link to the source spreadsheet.

```javascript
const sheet = SpreadsheetApp.openById('spreadsheetId').getSheets()[0];
const chart = sheet.getCharts()[0];
// Insert the spreadsheet chart in the first slide.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.insertSheetsChart(chart);
```

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The chart in a spreadsheet to be inserted in the page.

**Returns**

`SheetsChart` — The inserted chart in the page.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sourceChart, left, top, width, height)

`SheetsChart`

Inserts a Google Sheets chart on the page with the provided position and size.

In order to maintain the chart's aspect ratio, the chart is scaled and centered with respect to the provided size.

The inserted chart is linked with the source Google Sheets chart which allows it to be updated. Other collaborators can see the link to the source spreadsheet.

```javascript
const sheet = SpreadsheetApp.openById('spreadsheetId').getSheets()[0];
const chart = sheet.getCharts()[0];
// Insert the spreadsheet chart in the first slide.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const position = {
  left: 0,
  top: 0
};
const size = {
  width: 200,
  height: 200
};

// Also available for Layout, Master, and Page.
slide.insertSheetsChart(
    chart,
    position.left,
    position.top,
    size.width,
    size.height,
);
```

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The chart in a spreadsheet to be inserted in the page.
- `left` (`Number`) — The horizontal position of the chart in points, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the chart in points, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the chart in points.
- `height` (`Number`) — The height of the chart in points.

**Returns**

`SheetsChart` — The inserted chart in the page.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSheetsChart(sheetsChart)

`SheetsChart`

Inserts a copy of the provided SheetsChart on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a sheets chart between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const sheetsChart = otherPresentationSlide.getSheetsCharts[0];

// Also available for Layout, Master, and Page.
currentPresentationSlide.insertSheetsChart(sheetsChart);
```

**Parameters**

- `sheetsChart` (`SheetsChart`) — The sheets chart to be copied and inserted.

**Returns**

`SheetsChart` — The inserted sheets chart.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSheetsChartAsImage(sourceChart)

`Image`

Inserts a Google Sheets chart as an Image on the page.

The image of the chart is inserted with a default size at the top left corner of the page.

The inserted image of chart is not linked with the source Google Sheets chart.

```javascript
const sheet = SpreadsheetApp.openById('spreadsheetId').getSheets()[0];
const chart = sheet.getCharts()[0];
// Insert the spreadsheet chart in the first slide.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.insertSheetsChartAsImage(
    chart);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The chart in a spreadsheet to be inserted in the page.

**Returns**

`Image` — The inserted image of the chart in the page.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSheetsChartAsImage(sourceChart, left, top, width, height)

`Image`

Inserts a Google Sheets chart as an Image on the page with the provided position and size.

In order to maintain the chart image's aspect ratio, the image is scaled and centered with respect to the provided size.

The inserted image of the chart is not linked with the source Google Sheets chart.

```javascript
const sheet = SpreadsheetApp.openById('spreadsheetId').getSheets()[0];
const chart = sheet.getCharts()[0];
// Insert the spreadsheet chart in the first slide.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
const position = {
  left: 0,
  top: 0
};
const size = {
  width: 200,
  height: 200
};

// Also available for Layout, Master, and Page.
slide.insertSheetsChartAsImage(
    chart,
    position.left,
    position.right,
    size.width,
    size.height,
);
```

**Parameters**

- `sourceChart` (`EmbeddedChart`) — The chart in a spreadsheet to be inserted in the page.
- `left` (`Number`) — The horizontal position of the chart in points, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the chart in points, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the chart in points.
- `height` (`Number`) — The height of the chart in points.

**Returns**

`Image` — The inserted image of the chart in the page.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertTable(numRows, numColumns)

`Table`

Inserts a table on the page.

The table is centered on the page with default size and evenly distributed rows and columns.

**Parameters**

- `numRows` (`Integer`) — The number of rows in the table.
- `numColumns` (`Integer`) — The number of columns in the table.

**Returns**

`Table` — The inserted table.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertTable(numRows, numColumns, left, top, width, height)

`Table`

Inserts a table on the page with the provided position and size.

Rows and columns are evenly distributed in the created table.

**Parameters**

- `numRows` (`Integer`) — The number of rows in the table.
- `numColumns` (`Integer`) — The number of columns in the table.
- `left` (`Number`) — The horizontal position of the table, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the table, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the table.
- `height` (`Number`) — The minimum height of the table. The actual height of the rendered table depends on factors such as text font size.

**Returns**

`Table` — The inserted table.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertTable(table)

`Table`

Inserts a copy of the provided Table on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a table between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const table = otherPresentationSlide.getTables[0];
currentPresentationSlide.insertTable(
    table);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `table` (`Table`) — The table to be copied and inserted.

**Returns**

`Table` — The inserted table.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertTextBox(text)

`Shape`

Inserts a text box Shape containing the provided string on the page.

The text box shape is inserted with a default size at the top left corner of the page.

```javascript
// Insert text box with "Hello" on the first slide of presentation.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.insertTextBox('Hello');  // Also available for Layout, Master, and Page.
```

**Parameters**

- `text` (`String`) — The string the text box shape should contain.

**Returns**

`Shape` — The inserted text box shape.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertTextBox(text, left, top, width, height)

`Shape`

Inserts a text box Shape containing the provided string on the page.

```javascript
// Insert text box with "Hello" on the first slide of presentation. This text
// box is a square with a length of 10 points on each side.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.insertTextBox(
    'Hello', 0, 0, 10, 10);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `text` (`String`) — The string the text box shape should contain.
- `left` (`Number`) — The horizontal position of the text box shape, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the text box shape, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the text box shape.
- `height` (`Number`) — The height of the text box shape.

**Returns**

`Shape` — The inserted text box shape.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertVideo(videoUrl)

`Video`

Inserts a video at the top left corner of the page with a default size.

Only YouTube videos are currently supported.

**Parameters**

- `videoUrl` (`String`) — The URL of the video to insert.

**Returns**

`Video` — The inserted video.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertVideo(videoUrl, left, top, width, height)

`Video`

Inserts a video on the page with the provided position and size.

Only YouTube videos are currently supported.

**Parameters**

- `videoUrl` (`String`) — The URL of the video to insert.
- `left` (`Number`) — The horizontal position of the video in points, measured from the upper left corner of the page.
- `top` (`Number`) — The vertical position of the video in points, measured from the upper left corner of the page.
- `width` (`Number`) — The width of the video in points.
- `height` (`Number`) — The height of the video in points.

**Returns**

`Video` — The inserted video.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertVideo(video)

`Video`

Inserts a copy of the provided Video on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a video between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const video = otherPresentationSlide.getVideos[0];
currentPresentationSlide.insertVideo(
    video);  // Also available for Layout, Master, and Page.
```

**Parameters**

- `video` (`Video`) — The video to be copied and inserted.

**Returns**

`Video` — The inserted video.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertWordArt(wordArt)

`WordArt`

Inserts a copy of the provided WordArt on the page.

The inserted element's position on this page is determined from the source element's position on its respective page.

If the provided element is a placeholder being copied from within the current presentation, properties that inherit from master or layout pages also inherit on the inserted element.

If the provided element is a placeholder being copied from a different presentation, properties that inherit from master or layout pages are copied onto the element from the source presentation.

```javascript
// Copy a word art between presentations.
const otherPresentationSlide =
    SlidesApp.openById('presentationId').getSlides()[0];
const currentPresentationSlide =
    SlidesApp.getActivePresentation().getSlides()[0];
const wordArt = otherPresentationSlide.getWordArts[0];

// Also available for Layout, Master, and Page.
currentPresentationSlide.insertWordArt(wordArt);
```

**Parameters**

- `wordArt` (`WordArt`) — The group to be copied and inserted.

**Returns**

`WordArt` — The inserted word art.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### isSkipped()

`Boolean`

Returns whether the slide is skipped in the presentation mode.

**Returns**

`Boolean` — True if the slide is skipped in the presentation mode.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### move(index)

Move the slide to the specified index.

**Parameters**

- `index` (`Integer`) — The index where the slide should be moved to, based on the slide arrangement before the move. The index should be between zero and the number of slides in the presentation, inclusive.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### refreshSlide()

Refreshes the slide to reflect any changes made to the linked source slide. If this slide is not linked, returns without making any changes.

The refreshSlide method copies the linked source slide's corresponding master and layout pages into the slide's presentation if they do not already exist. If they do already exist, they are likewise updated to reflect any changes made to the source.

Note: The refresh overwrites any changes made to the current slide in order to reflect the state of the source slide.

```javascript
const currentPresentation = SlidesApp.getActivePresentation();
const sourcePresentation = SlidesApp.openById('sourcePresentationId');
const sourceSlide = sourcePresentation.getSlides()[0];
const linkedSlide = currentPresentation.append(
    sourceSlide,
    SlidesApp.SlideLinkingMode.LINKED,
);

sourceSlide.insertText(
    'hello world');  // Only the source slide has the text box.

linkedSlide.refreshSlide();  // The linked slide now has the text box.
```

**Throws**

Error — If read-access to the source presentation is no longer available.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### remove()

Removes the page.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text. The search is case insensitive.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.
- `matchCase` (`Boolean`) — If true, the search is case sensitive; if false, the search is case insensitive.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### selectAsCurrentPage()

Selects the Page in the active presentation as the current page selection and removes any previous selection.

A script can only access the selection of the user who is running the script, and only if the script is bound to the presentation.

```javascript
// Select the first slide as the current page selection and replace any previous
// selection.
const slide = SlidesApp.getActivePresentation().getSlides()[0];
slide.selectAsCurrentPage();  // Also available for Layout, Master, and Page.
```

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setSkipped(isSkipped)

Sets whether the slide is skipped in the presentation mode.

**Parameters**

- `isSkipped` (`Boolean`) — True to skip the slide in the presentation mode.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### unlink()

Unlinks the current Slide from its source slide. If this slide is not linked, returns without making any changes.

```javascript
const currentPresentation = SlidesApp.getActivePresentation();
const sourcePresentation = SlidesApp.openById('sourcePresentationId');
const sourceSlide = sourcePresentation.getSlides()[0];
const linkedSlide = currentPresentation.append(
    sourceSlide,
    SlidesApp.SlideLinkingMode.LINKED,
);

linkedSlide.unlink();

linkedSlide.getSourcePresentationId();  // returns null
linkedSlide.getSourceSlideObjectId();   // returns null
linkedSlide
    .getSlideLinkingMode();  // returns SlidesApp.SlideLinkingMode.NOT_LINKED
```

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
