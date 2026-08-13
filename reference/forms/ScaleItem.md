# ScaleItem

A question item that allows the respondent to choose one option from a numbered sequence of radio buttons.

A question item that allows the respondent to choose one option from a numbered sequence of radio buttons. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### createResponse(response)
`createResponse(response: Integer): ItemResponse`

Creates a new `ItemResponse` for this scale item. Throws an exception if the response argument is outside the bounds set for the item.

### duplicate()
`duplicate(): ScaleItem`

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

### getLeftLabel()
`getLeftLabel(): String`

Gets the label for the scale's lower bound, if any.

### getLowerBound()
`getLowerBound(): Integer`

Gets the scale's lower bound.

### getPoints()
`getPoints(): Integer`

Returns the point value of a gradeable item.

### getRightLabel()
`getRightLabel(): String`

Gets the label for the scale's upper bound, if any.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### getUpperBound()
`getUpperBound(): Integer`

Gets the scale's upper bound.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setBounds(lower, upper)
`setBounds(lower: Integer, upper: Integer): ScaleItem`

Sets the scale's lower and upper bounds. The lower bound must be 0 or 1. The upper bound must be between 3 and 10, inclusive.

### setGeneralFeedback(feedback)
`setGeneralFeedback(feedback: QuizFeedback): ScaleItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer (questions requiring manual grading).

### setHelpText(text)
`setHelpText(text: String): ScaleItem`

Sets the item's help text (sometimes called description text for layout items).

### setLabels(lower, upper)
`setLabels(lower: String, upper: String): ScaleItem`

Sets labels for the scale's lower and upper bounds.

### setPoints(points)
`setPoints(points: Integer): ScaleItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): ScaleItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): ScaleItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
