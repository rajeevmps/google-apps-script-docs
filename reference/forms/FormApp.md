# FormApp

Allows a script to open an existing Form or create a new one.

Allows a script to open an existing `Form` or create a new one.

## Code Sample

```javascript
// Open a form by ID.
const existingForm = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');

// Create and open a form.
const newForm = FormApp.create('Form Name');
```

## Properties

| Property | Type | Description |
| --- | --- | --- |
| Alignment | Alignment | An enumeration of types of image alignment. |
| DestinationType | DestinationType | An enumeration of types of destinations that can store form responses. |
| FeedbackType | FeedbackType | An enumeration of types of form Feedbacks. |
| ItemType | ItemType | An enumeration of types of form Items. |
| PageNavigationType | PageNavigationType | An enumeration of possible behaviors for navigating pages. |
| RatingIconType | RatingIconType | An enumeration of rating icon types RatingIcons |

## Methods

### create(title)
`create(title: String): Form`

Creates and returns a new `Form`. Throws an exception if the given title is null or empty.

### create(title, isPublished)
`create(title: String, isPublished: Boolean): Form`

Creates and returns a new `Form` in the requested publish state. Throws an exception if the given title is null or empty.

### createCheckboxGridValidation()
`createCheckboxGridValidation(): CheckboxGridValidationBuilder`

Returns an instance of a `CheckboxGridValidationBuilder` which can be used to set validation on a `CheckboxGridItem`.

### createCheckboxValidation()
`createCheckboxValidation(): CheckboxValidationBuilder`

Returns an instance of a `CheckboxValidationBuilder` which can be used to set validation on a `CheckboxItem`.

### createFeedback()
`createFeedback(): QuizFeedbackBuilder`

Returns an instance of a `QuizFeedbackBuilder` which can be used to set feedback on a gradeable `Item`.

### createGridValidation()
`createGridValidation(): GridValidationBuilder`

Returns an instance of a `GridValidationBuilder` which can be used to set validation on a `GridItem`.

### createParagraphTextValidation()
`createParagraphTextValidation(): ParagraphTextValidationBuilder`

Returns an instance of a `ParagraphTextValidationBuilder` which can be used to set validation on a `ParagraphTextItem`.

### createTextValidation()
`createTextValidation(): TextValidationBuilder`

Returns an instance of a `TextValidationBuilder` which can be used to set validation on a `TextItem`.

### getActiveForm()
`getActiveForm(): Form`

Returns the form to which the script is container-bound. To interact with forms to which the script is not container-bound, use `openById(id)` or `openByUrl(url)` instead.

### getUi()
`getUi(): Ui`

Returns an instance of the form editor's user-interface environment that allows the script to add features like menus, dialogs, and sidebars.

### openById(id)
`openById(id: String): Form`

Returns the `Form` with the specified ID. Throws an exception if the ID is invalid or the user does not have permission to open the form.

### openByUrl(url)
`openByUrl(url: String): Form`

Returns the `Form` with the specified URL. Throws an exception if the URL is invalid or the user does not have permission to open the form.
