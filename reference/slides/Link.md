# Link

Represents a hypertext link in Google Slides.

The `Link` object represents a hypertext link in Google Slides. You can determine the type of a link using the `getLinkType()` method. Methods like `getLinkedSlide()`, `getSlideId()`, `getSlideIndex()`, and `getSlidePosition()` are used to retrieve information about linked slides for non-URL link types. The `getUrl()` method is used to retrieve the URL for external web page links. Accessing link information may require specific authorization scopes.

## Methods

| Method | Return Type | Brief Description |
|--------|-------------|-------------------|
| `getLinkType()` | `LinkType` | Returns the `LinkType`. |
| `getLinkedSlide()` | `Slide\|null` | Returns the linked `Slide` for non-URL links types, if it exists. |
| `getSlideId()` | `String\|null` | Returns the ID of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_ID`. |
| `getSlideIndex()` | `Integer\|null` | Returns the zero-based index of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_INDEX`. |
| `getSlidePosition()` | `SlidePosition\|null` | Returns the `SlidePosition` of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_POSITION`. |
| `getUrl()` | `String\|null` | Returns the URL to the external web page or `null` if the `LinkType` is not `LinkType.URL`. |

### getLinkType()

`LinkType`

Returns the `LinkType`.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null) {
  Logger.log(`Shape has a link of type: ${link.getLinkType()}`);
}
```

**Returns**

`LinkType` — the type of the link.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLinkedSlide()

`Slide|null`

Returns the linked `Slide` for non-URL links types, if it exists. Returns `null` if the slide doesn't exist in the presentation, or if the `LinkType` is `LinkType.URL`.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null && link.getLinkType() !== SlidesApp.LinkType.URL) {
  Logger.log(`Shape has link to slide: ${link.getLinkedSlide()}`);
}
```

**Returns**

`Slide|null` — the linked slide, or `null` if it doesn't exist or the link is a URL link.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlideId()

`String|null`

Returns the ID of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_ID`. Note that the slide with the returned ID might not exist.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null && link.getLinkType() === SlidesApp.LinkType.SLIDE_ID) {
  Logger.log(`Shape has link to slide with ID: ${link.getSlideId()}`);
}
```

**Returns**

`String|null` — the linked slide ID, or `null` if the link type is not `SLIDE_ID`.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlideIndex()

`Integer|null`

Returns the zero-based index of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_INDEX`. Note that the slide at the returned index might not exist.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null && link.getLinkType() === SlidesApp.LinkType.SLIDE_INDEX) {
  Logger.log(`Shape has link to slide with index: ${link.getSlideIndex()}`);
}
```

**Returns**

`Integer|null` — the linked slide index, or `null` if the link type is not `SLIDE_INDEX`.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlidePosition()

`SlidePosition|null`

Returns the `SlidePosition` of the linked `Slide` or `null` if the `LinkType` is not `LinkType.SLIDE_POSITION`. Note that the slide with the returned relative position might not exist.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null && link.getLinkType() === SlidesApp.LinkType.SLIDE_POSITION) {
  Logger.log(
      `Shape has link to slide with relative position: ${
          link.getSlidePosition()}`,
  );
}
```

**Returns**

`SlidePosition|null` — the linked slide position, or `null` if the link type is not `SLIDE_POSITION`.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getUrl()

`String|null`

Returns the URL to the external web page or `null` if the `LinkType` is not `LinkType.URL`.

```javascript
const shape = SlidesApp.getActivePresentation().getSlides()[0].getShapes()[0];
const link = shape.getLink();
if (link != null && link.getLinkType() === SlidesApp.LinkType.URL) {
  Logger.log(`Shape has link to URL: ${link.getUrl()}`);
}
```

**Returns**

`String|null` — the linked URL, or `null` if the link type is not `URL`.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
