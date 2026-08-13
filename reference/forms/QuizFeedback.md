# QuizFeedback

Represents feedback that can be associated with gradable form items.

Represents feedback that can be associated with gradable form items, containing properties like display text and helpful links. The feedback can be added to gradable Form items and is automatically shown when users respond to questions.

## Code Sample

```javascript
const form = FormApp.create('My Form');
const textItem = form.addTextItem().setTitle(
    'Re-hydrating dried fruit is an example of what?');
const feedback =
    FormApp.createFeedback()
        .setDisplayText(
            'Good answer, but not quite right.  Please review chapter 4 before next time.',
            )
        .addLink('http://wikipedia.com/osmosis');
textItem.setFeedbackForIncorrect(feedback);
```

## Methods

### getLinkUrls()
`getLinkUrls(): String[]`

Gets a list of the URLs associated with the Feedback. These are displayed to the user as a list of helpful links.

### getText()
`getText(): String`

Gets the Feedback's display text. This text is shown to the user after they've submitted a response.
