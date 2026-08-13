# CheckboxItem

A question item that allows the respondent to select one or more checkboxes, as well as an optional "other" field.

A question item that allows the respondent to select one or more checkboxes, as well as an optional "other" field. Items are created or accessed from a `Form` using methods such as `Form.addCheckboxItem()`. When used in a quiz, these items are autograded.

## Methods

### clearValidation()
`clearValidation(): CheckboxItem`

Removes any data validation for this checkbox item.

### createChoice(value)
`createChoice(value: String): Choice`

Creates a new choice. The value parameter is the choice's value, which respondents see as a label when viewing the form.

### createChoice(value, isCorrect)
`createChoice(value: String, isCorrect: Boolean): Choice`

Creates a new choice. The value is the choice's label; isCorrect indicates whether the choice is a correct answer.

### createResponse(responses)
`createResponse(responses: String[]): ItemResponse`

Creates a new `ItemResponse` for this checkbox item. Accepts a `String` array containing values to be checked. Throws an exception if any of the values do not match a valid choice for this item, unless `showOtherOption(enabled)` is set to true.

### duplicate()
`duplicate(): CheckboxItem`

Creates a copy of this item and appends it to the end of the form.

### getChoices()
`getChoices(): Choice[]`

Gets all choices for an item. Returns an array of choices.

### getFeedbackForCorrect()
`getFeedbackForCorrect(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond correctly to a question.

### getFeedbackForIncorrect()
`getFeedbackForIncorrect(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond incorrectly to a question.

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

Gets the item's title (sometimes called header text).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### hasOtherOption()
`hasOtherOption(): Boolean`

Determines whether the item has an "other" option.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setChoiceValues(values)
`setChoiceValues(values: String[]): CheckboxItem`

Sets the choices for an item from an array of strings. Throws an exception if the given array is empty.

### setChoices(choices)
`setChoices(choices: Choice[]): CheckboxItem`

Sets an array of choices for an item. Throws an exception if the given array is null, empty, or contains null elements.

### setFeedbackForCorrect(feedback)
`setFeedbackForCorrect(feedback: QuizFeedback): CheckboxItem`

Sets the feedback to be shown to respondents when they respond correctly to a question.

### setFeedbackForIncorrect(feedback)
`setFeedbackForIncorrect(feedback: QuizFeedback): CheckboxItem`

Sets the feedback to be shown to respondents when they respond incorrectly to a question.

### setHelpText(text)
`setHelpText(text: String): CheckboxItem`

Sets the item's help text (sometimes called description text for layout items).

### setPoints(points)
`setPoints(points: Integer): CheckboxItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): CheckboxItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): CheckboxItem`

Sets the item's title (sometimes called header text).

### setValidation(validation)
`setValidation(validation: CheckboxValidation): CheckboxItem`

Sets the data validation for this checkbox item. Passing in null removes any prior validation.

### showOtherOption(enabled)
`showOtherOption(enabled: Boolean): CheckboxItem`

Sets whether the item has an "other" option. Default for new items is false.
