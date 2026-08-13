# Item

A generic form item that contains properties common to all items.

A generic form item that contains properties common to all items, such as title and help text. Items can be accessed or created from a `Form`.

To work with specific item types, developers should use `getType()` to check the item's `ItemType`, then cast to the appropriate class using methods like `asCheckboxItem()`.

## Code Sample

```javascript
const form = FormApp.create('Form Name');
form.addTextItem();

const items = form.getItems();
const item = items[0];

if (item.getType() === 'TEXT') {
  const textItem = item.asTextItem();
  textItem.setRequired(false);
}
```

## Methods

### asCheckboxGridItem()
`asCheckboxGridItem(): CheckboxGridItem`

Returns the item as a checkbox grid item. Throws a scripting exception if the `ItemType` was not already `CHECKBOX_GRID`.

### asCheckboxItem()
`asCheckboxItem(): CheckboxItem`

Returns the item as a checkbox item. Throws a scripting exception if the `ItemType` was not already `CHECKBOX`.

### asDateItem()
`asDateItem(): DateItem`

Returns the item as a date item. Throws a scripting exception if the `ItemType` was not already `DATE`.

### asDateTimeItem()
`asDateTimeItem(): DateTimeItem`

Returns the item as a date-time item. Throws a scripting exception if the `ItemType` was not already `DATETIME`.

### asDurationItem()
`asDurationItem(): DurationItem`

Returns the item as a duration item. Throws a scripting exception if the `ItemType` was not already `DURATION`.

### asGridItem()
`asGridItem(): GridItem`

Returns the item as a grid item. Throws a scripting exception if the `ItemType` was not already `GRID`.

### asImageItem()
`asImageItem(): ImageItem`

Returns the item as an image item. Throws a scripting exception if the `ItemType` was not already `IMAGE`.

### asListItem()
`asListItem(): ListItem`

Returns the item as a list item. Throws a scripting exception if the `ItemType` was not already `LIST`.

### asMultipleChoiceItem()
`asMultipleChoiceItem(): MultipleChoiceItem`

Returns the item as a multiple-choice item. Throws a scripting exception if the `ItemType` was not already `MULTIPLE_CHOICE`.

### asPageBreakItem()
`asPageBreakItem(): PageBreakItem`

Returns the item as a page-break item. Throws a scripting exception if the `ItemType` was not already `PAGE_BREAK`.

### asParagraphTextItem()
`asParagraphTextItem(): ParagraphTextItem`

Returns the item as a paragraph-text item. Throws a scripting exception if the `ItemType` was not already `PARAGRAPH_TEXT`.

### asRatingItem()
`asRatingItem(): RatingItem`

Returns the item as a rating item. Throws a ScriptingException if the `ItemType` was not already `RATING`.

### asScaleItem()
`asScaleItem(): ScaleItem`

Returns the item as a scale item. Throws a scripting exception if the `ItemType` was not already `SCALE`.

### asSectionHeaderItem()
`asSectionHeaderItem(): SectionHeaderItem`

Returns the item as a section-header item. Throws a scripting exception if the `ItemType` was not already `SECTION_HEADER`.

### asTextItem()
`asTextItem(): TextItem`

Returns the item as a text item. Throws a scripting exception if the `ItemType` was not already `TEXT`.

### asTimeItem()
`asTimeItem(): TimeItem`

Returns the item as a time item. Throws a scripting exception if the `ItemType` was not already `TIME`.

### asVideoItem()
`asVideoItem(): VideoItem`

Returns the item as a video item. Throws a scripting exception if the `ItemType` was not already `VIDEO`.

### duplicate()
`duplicate(): Item`

Creates a copy of this item and appends it to the end of the form.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### setHelpText(text)
`setHelpText(text: String): Item`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setTitle(title)
`setTitle(title: String): Item`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
