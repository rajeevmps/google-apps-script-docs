# Choice

A single choice associated with a type of Item that supports choices.

A single choice associated with a type of `Item` that supports choices, like `CheckboxItem`, `ListItem`, or `MultipleChoiceItem`.

## Code Sample

```javascript
const form = FormApp.create('Form Name');
const item = form.addMultipleChoiceItem();
item.setTitle('Do you prefer cats or dogs?').setChoices([
  item.createChoice('Cats', FormApp.PageNavigationType.CONTINUE),
  item.createChoice('Dogs', FormApp.PageNavigationType.RESTART),
]);

form.addPageBreakItem().setTitle('You chose well!');

const choices = item.getChoices();
for (let i = 0; i < choices.length; i++) {
  Logger.log(
      'If the respondent chooses "%s", the form will %s.',
      choices[i].getValue(),
      choices[i].getPageNavigationType(),
  );
}
```

## Methods

### getGotoPage()
`getGotoPage(): PageBreakItem`

Gets the `PageBreakItem` set as a `GO_TO_PAGE` destination if the responder selects this choice and completes the current page. This method applies only to choices associated with `MultipleChoiceItem`s; for other choices, it returns null.

Returns: the `GO_TO_PAGE` destination for this choice, or null if there is none

### getPageNavigationType()
`getPageNavigationType(): PageNavigationType`

Gets the `PageNavigationType` that occurs if the responder selects this choice and completes the current page. This method applies only to choices associated with `MultipleChoiceItem`s; for other choices, it returns null.

Returns: the navigation action for this choice, or null if there is none

### getValue()
`getValue(): String`

Gets the choice's value, which respondents see as a label when viewing the form.

Returns: the choice's value

### isCorrectAnswer()
`isCorrectAnswer(): Boolean`

Gets whether the choice is a correct answer for the question. This method only applies to questions that are part of a quiz; for non-quiz forms, it returns false.

Returns: Whether the choice is a correct answer.
