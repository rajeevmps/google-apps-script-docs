# TimeItem

A question item that allows the respondent to indicate a time of day.

A question item that allows the respondent to indicate a time of day. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### createResponse(hour, minute)
`createResponse(hour: Integer, minute: Integer): ItemResponse`

Generates a response object for this time item. The hour and minute parameters should typically range from 0-23 and 0-59 respectively. Values exceeding these bounds wrap around like a clock (e.g., 10:90 becomes 11:30, -1:60 becomes 00:00).

### duplicate()
`duplicate(): TimeItem`

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

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setGeneralFeedback(feedback)
`setGeneralFeedback(feedback: QuizFeedback): TimeItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer (questions requiring manual grading).

### setHelpText(text)
`setHelpText(text: String): TimeItem`

Sets the item's help text (sometimes called description text for layout items).

### setPoints(points)
`setPoints(points: Integer): TimeItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): TimeItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): TimeItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
