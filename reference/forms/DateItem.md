# DateItem

A question item that allows the respondent to indicate a date.

A question item that allows the respondent to indicate a date. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### createResponse(response)
`createResponse(response: Date): ItemResponse`

Creates a new `ItemResponse` for this date item. The time fields of the Date object are ignored; by default, only the year, month, and day fields are used.

### duplicate()
`duplicate(): DateItem`

Creates a copy of this item and appends it to the end of the form.

### getGeneralFeedback()
`getGeneralFeedback(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond to a gradeable question.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getPoints()
`getPoints(): Integer`

Returns the point value of a gradeable item.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### includesYear()
`includesYear(): Boolean`

Determines whether the date item includes a year option.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setGeneralFeedback(feedback)
`setGeneralFeedback(feedback: QuizFeedback): DateItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer.

### setHelpText(text)
`setHelpText(text: String): DateItem`

Sets the item's help text (sometimes called description text for layout items).

### setIncludesYear(enableYear)
`setIncludesYear(enableYear: Boolean): DateItem`

Sets whether the date item includes a year setting. The default for new date items is true.

### setPoints(points)
`setPoints(points: Integer): DateItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): DateItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): DateItem`

Sets the item's title (sometimes called header text).
