# DateTimeItem

A question item that allows the respondent to indicate a date and time.

A question item that allows the respondent to indicate a date and time. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### createResponse(response)
`createResponse(response: Date): ItemResponse`

Creates a new `ItemResponse` for this date-time item. The seconds field of the Date object is ignored; by default, the year, month, day, hour, and minute fields are used.

### duplicate()
`duplicate(): DateTimeItem`

Creates a copy of this item and appends it to the end of the form.

### getGeneralFeedback()
`getGeneralFeedback(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond to a gradeable question.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items).

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

Gets the item's title (sometimes called header text).

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
`setGeneralFeedback(feedback: QuizFeedback): DateTimeItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer.

### setHelpText(text)
`setHelpText(text: String): DateTimeItem`

Sets the item's help text (sometimes called description text for layout items).

### setIncludesYear(enableYear)
`setIncludesYear(enableYear: Boolean): DateTimeItem`

Sets whether the date item includes a year setting. The default for new date items is true.

### setPoints(points)
`setPoints(points: Integer): DateTimeItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): DateTimeItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): DateTimeItem`

Sets the item's title (sometimes called header text).
