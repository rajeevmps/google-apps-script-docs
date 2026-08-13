# QuizFeedbackBuilder

The base FeedbackBuilder that contains setters for properties common to all feedback.

The base FeedbackBuilder that contains setters for properties common to all feedback, such as display text. Used to build `Feedback` objects. Obtained via `FormApp.createFeedback()`.

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
    FormApp.createFeedback().setText('Dogs rule, cats drool.').build(),
);
```

## Methods

### addLink(url)
`addLink(url: String): QuizFeedbackBuilder`

Adds a link to the feedback's supplemental material. Parameter `url`: the link to display under the display text.

### addLink(url, displayText)
`addLink(url: String, displayText: String): QuizFeedbackBuilder`

Adds a link to the feedback's supplemental material. Parameters: `url` - the link to display under the display text; `displayText` - the text to display for the link.

### setText(text)
`setText(text: String): QuizFeedbackBuilder`

Sets the feedback text. Parameter `text`: the new text.

### build()
`build(): QuizFeedback`

Builds a Feedback of the corresponding type for this builder.

### copy()
`copy(): QuizFeedbackBuilder`

Returns a copy of this builder.
