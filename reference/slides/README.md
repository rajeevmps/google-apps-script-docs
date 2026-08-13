# Google Apps Script — Slides Service Reference

Offline local markdown copy of the [Google Apps Script Slides service reference](https://developers.google.com/apps-script/reference/slides), for use as coding context.

## Core

- [SlidesApp](SlidesApp.md) — Entry point for accessing and creating Slides presentations.
- [Presentation](Presentation.md) — The presentation itself, containing slides, masters, and layouts.
- [Selection](Selection.md) — The user's current selection in the active presentation.
- [SpeakerSpotlight](SpeakerSpotlight.md) — A page element that spotlights the speaker's video feed.

## Pages

- [Page](Page.md) — Base interface implemented by slides, layouts, masters, and notes pages.
- [Slide](Slide.md) — A slide in a presentation.
- [Layout](Layout.md) — A slide layout predefining slide content placement.
- [Master](Master.md) — A slide master defining common slide page properties.
- [NotesMaster](NotesMaster.md) — The master for notes pages.
- [NotesPage](NotesPage.md) — A notes page associated with a slide.
- [PageBackground](PageBackground.md) — The background of a page.
- [PageRange](PageRange.md) — A collection of Page objects.

## Page elements

- [PageElement](PageElement.md) — Base interface for any visual element on a page.
- [PageElementRange](PageElementRange.md) — A collection of PageElement objects.
- [Shape](Shape.md) — A generic shape page element.
- [Image](Image.md) — An image page element.
- [Line](Line.md) — A line page element.
- [Group](Group.md) — A collection of page elements joined as a single unit.
- [Table](Table.md) — A table page element.
- [TableCell](TableCell.md) — A single cell of a table.
- [TableCellRange](TableCellRange.md) — A collection of TableCell objects.
- [TableColumn](TableColumn.md) — A column of a table.
- [TableRow](TableRow.md) — A row of a table.
- [SheetsChart](SheetsChart.md) — A linked Google Sheets chart embedded in a presentation.
- [Video](Video.md) — A video page element.
- [WordArt](WordArt.md) — A word art page element.
- [AutoText](AutoText.md) — Auto-generated text, such as a slide number.
- [ConnectionSite](ConnectionSite.md) — A location on a page element that can be connected to by a Line.

## Positioning & transforms

- [AffineTransform](AffineTransform.md) — An affine transform used to move, scale, rotate, and shear page elements.
- [AffineTransformBuilder](AffineTransformBuilder.md) — Builder for AffineTransform objects.
- [Point](Point.md) — An (x, y) coordinate pair.

## Fills, borders, and color

- [Fill](Fill.md) — Base interface for the fill of a page element or shape.
- [SolidFill](SolidFill.md) — A fill that renders a single, solid color.
- [PictureFill](PictureFill.md) — A fill that renders an image.
- [LineFill](LineFill.md) — The fill of a Line.
- [Border](Border.md) — The border of a page element.
- [Color](Color.md) — A single color, either RGB or theme-based.
- [ColorScheme](ColorScheme.md) — The color scheme associated with a page.
- [ThemeColor](ThemeColor.md) — A theme color that references an entry in a ColorScheme.
- [Autofit](Autofit.md) — The autofit settings of a shape's text.

## Text & style

- [TextRange](TextRange.md) — A contiguous run of text within a Shape or TableCell.
- [TextStyle](TextStyle.md) — The text style of a range of text.
- [Paragraph](Paragraph.md) — A paragraph of text.
- [ParagraphStyle](ParagraphStyle.md) — The style properties of a Paragraph.
- [List](List.md) — A list of paragraphs sharing the same bulleting/numbering.
- [ListStyle](ListStyle.md) — The list style of the text in a range.
- [Link](Link.md) — A link to a URL, slide, or other resource.

## Enums

- [AlignmentPosition](AlignmentPosition.md) — Positions to which a page element can be aligned.
- [ArrowStyle](ArrowStyle.md) — Styles of arrows on the ends of a Line.
- [AutoTextType](AutoTextType.md) — Types of auto text.
- [AutofitType](AutofitType.md) — Types of shape text autofit.
- [CellMergeState](CellMergeState.md) — Merge states of a TableCell.
- [ContentAlignment](ContentAlignment.md) — Content alignment types for text within a shape/cell.
- [DashStyle](DashStyle.md) — Dash styles for the outline of a shape or line.
- [FillType](FillType.md) — Fill types for a page element.
- [LineCategory](LineCategory.md) — Categories of Line.
- [LineFillType](LineFillType.md) — Fill types for a Line.
- [LineType](LineType.md) — Types of Line.
- [LinkType](LinkType.md) — Types of Link destinations.
- [ListPreset](ListPreset.md) — Preset patterns of bullets/numbers for list creation.
- [PageBackgroundType](PageBackgroundType.md) — Types of page background.
- [PageElementType](PageElementType.md) — Types of PageElement.
- [PageType](PageType.md) — Types of Page.
- [ParagraphAlignment](ParagraphAlignment.md) — Types of paragraph text alignment.
- [PlaceholderType](PlaceholderType.md) — Types of placeholder page elements.
- [PredefinedLayout](PredefinedLayout.md) — Predefined slide layouts.
- [SelectionType](SelectionType.md) — Types of selection within a presentation.
- [ShapeType](ShapeType.md) — Types of shapes.
- [SheetsChartEmbedType](SheetsChartEmbedType.md) — Types of embedded Sheets charts.
- [SlideLinkingMode](SlideLinkingMode.md) — Modes for linking a slide to a source slide.
- [SlidePosition](SlidePosition.md) — Positions of a slide relative to others.
- [SpacingMode](SpacingMode.md) — Types of paragraph spacing.
- [TextBaselineOffset](TextBaselineOffset.md) — Types of text baseline offset (superscript/subscript).
- [TextDirection](TextDirection.md) — Directions of text within a text box or shape.
- [ThemeColorType](ThemeColorType.md) — Types of theme colors.
- [VideoSourceType](VideoSourceType.md) — Sources of a Video.

## Coverage

All 76 classes and enums from the Apps Script Slides reference are included. No fetch failures were encountered.
