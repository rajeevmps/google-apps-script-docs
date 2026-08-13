# GridItem

A question item, presented as a grid of columns and rows, that allows the respondent to select one choice per row from a sequence of radio buttons.

A question item, presented as a grid of columns and rows, that allows the respondent to select one choice per row from a sequence of radio buttons. Items can be accessed or created from a `Form`.

## Methods

### clearValidation()
`clearValidation(): GridItem`

Removes any data validation for this grid item.

### createResponse(responses)
`createResponse(responses: String[]): ItemResponse`

Creates a new `ItemResponse` for this grid item. The responses array must contain values matching the number of grid rows, with null indicating no response to non-required questions. Throws an exception if values don't match valid choices.

### duplicate()
`duplicate(): GridItem`

Creates a copy of this item and appends it to the end of the form.

### getColumns()
`getColumns(): String[]`

Returns an array of column values that respondents see as labels when viewing the form.

### getHelpText()
`getHelpText(): String`

Returns the item's help text (description text for layout items).

### getId()
`getId(): Integer`

Returns the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Returns the index of the item among all items in the form.

### getRows()
`getRows(): String[]`

Returns an array of row values that respondents see as labels when viewing the form.

### getTitle()
`getTitle(): String`

Returns the item's title (header text).

### getType()
`getType(): ItemType`

Returns the item's type as an `ItemType` representation.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setColumns(columns)
`setColumns(columns: String[]): GridItem`

Sets grid columns based on array values. Throws an exception if the array is empty or null.

### setHelpText(text)
`setHelpText(text: String): GridItem`

Sets the item's help text.

### setRequired(enabled)
`setRequired(enabled: Boolean): GridItem`

Sets whether respondents must answer the question.

### setRows(rows)
`setRows(rows: String[]): GridItem`

Sets grid rows based on array values. Throws an exception if the array is empty or null.

### setTitle(title)
`setTitle(title: String): GridItem`

Sets the item's title.

### setValidation(validation)
`setValidation(validation: GridValidation): GridItem`

Sets data validation for this grid item. Passing null removes any prior validation.
