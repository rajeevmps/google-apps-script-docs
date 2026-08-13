# PageNavigationType

An enum representing the supported types of page navigation.

An enum representing the supported types of page navigation. Page navigation occurs after the respondent completes a page that contains the option, and only if the respondent chose that option. If the respondent chose multiple options with page-navigation instructions on the same page, only the last navigation option has any effect. Page navigation also has no effect on the last page of a form.

## Code Sample

```javascript
const form = FormApp.create('Form Name');
const item = form.addMultipleChoiceItem();
const pageBreak = form.addPageBreakItem();

const rightChoice = item.createChoice(
    'Vanilla',
    FormApp.PageNavigationType.SUBMIT,
);
const wrongChoice = item.createChoice(
    'Chocolate',
    FormApp.PageNavigationType.RESTART,
);
```

## Properties

| Property | Description |
| --- | --- |
| `CONTINUE` | Continue to the next page of the form after completing the current page. |
| `GO_TO_PAGE` | Jump to a specified page of the form after completing the current page. |
| `RESTART` | Restart the form from the beginning, without clearing answers entered so far, after completing the current page. |
| `SUBMIT` | Submit the form response after completing the current page. |
