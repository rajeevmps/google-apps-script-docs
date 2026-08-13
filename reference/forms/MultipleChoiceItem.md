# MultipleChoiceItem

A question item that allows the respondent to select one choice from a list of radio buttons or an optional "other" field.

A question item that allows the respondent to select one choice from a list of radio buttons or an optional "other" field. When used in a quiz, these items are autograded.

## Methods

### createChoice(value)
`createChoice(value: String): Choice`

Creates a new choice.

### createChoice(value, isCorrect)
`createChoice(value: String, isCorrect: Boolean): Choice`

Creates a new choice, designating whether it represents a correct answer.

### createChoice(value, navigationItem)
`createChoice(value: String, navigationItem: PageBreakItem): Choice`

Creates a new choice with page-navigation capability directing to a specified page-break item. Navigation occurs after respondents complete a page containing the option. Page navigation cannot combine with non-navigating choices on the same item.

### createChoice(value, navigationType)
`createChoice(value: String, navigationType: PageNavigationType): Choice`

Creates a new choice incorporating page-navigation specifications. Navigating choices cannot mix with non-navigating choices within the same item.

### createResponse(response)
`createResponse(response: String): ItemResponse`

Creates a new `ItemResponse` for this multiple-choice item. Throws an exception if the response argument does not match a valid choice for this item, unless the "other" option is enabled.

### duplicate()
`duplicate(): MultipleChoiceItem`

Creates a copy of this item and appends it to the end of the form.

### getChoices()
`getChoices(): Choice[]`

Gets all choices for an item.

### getFeedbackForCorrect()
`getFeedbackForCorrect(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond correctly to a question.

### getFeedbackForIncorrect()
`getFeedbackForIncorrect(): QuizFeedback|null`

Returns the feedback that is shown to respondents when they respond incorrectly to a question.

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

### hasOtherOption()
`hasOtherOption(): Boolean`

Determines whether the item has an "other" option.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setChoiceValues(values)
`setChoiceValues(values: String[]): MultipleChoiceItem`

Sets the choices for an item from an array of strings. Throws an exception if the given array is empty.

### setChoices(choices)
`setChoices(choices: Choice[]): MultipleChoiceItem`

Sets an array of choices for an item. Throws an exception if the given array is null, empty, or contains null elements.

### setFeedbackForCorrect(feedback)
`setFeedbackForCorrect(feedback: QuizFeedback): MultipleChoiceItem`

Sets the feedback to be shown to respondents when they respond correctly to a question. A null value clears existing feedback.

### setFeedbackForIncorrect(feedback)
`setFeedbackForIncorrect(feedback: QuizFeedback): MultipleChoiceItem`

Sets the feedback to be shown to respondents when they respond incorrectly to a question.

### setHelpText(text)
`setHelpText(text: String): MultipleChoiceItem`

Sets the item's help text.

### setPoints(points)
`setPoints(points: Integer): MultipleChoiceItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): MultipleChoiceItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): MultipleChoiceItem`

Sets the item's title.

### showOtherOption(enabled)
`showOtherOption(enabled: Boolean): MultipleChoiceItem`

Sets whether the item has an "other" option. Default for new items is false.
