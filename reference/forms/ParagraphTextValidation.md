# ParagraphTextValidation

A DataValidation for a ParagraphTextItem.

A `DataValidation` for a `ParagraphTextItem` in Google Forms that allows you to establish validation rules for paragraph text responses. Instances are created via `ParagraphTextValidationBuilder.build()` and applied with `ParagraphTextItem.setValidation(validation)`.

## Code Sample

```javascript
const form = FormApp.create('My Form');
const paragraphTextItem = form.addParagraphTextItem().setTitle('Describe yourself:');
const paragraphTextValidation = FormApp.createParagraphTextValidation()
    .setHelpText('Answer must be more than 100 characters.')
    .requireTextLengthGreaterThanOrEqualTo(100)
    .build();
paragraphTextItem.setValidation(paragraphTextValidation);
```

## Methods

This class has no public methods of its own beyond those inherited as a built validation object; validation rules are configured on the corresponding `ParagraphTextValidationBuilder` (via `setHelpText(helpText)` and the various `requireText...` methods) and finalized with `build()`, which returns a `ParagraphTextValidation` instance.
