# NotesPage

A notes page in a presentation.

"A notes page in a presentation. These pages contain the content for presentation handouts, including a shape that contains the slide's speaker notes. Each slide has one corresponding notes page. Only the text in the speaker notes shape can be modified."

## Methods

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

- `id` (`String`) — The ID of the page element being retrieved.

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

### getSpeakerNotesShape()

`Shape`

Gets the shape containing the speaker notes on the page.

**Returns**

`Shape` — the shape containing the speaker notes.

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

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text. The search is case insensitive.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.

**Returns**

`Integer` — the number of occurrences changed.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.
- `matchCase` (`Boolean`) — If `true`, search is case sensitive; if `false`, search is case insensitive.

**Returns**

`Integer` — the number of occurrences changed.

**Authorization**

Requires `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

## Properties

None.
