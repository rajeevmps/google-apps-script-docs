# RatingItem

A question item that allows the respondent to give a rating.

A question item that allows the respondent to give a rating. Items can be accessed or created from a `Form`. When used in a quiz, these items are graded.

## Methods

### createResponse(response)
`createResponse(response: Integer): ItemResponse`

Creates a new `ItemResponse` for this rating item. Throws a scripting exception if the provided response is less than 1 or greater than the value returned by `getRatingScaleLevel()`.

### duplicate()
`duplicate(): RatingItem`

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

### getRatingIcon()
`getRatingIcon(): RatingIconType`

Gets the icon chosen for the rating.

### getRatingScaleLevel()
`getRatingScaleLevel(): Integer`

Gets the rating's scale level.

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
`setGeneralFeedback(feedback: QuizFeedback): RatingItem`

Sets the feedback to be shown to respondents when they respond to a gradeable question that doesn't have a correct or incorrect answer (questions requiring manual grading).

### setHelpText(text)
`setHelpText(text: String): RatingItem`

Sets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### setPoints(points)
`setPoints(points: Integer): RatingItem`

Sets the number of points a gradeable item is worth. The default for new items is 0.

### setRatingIcon(ratingIcon)
`setRatingIcon(ratingIcon: RatingIconType): RatingItem`

Sets the rating's icon. Throws a scripting exception if the rating icon type is invalid.

### setRatingScaleLevel(ratingScaleLevel)
`setRatingScaleLevel(ratingScaleLevel: Integer): RatingItem`

Sets the rating's maximum scale level between 3 and 10 inclusive. A new rating defaults to 3. Throws an exception if the value is outside the permitted limits.

### setRequired(enabled)
`setRequired(enabled: Boolean): RatingItem`

Sets whether the respondent must answer the question.

### setTitle(title)
`setTitle(title: String): RatingItem`

Sets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).
