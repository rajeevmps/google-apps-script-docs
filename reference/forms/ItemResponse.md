# ItemResponse

A response to one question item within a form.

A response to one question item within a form. Item responses can be accessed from `FormResponse` and created from any `Item` that asks the respondent to answer a question.

## Code Sample

```javascript
const formResponses = FormApp.getActiveForm().getResponses();
for (let i = 0; i < formResponses.length; i++) {
  const response = formResponses[i];
  const items = FormApp.getActiveForm().getItems();
  const item = items[0];
  const itemResponse = response.getGradableResponseForItem(item);
  if (itemResponse != null && itemResponse.getResponse() === 'Sometimes true') {
    const points = item.asMultipleChoiceItem().getPoints();
    itemResponse.setScore(points * 0.5);
    response.withItemGrade(itemResponse);
  }
}
FormApp.getActiveForm().submitGrades(formResponses);
```

## Methods

### getFeedback()
`getFeedback(): Object`

Gets the feedback that was given for the respondent's submitted answer. Returns a `QuizFeedback` for the question item.

### getItem()
`getItem(): Item`

Gets the question item that this response answers.

### getResponse()
`getResponse(): Object`

Gets the answer that the respondent submitted. For most types of question items, this returns a `String`. For `CheckboxItem` questions, this returns a `String[]` array containing the responder's choices. For `GridItem` questions, this returns a `String[]` array in which the answer at index n corresponds to the question at row n + 1 in the grid. For `CheckboxGridItem` questions, this returns a `String[][]` array in which the answers at row index n corresponds to the question at row n + 1 in the checkbox grid.

### getScore()
`getScore(): Object`

Gets the score for the respondent's submitted answer. Returns a `Double` representing the score.

### setFeedback(feedback)
`setFeedback(feedback: Object): ItemResponse`

Sets the feedback that should be displayed for the respondent's submitted answer. This method does not actually save the feedback in Forms until `Form.submitGrades(responses)` is called with the updated `FormResponse`s.

### setScore(score)
`setScore(score: Object): ItemResponse`

Sets the score for the respondent's submitted answer. A null value will clear the existing score. This method does not actually save the score in Forms until `Form.submitGrades(responses)` is called with the updated `FormResponse`s.
