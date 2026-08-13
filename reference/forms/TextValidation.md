# TextValidation

A DataValidation for a TextItem.

A `DataValidation` for a `TextItem`. `TextValidation` is specifically designed for text input fields in Google Forms, allowing you to establish validation rules such as numeric ranges or custom requirements. Instances are created via `TextValidationBuilder.build()` and applied with `TextItem.setValidation(validation)`.

## Code Sample

```javascript
const form = FormApp.create('My form');
const textItem = form.addTextItem().setTitle('Pick a number between 1 and 100?');
const textValidation = FormApp.createTextValidation()
    .setHelpText('Input was not a number between 1 and 100.')
    .requireNumberBetween(1, 100)
    .build();
textItem.setValidation(textValidation);
```

## Methods

This class has no public methods of its own beyond those inherited as a built validation object; validation rules are configured on the corresponding `TextValidationBuilder` (via `setHelpText(helpText)` and the various `requireNumber...`/`requireText...` methods) and finalized with `build()`, which returns a `TextValidation` instance.
