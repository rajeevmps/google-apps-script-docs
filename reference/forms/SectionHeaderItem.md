# SectionHeaderItem

A layout item that visually indicates the start of a section.

A layout item that visually indicates the start of a section. Items can be accessed or created from a `Form`.

## Code Sample

```javascript
// Open a form by ID and add a new section header.
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
const item = form.addSectionHeaderItem();
item.setTitle('Title of new section');
```

## Methods

### duplicate()
`duplicate(): SectionHeaderItem`

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
`setHelpText(text: String): SectionHeaderItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s). Parameter `text`: the new help text.

### setTitle(title)
`setTitle(title: String): SectionHeaderItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`). Parameter `title`: the new title or header text.
