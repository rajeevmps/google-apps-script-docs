# Edit and style text

## Page Summary

- Text ranges, represented by the `TextRange` type, allow you to edit and style segments of text within shapes or table cells.
- You can determine a text range's start and end indexes using `getStartIndex()` and `getEndIndex()`, and read its contents with `asString()` or `asRenderedString()`.
- Text ranges provide functions for inserting, deleting, and replacing text, including `insertText()`, `appendText()`, `setText()`, and `clear()`.
- You can search for and replace text globally using `replaceAllText()` on a presentation or page, or within a text range using `find()` and `setText()`.
- Text ranges allow access to collections of text entities like paragraphs, list items, and runs, and enable styling through `TextStyle`, `ParagraphStyle`, and `ListStyle` objects.

Edit and style text using *text ranges*, which are represented by the
`TextRange` type. A `TextRange` represents a segment of text within a shape or
within a table cell. Calling `getText` on a shape or table cell returns a
text range that covers the entire text.

If you use methods that edit how text fits within a shape, any autofit settings
applied to the shape are deactivated.

## Use text ranges

A text range has two indexes that delimit the segment of text
covered by a text range: the *start index* and *end index*. Determine
these indexes using the `getStartIndex` and `getEndIndex` functions.

A text range's start index is inclusive, and its end index
is exclusive. Both indexes are zero based.

To read the contents of a text range, use the `asString` or
`asRenderedString` functions.

To retrieve a subrange from within a text range, use the `getRange` function.

The following script creates a text box
on the first slide and sets its text content
to "Hello world!". It then retrieves a subrange that spans just the "Hello".

```javascript
try {
  // Get the first slide of active presentation
  const slide = SlidesApp.getActivePresentation().getSlides()[0];
  // Insert shape in the slide with dimensions
  const shape = slide.insertShape(
    SlidesApp.ShapeType.TEXT_BOX,
    100,
    200,
    300,
    60,
  );
  const textRange = shape.getText();
  // Set text in TEXT_BOX
  textRange.setText("Hello world!");
  console.log(
    `Start: ${textRange.getStartIndex()}; End: ${textRange.getEndIndex()}; Content: ${textRange.asString()}`,
  );
  const subRange = textRange.getRange(0, 5);
  console.log(
    `Sub-range Start: ${subRange.getStartIndex()}; Sub-range End: ${subRange.getEndIndex()}; Sub-range Content: ${subRange.asString()}`,
  );
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with an error %s ", err.message);
}
```

The text range returned by a shape or table cell always covers the entire text,
even if text is inserted and deleted. So this example produces the
following log statements:

```
Start: 0; End: 13; Content: Hello world!
Start: 0; End: 5; Content: Hello
```

## Insert and delete text

You can insert and delete text in shapes and table cells using text ranges.

- `insertText` and `appendText` let you insert text.
- `setText` replaces a text range's text with the provided text.
- `clear` deletes text from within a text range.

The following script demonstrates the use of these functions:

```javascript
try {
  // Get the first slide of active presentation
  const slide = SlidesApp.getActivePresentation().getSlides()[0];
  // Insert shape in the slide with dimensions
  const shape = slide.insertShape(
    SlidesApp.ShapeType.TEXT_BOX,
    100,
    200,
    300,
    60,
  );
  const textRange = shape.getText();
  textRange.setText("Hello world!");
  textRange.clear(6, 11);
  // Insert text in TEXT_BOX
  textRange.insertText(6, "galaxy");
  console.log(
    `Start: ${textRange.getStartIndex()}; End: ${textRange.getEndIndex()}; Content: ${textRange.asString()}`,
  );
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with an error %s ", err.message);
}
```

This script creates a text box on the first slide and sets its text content
to "Hello world!". It then deletes characters 6 through 11 ("world"), and
inserts the text "galaxy" at index 6 instead. This example produces the
following log statement:

```
Start: 0; End: 14; Content: Hello galaxy!
```

## Search and replace

Use the `replaceAllText` function on presentation or page to perform a global
find and replace across the entire presentation or a specific page.

The `find` function on TextRange returns the instances of a string within the
range. It can be used along with `setText` for performing find-and-replace
within a shape or table cell.

## Paragraphs, list items, and runs

`TextRange` provides functions to return useful collections of text entities.
Some of these functions include:

- `getParagraphs,` which provides all paragraphs which overlap the text range. A
paragraph is a sequence of text which terminates with the newline character,
"\n".
- `getListParagraphs,` which returns the list items in the current text range.
- `getRuns,` which provides the text runs that overlap the current text range. A
text run is a segment of text where all the characters have the same text
style.

## Text styling

Text style determines the rendering of text characters in your presentation,
including font, color, and hyperlinking.

