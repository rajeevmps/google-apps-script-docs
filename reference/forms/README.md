# Google Apps Script Forms Service — Reference Index

Local offline markdown copy of the Google Apps Script Forms service reference documentation (https://developers.google.com/apps-script/reference/forms), for use as coding context.

## Core

| Class | Description |
| --- | --- |
| [FormApp](./FormApp.md) | Allows a script to open an existing Form or create a new one. Entry point for the Forms service. |
| [Form](./Form.md) | A form that has been created and saved in Google Drive; the main object for reading/editing a form's items, settings, and responses. |
| [FormResponse](./FormResponse.md) | A response to the form as a whole; used to read submitted answers or programmatically build and submit a response. |
| [ItemResponse](./ItemResponse.md) | A response to one question item within a form. |
| [Item](./Item.md) | A generic form item with properties common to all items (title, help text); cast to a specific item type via `asXxxItem()` methods. |
| [Choice](./Choice.md) | A single choice associated with a choice-based item type, like `CheckboxItem`, `ListItem`, or `MultipleChoiceItem`. |

## Item Types

| Class | Description |
| --- | --- |
| [CheckboxGridItem](./CheckboxGridItem.md) | A grid question item where respondents select multiple checkboxes per row. |
| [CheckboxItem](./CheckboxItem.md) | A question item that allows selecting one or more checkboxes, with an optional "other" field. |
| [DateItem](./DateItem.md) | A question item that allows the respondent to indicate a date. |
| [DateTimeItem](./DateTimeItem.md) | A question item that allows the respondent to indicate a date and time. |
| [DurationItem](./DurationItem.md) | A question item that allows the respondent to indicate a length of time. |
| [GridItem](./GridItem.md) | A grid question item where respondents select one radio-button choice per row. |
| [ImageItem](./ImageItem.md) | A layout item that displays an image. |
| [ListItem](./ListItem.md) | A question item that allows the respondent to select one choice from a drop-down list. |
| [MultipleChoiceItem](./MultipleChoiceItem.md) | A question item that allows selecting one choice from a list of radio buttons, with an optional "other" field. |
| [PageBreakItem](./PageBreakItem.md) | A layout item that marks the start of a page. |
| [ParagraphTextItem](./ParagraphTextItem.md) | A question item that allows the respondent to enter a block of text. |
| [RatingItem](./RatingItem.md) | A question item that allows the respondent to give a rating. |
| [ScaleItem](./ScaleItem.md) | A question item that allows choosing one option from a numbered sequence of radio buttons. |
| [SectionHeaderItem](./SectionHeaderItem.md) | A layout item that visually indicates the start of a section. |
| [TextItem](./TextItem.md) | A question item that allows the respondent to enter a single line of text. |
| [TimeItem](./TimeItem.md) | A question item that allows the respondent to indicate a time of day. |
| [VideoItem](./VideoItem.md) | A layout item that displays a video. |

## Validation & Builders

| Class | Description |
| --- | --- |
| [CheckboxGridValidation](./CheckboxGridValidation.md) | A `DataValidation` for a `CheckboxGridItem`. |
| [CheckboxGridValidationBuilder](./CheckboxGridValidationBuilder.md) | A `DataValidationBuilder` for a `CheckboxGridValidation`. |
| [CheckboxValidation](./CheckboxValidation.md) | A `DataValidation` for a `CheckboxItem`. |
| [CheckboxValidationBuilder](./CheckboxValidationBuilder.md) | A `DataValidationBuilder` for a `CheckboxValidation`. |
| [GridValidation](./GridValidation.md) | A `DataValidation` for a `GridItem`. |
| [GridValidationBuilder](./GridValidationBuilder.md) | A `DataValidationBuilder` for a `GridValidation`. |
| [ParagraphTextValidation](./ParagraphTextValidation.md) | A `DataValidation` for a `ParagraphTextItem`. |
| [ParagraphTextValidationBuilder](./ParagraphTextValidationBuilder.md) | A `DataValidationBuilder` for a `ParagraphTextValidation`. |
| [TextValidation](./TextValidation.md) | A `DataValidation` for a `TextItem`. |
| [TextValidationBuilder](./TextValidationBuilder.md) | A `DataValidationBuilder` for a `TextValidation`. |
| [QuizFeedback](./QuizFeedback.md) | Feedback that can be associated with gradable form items (display text and helpful links). |
| [QuizFeedbackBuilder](./QuizFeedbackBuilder.md) | The base builder used to construct `QuizFeedback` objects. |

## Enums

| Enum | Description |
| --- | --- |
| [Alignment](./Alignment.md) | Types of image/video alignment (`LEFT`, `CENTER`, `RIGHT`). |
| [DestinationType](./DestinationType.md) | Types of destinations that can store form responses (`SPREADSHEET`). |
| [FeedbackType](./FeedbackType.md) | Types of form feedback (`CORRECT`, `INCORRECT`, `GENERAL`). |
| [ItemType](./ItemType.md) | Types of form items (`CHECKBOX`, `TEXT`, `MULTIPLE_CHOICE`, etc.). |
| [PageNavigationType](./PageNavigationType.md) | Behaviors for navigating between pages (`CONTINUE`, `GO_TO_PAGE`, `RESTART`, `SUBMIT`). |
| [RatingIconType](./RatingIconType.md) | Rating icon types (`STAR`, `HEART`, `THUMB_UP`). |
