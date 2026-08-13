# Structure of a presentation

## Page Summary

- A Google Slides Presentation is composed of pages, and a Page can have one or more page elements.
- There are various types of pages a presentation can contain, including Slide, Master, Layout, NotesPage, and NotesMasters.
- Each PageElement on a page can be one of several types, such as Shape, Line, Image, SheetsChart, Video, Table, WordArt, or Group.
- The visual appearance, size, and position of some page elements can be modified.

This guide describes the data types that make up a Slides
presentation. For additional detail on pages, page elements, and their
properties, see the corresponding section of the [Google Slides API
documentation](https://developers.google.com/slides/concepts/page-elements).

A Slides
[`Presentation`](https://developers.google.com/apps-script/reference/slides/presentation) is composed of
pages. A [`Page`](https://developers.google.com/apps-script/reference/slides/page) can have one or more page
elements.

![Diagram showing the hierarchical structure of a Google Slides presentation,
with Presentation at the top, containing Pages, and Pages containing Page
Elements.](https://developers.google.com/static/slides/api/images/presentation-architecture.png)

## Page types

There are various different types of pages that a presentation can contain. A
[`Page`](https://developers.google.com/apps-script/reference/slides/page) can be one of the following types:

| Page type | Description |
|---|---|
| [`Slide`](https://developers.google.com/apps-script/reference/slides/slide) | The pages that users see and flip between when the presentation is rendered on a screen. |
| [`Master`](https://developers.google.com/apps-script/reference/slides/master) | Contains placeholders that establish default text styles, as well as background and other shapes that make up the default background for all slides based on that master. |
| [`Layout`](https://developers.google.com/apps-script/reference/slides/layout) | Determines how content is arranged on each type of slide. |
| [`NotesPage`](https://developers.google.com/apps-script/reference/slides/notes-page) | Used for speaker's notes. |
| [`NotesMasters`](https://developers.google.com/apps-script/reference/slides/notes-master) | Used for speaker's notes. |

## Page element types

Each [`PageElement`](https://developers.google.com/apps-script/reference/slides/page-element) on a page can
be one of the following types:

| Page element type | Description |
|---|---|
| [`Shape`](https://developers.google.com/apps-script/reference/slides/shape) | A plain visual object, such as rectangles, ellipses, and text boxes. Shapes can contain text, so they are the most common page elements to build slides. |
| [`Line`](https://developers.google.com/apps-script/reference/slides/line) | A visual line, curve, or connector. |
| [`Image`](https://developers.google.com/apps-script/reference/slides/image) | A graphic imported into Slides. |
| [`SheetsChart`](https://developers.google.com/apps-script/reference/slides/sheets-chart) | A chart imported into Slides from Google Sheets. |
| [`Video`](https://developers.google.com/apps-script/reference/slides/video) | A video imported into Slides. |
| [`Table`](https://developers.google.com/apps-script/reference/slides/table) | A grid of content. |
| [`WordArt`](https://developers.google.com/apps-script/reference/slides/word-art) | A visual text element that behaves more like a shape. |
| [`Group`](https://developers.google.com/apps-script/reference/slides/group) | A set of page elements that are treated as an individual unit. They can be moved, scaled, and rotated together. |

The visual appearance of some page elements can be modified by changing their
[fill](https://developers.google.com/apps-script/reference/slides/fill),
[border](https://developers.google.com/apps-script/reference/slides/border), and
[text](https://developers.google.com/apps-script/reference/slides/text-range). Also change a page element's
[size and position](https://developers.google.com/apps-script/guides/slides/moving-elements).
