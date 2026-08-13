# ItemType

An enum representing the supported types of form items.

An enum representing the supported types of form items. Item types are accessed via `FormApp.ItemType`.

## Code Sample

```javascript
// Open a form by ID and add a new section header.
const form = FormApp.create('Form Name');
const item = form.addSectionHeaderItem();
item.setTitle('Title of new section');

// Check the item type.
if (item.getType() === FormApp.ItemType.SECTION_HEADER) {
  item.setHelpText('Description of new section.');
}
```

## Properties

| Property | Description |
| --- | --- |
| `CHECKBOX` | A question item that allows the respondent to select one or more checkboxes, as well as an optional "other" field. |
| `CHECKBOX_GRID` | A question item, presented as a grid of columns and rows, that allows the respondent to select multiple choices per row from a sequence of checkboxes. |
| `DATE` | A question item that allows the respondent to indicate a date. |
| `DATETIME` | A question item that allows the respondent to indicate a date and time. |
| `DURATION` | A question item that allows the respondent to indicate a length of time. |
| `GRID` | A question item, presented as a grid of columns and rows, that allows the respondent to select one choice per row from a sequence of radio buttons. |
| `IMAGE` | A layout item that displays an image. |
| `LIST` | A question item that allows the respondent to select one choice from a drop-down list. |
| `MULTIPLE_CHOICE` | A question item that allows the respondent to select one choice from a list of radio buttons or an optional "other" field. |
| `PAGE_BREAK` | A layout item that marks the start of a page. |
| `PARAGRAPH_TEXT` | A question item that allows the respondent to enter a block of text. |
| `RATING` | A question item that allows the respondent to give a rating. |
| `SCALE` | A question item that allows the respondent to choose one option from a numbered sequence of radio buttons. |
| `SECTION_HEADER` | A layout item that visually indicates the start of a section. |
| `TEXT` | A question item that allows the respondent to enter a single line of text. |
| `TIME` | A question item that allows the respondent to indicate a time of day. |
| `VIDEO` | A layout item that displays a YouTube video. |
| `FILE_UPLOAD` | A question item that lets the respondent upload a file. |
| `UNSUPPORTED` | An item that is currently not supported through APIs. |
