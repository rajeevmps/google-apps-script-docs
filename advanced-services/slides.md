# Advanced Slides Service

Source: https://developers.google.com/apps-script/advanced/slides

## Overview

The Advanced Slides service enables Google Apps Script to read and edit Google Slides content by accessing the Slides API. This is an advanced service requiring explicit enablement before use.

## Key Features

- Access the Slides API through Apps Script
- Read and edit presentation content
- Uses identical objects, methods, and parameters as the public API
- Supports batch updates for efficient operations

## Sample Code Examples

### Create a New Presentation

```javascript
/**
 * Create a new presentation.
 * @return {string} presentation Id.
 * @see https://developers.google.com/slides/api/reference/rest/v1/presentations/create
 */
function createPresentation() {
  try {
    const presentation = Slides.Presentations.create({
      title: "MyNewPresentation",
    });
    console.log(`Created presentation with ID: ${presentation.presentationId}`);
    return presentation.presentationId;
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Create a New Slide

```javascript
/**
 * Create a new slide.
 * @param {string} presentationId The presentation to add the slide to.
 * @return {Object} slide
 * @see https://developers.google.com/slides/api/reference/rest/v1/presentations/batchUpdate
 */
function createSlide(presentationId) {
  const pageId = Utilities.getUuid();

  const requests = [
    {
      createSlide: {
        objectId: pageId,
        insertionIndex: 1,
        slideLayoutReference: {
          predefinedLayout: "TITLE_AND_TWO_COLUMNS",
        },
      },
    },
  ];
  try {
    const slide = Slides.Presentations.batchUpdate(
      { requests: requests },
      presentationId,
    );
    console.log(
      `Created Slide with ID: ${slide.replies[0].createSlide.objectId}`,
    );
    return slide;
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Read Page Element Object IDs

```javascript
/**
 * Read page element IDs.
 * @param {string} presentationId The presentation to read from.
 * @param {string} pageId The page to read from.
 * @return {Object} response
 * @see https://developers.google.com/slides/api/reference/rest/v1/presentations.pages/get
 */
function readPageElementIds(presentationId, pageId) {
  try {
    const response = Slides.Presentations.Pages.get(presentationId, pageId, {
      fields: "pageElements.objectId",
    });
    console.log(response);
    return response;
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Add a Text Box

```javascript
/**
 * Add a new text box with text to a page.
 * @param {string} presentationId The presentation ID.
 * @param {string} pageId The page ID.
 * @return {Object} response
 * @see https://developers.google.com/slides/api/reference/rest/v1/presentations/batchUpdate
 */
function addTextBox(presentationId, pageId) {
  const pageElementId = Utilities.getUuid();

  const requests = [
    {
      createShape: {
        objectId: pageElementId,
        shapeType: "TEXT_BOX",
        elementProperties: {
          pageObjectId: pageId,
          size: {
            width: {
              magnitude: 150,
              unit: "PT",
            },
            height: {
              magnitude: 50,
              unit: "PT",
            },
          },
          transform: {
            scaleX: 1,
            scaleY: 1,
            translateX: 200,
            translateY: 100,
            unit: "PT",
          },
        },
      },
    },
    {
      insertText: {
        objectId: pageElementId,
        text: "My Added Text Box",
        insertionIndex: 0,
      },
    },
  ];
  try {
    const response = Slides.Presentations.batchUpdate(
      { requests: requests },
      presentationId,
    );
    console.log(
      `Created Textbox with ID: ${response.replies[0].createShape.objectId}`,
    );
    return response;
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Format Shape Text

```javascript
/**
 * Format the text in a shape.
 * @param {string} presentationId The presentation ID.
 * @param {string} shapeId The shape ID.
 * @return {Object} replies
 * @see https://developers.google.com/slides/api/reference/rest/v1/presentations/batchUpdate
 */
function formatShapeText(presentationId, shapeId) {
  const requests = [
    {
      updateTextStyle: {
        objectId: shapeId,
        fields: "foregroundColor,bold,italic,fontFamily,fontSize,underline",
        style: {
          foregroundColor: {
            opaqueColor: {
              themeColor: "ACCENT5",
            },
          },
          bold: true,
          italic: true,
          underline: true,
          fontFamily: "Corsiva",
          fontSize: {
            magnitude: 18,
            unit: "PT",
          },
        },
        textRange: {
          type: "ALL",
        },
      },
    },
  ];
  try {
    const response = Slides.Presentations.batchUpdate(
      { requests: requests },
      presentationId,
    );
    return response.replies;
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

## Best Practices

### Batch Updates

**Recommended:** Combine multiple requests in an array when calling `batchUpdate` rather than executing it in a loop.

**Inefficient approach:**
```javascript
var titles = ["slide 1", "slide 2"];
for (var i = 0; i < titles.length; i++) {
  Slides.Presentations.batchUpdate(preso, {
    requests: [{
      createSlide: ...
    }]
  });
}
```

**Efficient approach:**
```javascript
var requests = [];
var titles = ["slide 1", "slide 2"];
for (var i = 0; i < titles.length; i++) {
  requests.push({ createSlide: ... });
}

Slides.Presentations.batchUpdate(preso, {
  requests: requests
});
```

## Reference Documentation

For detailed information: [Slides API reference](https://developers.google.com/slides/reference/rest) (external — not scraped)
</content>
