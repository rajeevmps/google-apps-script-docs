# ListItem

A question item that allows the respondent to select one choice from a drop-down list.

A question item that allows the respondent to select one choice from a drop-down list. Items can be accessed or created from a `Form`.

## Methods

### createChoice(value)
`createChoice(value: String): Choice`

Creates a new choice.

### createChoice(value, isCorrect)
`createChoice(value: String, isCorrect: Boolean): Choice`

Creates a new choice.

### createChoice(value, navigationItem)
`createChoice(value: String, navigationItem: PageBreakItem): Choice`

Creates a new choice with a page-navigation option that jumps to a given page-break item. This is equivalent to `createChoice(value, navigationType)` with navigationType set to `FormApp.PageNavigationType.GO_TO_PAGE`. Choices that use page navigation cannot be combined in the same item with choices that do not use page navigation.

### createChoice(value, navigationType)
`createChoice(value: String, navigationType: PageNavigationType): Choice`

Creates a new choice with a page-navigation option. Choices that use page navigation cannot be combined in the same item with choices that do not use page navigation.

### createResponse(response)
`createResponse(response: String): ItemResponse`

Creates a new `ItemResponse` for this list item. Throws an exception if the response argument does not match a valid choice for this item.

### duplicate()
`duplicate(): ListItem`

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

### setChoiceValues(values)
`setChoiceValues(values: String[]): ListItem`

Sets the choices for an item from an array of strings. Throws an exception if the given array is empty.

### setChoices(choices)
`setChoices(choices: Choice[]): ListItem`

Sets an array of choices for an item. Throws an exception if the given array is empty or contains a null element.

### setFeedbackForCorrect(feedback)
`setFeedbackForCorrect(feedback: QuizFeedback): ListItem`

Sets the feedback to be shown to respondents when they respond correctly to a question.

### setFeedbackForIncorrect(feedback)
`setFeedbackForIncorrect(feedback: QuizFeedback): ListItem`

Sets the feedback to be shown to respondents when they respond incorrectly to a question.

### setHelpText(text)
`setHelpText(text: String): ListItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setPoints(points)
`setPoints(points: Integer): ListItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRequired(enabled)
`setRequired(enabled: Boolean): ListItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): ListItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
