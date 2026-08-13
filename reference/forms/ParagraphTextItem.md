# ParagraphTextItem

A question item that allows the respondent to enter a block of text.

A question item that allows the respondent to enter a block of text. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### clearValidation()
`clearValidation(): ParagraphTextItem`

Removes any data validation for this paragraph text item.

### createResponse(response)
`createResponse(response: String): ItemResponse`

Creates a new `ItemResponse` for this paragraph text item. The `response` parameter is an answer to the question posed by the item.

### duplicate()
`duplicate(): ParagraphTextItem`

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
`setGeneralFeedback(feedback: QuizFeedback): ParagraphTextItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer (questions requiring manual grading).

### setHelpText(text)
`setHelpText(text: String): ParagraphTextItem`

Sets the item's help text (sometimes called description text for layout items).

### setPoints(points)
`setPoints(points: Integer): ParagraphTextItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): ParagraphTextItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): ParagraphTextItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### setValidation(validation)
`setValidation(validation: ParagraphTextValidation): ParagraphTextItem`

Sets the data validation for this paragraph text item. Passing in null or a `ParagraphTextValidation` instance on which no require functions have been called removes any prior validation.