The `getTextStyle` function of a text range provides a `TextStyle` object
used for
styling text. The `TextStyle` object covers the same text as its parent
`TextRange`.

```javascript
try {
  // Get the first slide of active presentation
  const slide = SlidesApp.getActivePresentation().getSlides()[0];
  // Insert shape in the slide with dimensions
  const shape = slide.insertShape(
    SlidesApp.ShapeType.TEXT_BOX,
    100,
    200,
    300,
    60,
  );
  const textRange = shape.getText();
  // Set text in TEXT_BOX
  textRange.setText("Hello ");
  // Append text in TEXT_BOX
  const insertedText = textRange.appendText("world!");
  // Style the text with url,bold
  insertedText
    .getTextStyle()
    .setBold(true)
    .setLinkUrl("www.example.com")
    .setForegroundColor("#ff0000");
  const helloRange = textRange.getRange(0, 5);
  console.log(
    `Text: ${helloRange.asString()}; Bold: ${helloRange.getTextStyle().isBold()}`,
  );
  console.log(
    `Text: ${insertedText.asString()}; Bold: ${insertedText.getTextStyle().isBold()}`,
  );
  console.log(
    `Text: ${textRange.asString()}; Bold: ${textRange.getTextStyle().isBold()}`,
  );
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with an error %s ", err.message);
}
```

The preceding example first creates a text box on the first slide and sets its
content to "Hello ". Then it appends the text "world!". The newly appended text
is bolded, linked to `www.example.com`, and its color is set
to red.

When reading styles, the function returns null if the range has multiple values
for the style. So this sample produces the following log statements:

```
Text: Hello; Bold: false
Text: world!; Bold: true
Text: Hello world!; Bold: null
```

There are many other styles that can be applied to text. More details can be
found in the `TextStyle` reference documentation.

## Paragraph styling

Paragraph styles apply to entire paragraphs, and include things like text
alignment and line
spacing. The `getParagraphStyle` function in `TextRange` provides a
`ParagraphStyle`
object for styling all the paragraphs that overlap the parent text range.

The following example creates a text box on the first slide with four
paragraphs, then center aligns the first three paragraphs.

```javascript
try {
  // Get the first slide of active presentation
  const slide = SlidesApp.getActivePresentation().getSlides()[0];
  // Insert shape in the slide with dimensions
  const shape = slide.insertShape(
    SlidesApp.ShapeType.TEXT_BOX,
    50,
    50,
    300,
    300,
  );
  const textRange = shape.getText();
  // Set the text in the shape/TEXT_BOX
  textRange.setText("Paragraph 1\nParagraph2\nParagraph 3\nParagraph 4");
  const paragraphs = textRange.getParagraphs();
  // Style the paragraph alignment center.
  for (let i = 0; i <= 3; i++) {
    const paragraphStyle = paragraphs[i].getRange().getParagraphStyle();
    paragraphStyle.setParagraphAlignment(SlidesApp.ParagraphAlignment.CENTER);
  }
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with an error %s ", err.message);
}
```

## List styling

Similar to `ParagraphStyle`, `ListStyle` can be used for styling all paragraphs
which overlap the parent text range.

```javascript
try {
  // Get the first slide of active presentation
  const slide = SlidesApp.getActivePresentation().getSlides()[0];
  // Insert shape in the slide with dimensions
  const shape = slide.insertShape(
    SlidesApp.ShapeType.TEXT_BOX,
    50,
    50,
    300,
    300,
  );
  // Add and style the list
  const textRange = shape.getText();
  textRange
    .appendText("Item 1\n")
    .appendText("\tItem 2\n")
    .appendText("\t\tItem 3\n")
    .appendText("Item 4");
  // Preset patterns of glyphs for lists in text.
  textRange
    .getListStyle()
    .applyListPreset(SlidesApp.ListPreset.DIGIT_ALPHA_ROMAN);
  const paragraphs = textRange.getParagraphs();
  for (let i = 0; i < paragraphs.length; i++) {
    const listStyle = paragraphs[i].getRange().getListStyle();
    console.log(
      `Paragraph ${i + 1}'s nesting level: ${listStyle.getNestingLevel()}`,
    );
  }
} catch (err) {
  // TODO (developer) - Handle exception
  console.log("Failed with an error %s ", err.message);
}
```

The preceding example creates a text box on the first slide, containing four
paragraphs:
the second paragraph is indented once and the third paragraph is indented
twice. Then it applies a list preset to all the paragraphs. Finally, each
paragraph's nesting level is logged. The paragraph's nesting level comes from
the number of tabs before the paragraph's text. So the script produces the
following log statements:

```
Paragraph 1's nesting level: 0
Paragraph 2's nesting level: 1
Paragraph 3's nesting level: 2
Paragraph 4's nesting level: 0
```
