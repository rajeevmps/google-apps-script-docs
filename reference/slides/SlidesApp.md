# SlidesApp

Allows a script to create and open Presentations, which can be edited to change content, formatting, and other properties.

SlidesApp is used to create and open editable presentations. It enables creation and opening of Presentation objects that can be edited programmatically.

## Methods

### create(name)

`Presentation`

Creates and opens a new Presentation.

**Parameters**

- `name` (`String`) — The name to be given to the created presentation.

**Returns**

`Presentation` — the presentation with the given name

Requires authorization scope: `https://www.googleapis.com/auth/presentations`

### getActivePresentation()

`Presentation`

Returns the currently active presentation to which the script is container-bound, or null if there is no active presentation. To interact with a presentation to which the script is not container-bound, use openById(id) instead. If the presentation is already open, the same presentation instance is returned.

**Returns**

`Presentation` — the active presentation, or null if there is no active presentation

Requires scopes: `https://www.googleapis.com/auth/presentations.currentonly` or `https://www.googleapis.com/auth/presentations`

### getUi()

`Ui`

Returns an instance of the presentation's user-interface environment that allows the script to add features like menus, dialogs, and sidebars. A script can only interact with the UI for the current instance of an open presentation, and only if the script is bound to the presentation.

**Returns**

`Ui` — an instance of this presentation's user-interface environment

### newAffineTransformBuilder()

`AffineTransformBuilder`

Returns a new AffineTransformBuilder to build an AffineTransform.

**Returns**

`AffineTransformBuilder` — the new builder

### openById(id)

`Presentation`

Opens the Presentation with the given ID. If the presentation is already open, the same presentation instance is returned.

**Parameters**

- `id` (`String`) — the ID of the presentation to open

**Returns**

`Presentation` — the presentation with the given ID

Requires authorization scope: `https://www.googleapis.com/auth/presentations`

### openByUrl(url)

`Presentation`

Opens the Presentation with the given URL. If the presentation is already open, the same presentation instance is returned.

**Parameters**

- `url` (`String`) — the URL of the presentation to open

**Returns**

`Presentation` — the presentation with the given URL

Requires authorization scope: `https://www.googleapis.com/auth/presentations`

## Properties

SlidesApp exposes enumeration properties for styling and structure:

| Property | Type | Description |
| --- | --- | --- |
| `AlignmentPosition` | `AlignmentPosition` | An enumeration of the types of alignment positions. |
| `ArrowStyle` | `ArrowStyle` | An enumeration of the different arrow styles that a Line can have. |
| `AutoTextType` | `AutoTextType` | An enumeration of the types of auto text. |
| `AutofitType` | `AutofitType` | An enumeration of autofit types. |
| `CellMergeState` | `CellMergeState` | An enumeration of the different merge states of a table cell. |
| `ContentAlignment` | `ContentAlignment` | An enumeration of values used to specify content alignment. |
| `DashStyle` | `DashStyle` | An enumeration of the different dash styles that a Line can have. |
| `FillType` | `FillType` | An enumeration of fill types. |
| `LineCategory` | `LineCategory` | An enumeration of the categories of Line. |
| `LineFillType` | `LineFillType` | An enumeration of the types of LineFill. |
| `LineType` | `LineType` | An enumeration of the types of Line. |
| `LinkType` | `LinkType` | An enumeration of the types of links. |
| `ListPreset` | `ListPreset` | An enumeration of the types of list presets. |
| `PageBackgroundType` | `PageBackgroundType` | An enumeration of the types of page backgrounds. |
| `PageElementType` | `PageElementType` | An enumeration of the types of page elements. |
| `PageType` | `PageType` | An enumeration of the types of pages. |
| `ParagraphAlignment` | `ParagraphAlignment` | An enumeration of the types of paragraph alignment. |
| `PlaceholderType` | `PlaceholderType` | An enumeration of the types of placeholders. |
| `PredefinedLayout` | `PredefinedLayout` | An enumeration of the predefined layouts. |
| `SelectionType` | `SelectionType` | An enumeration of the types of selections. |
| `ShapeType` | `ShapeType` | An enumeration of the types of shapes. |
| `SheetsChartEmbedType` | `SheetsChartEmbedType` | An enumeration of Sheets chart embed types. |
| `SlideLinkingMode` | `SlideLinkingMode` | An enumeration of the ways Slides can be linked. |
| `SlidePosition` | `SlidePosition` | An enumeration of the types of slide positions. |
| `SpacingMode` | `SpacingMode` | An enumeration of the types of spacing modes. |
| `TextBaselineOffset` | `TextBaselineOffset` | An enumeration of the types of text baseline offset. |
| `TextDirection` | `TextDirection` | An enumeration of the types of text directions. |
| `ThemeColorType` | `ThemeColorType` | An enumeration of theme colors. |
| `VideoSourceType` | `VideoSourceType` | An enumeration of the types of video source. |
