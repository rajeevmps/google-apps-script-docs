# CheckboxGridItem

A question item, presented as a grid of columns and rows, that allows the respondent to select multiple choices per row from a sequence of checkboxes.

A question item, presented as a grid of columns and rows, that allows the respondent to select multiple choices per row from a sequence of checkboxes. Items can be accessed or created from a `Form` object.

## Code Sample

```javascript
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
const item = form.addCheckboxGridItem();
item.setTitle('Where did you celebrate New Years?')
    .setRows(['New York', 'San Francisco', 'London'])
    .setColumns(['2014', '2015', '2016', '2017']);
```

## Methods

### clearValidation()
`clearValidation(): CheckboxGridItem`

Removes any data validation for this grid item.

### createResponse(responses)
`createResponse(responses: String[][]): ItemResponse`

Creates a new `ItemResponse` for this checkbox grid item. The responses parameter must be a `String[][]` array containing as many values as the number of inputs. A null element for a non-required grid indicates no response to that row. Throws an exception if any of the values does not match a valid choice.

### duplicate()
`duplicate(): CheckboxGridItem`

Creates a copy of this item and appends it to the end of the form.

### getColumns()
`getColumns(): String[]`

Gets the values for every column in the grid. Returns an array of column values respondents see as labels.

### getHelpText()
`getHelpText(): String`

Gets the item's help text (sometimes called description text for layout items like `ImageItem`s, `PageBreakItem`s, and `SectionHeaderItem`s).

### getId()
`getId(): Integer`

Gets the item's unique identifier.

### getIndex()
`getIndex(): Integer`

Gets the index of the item among all the items in the form.

### getRows()
`getRows(): String[]`

Gets the values for every row in the grid. Returns an array of row values respondents see as labels.

### getTitle()
`getTitle(): String`

Gets the item's title (sometimes called header text, in the case of a `SectionHeaderItem`).

### getType()
`getType(): ItemType`

Gets the item's type, represented as an `ItemType`.

### isRequired()
`isRequired(): Boolean`

Determines whether the respondent must answer the question.

### setColumns(columns)
`setColumns(columns: String[]): CheckboxGridItem`

Sets the columns of the grid based on an array of values. Throws an exception if the given array is empty.

### setHelpText(text)
`setHelpText(text: String): CheckboxGridItem`

Sets the item's help text (sometimes called description text for layout items).

### setRequired(enabled)
`setRequired(enabled: Boolean): CheckboxGridItem`

Sets whether the respondent must answer the question.

### setRows(rows)
`setRows(rows: String[]): CheckboxGridItem`

Sets the rows of the grid based on an array of values. Throws an exception if the given array is empty.

### setTitle(title)
`setTitle(title: String): CheckboxGridItem`

Sets the item's title (sometimes called header text).

### setValidation(validation)
`setValidation(validation: CheckboxGridValidation): CheckboxGridItem`

Sets the data validation for this checkbox grid item. Passing in null or a validation without any require functions called will remove any prior validation.
