# FeedbackType

An enum representing supported feedback types.

An enum representing supported feedback types that can be accessed from `FormApp.FeedbackType`. You access properties by calling the parent class, name, and property (e.g., `FormApp.FeedbackType.CORRECT`).

## Code Sample

```javascript
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
const item = form.addListItem();
item.setTitle('Do you prefer cats or dogs?');
item.setChoices([
  item.createChoice('Dogs', true),
  item.createChoice('Cats', false),
]);
item.setFeedbackForCorrect(
    FormApp.createFeedback().setDisplayText('Dogs rule, cats drool.').build(),
);
```

## Properties

| Property | Description |
| --- | --- |
| `CORRECT` | Feedback that is automatically displayed to respondents for a question answered correctly. Correct feedback can only be attached to a question type that supports autograding (e.g. radio, checkbox, select). |
| `INCORRECT` | Feedback that is automatically displayed to respondents for a question answered incorrectly. Incorrect feedback can only be attached to a question type that supports autograding (e.g. radio, checkbox, select). |
| `GENERAL` | Feedback that is automatically displayed to respondents when they submit their response. General feedback can only be attached to question types that do not support auto-grading, but are gradeable (i.e. everything but grid). |
