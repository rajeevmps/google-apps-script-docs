# PageBreakItem

A layout item that marks the start of a page.

A layout item that marks the start of a page. Items can be accessed or created from a `Form`.

## Methods

### duplicate()
`duplicate(): PageBreakItem`

Creates a copy of this item and appends it to the end of the form.

### getGoToPage()
`getGoToPage(): PageBreakItem`

Gets the `PageBreakItem` that the form will jump to after completing the page before this page break (that is, upon reaching this page break by normal linear progression through the form).

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getPageNavigationType()
`getPageNavigationType(): PageNavigationType`

Gets the type of page navigation that occurs after completing the page before this page break (that is, upon reaching this page break by normal linear progression through the form).

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### setGoToPage(goToPageItem)
`setGoToPage(goToPageItem: PageBreakItem): PageBreakItem`

Sets the page to jump to after completing the page before this page break (that is, upon reaching this page break by normal linear progression through the form). If the previous page contained a `MultipleChoiceItem` or `ListItem` with a navigation option, that navigation overrules this navigation.

### setGoToPage(navigationType)
`setGoToPage(navigationType: PageNavigationType): PageBreakItem`

Sets the type of page navigation that occurs after completing the page before this page break (that is, upon reaching this page break by normal linear progression through the form). If the page contained a `MultipleChoiceItem` or `ListItem` with a navigation option, that navigation overrules this navigation.

### setHelpText(text)
`setHelpText(text: String): PageBreakItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setTitle(title)
`setTitle(title: String): PageBreakItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
