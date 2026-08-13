# ParagraphTextValidationBuilder

A DataValidationBuilder for a ParagraphTextValidation.

A `DataValidationBuilder` for a `ParagraphTextValidation`. This builder enables developers to establish validation constraints for paragraph text responses in Google Forms, supporting pattern matching and text length requirements. Obtained via `FormApp.createParagraphTextValidation()`.

## Code Sample

```javascript
// Add a paragraph text item to a form and require the answer to be at least 100
// characters.
const form = FormApp.create('My Form');
const paragraphTextItem =
    form.addParagraphTextItem().setTitle('Describe yourself:');
const paragraphtextValidation =
    FormApp.createParagraphTextValidation()
        .setHelpText('Answer must be more than 100 characters.')
        .requireTextLengthGreaterThan(100);
paragraphTextItem.setValidation(paragraphtextValidation);
```

## Methods

### requireTextContainsPattern(pattern)
`requireTextContainsPattern(pattern: String): ParagraphTextValidationBuilder`

Requires response to contain pattern.

### requireTextDoesNotContainPattern(pattern)
`requireTextDoesNotContainPattern(pattern: String): ParagraphTextValidationBuilder`

Requires response to not contain pattern.

### requireTextDoesNotMatchPattern(pattern)
`requireTextDoesNotMatchPattern(pattern: String): ParagraphTextValidationBuilder`

Requires response to not match pattern.

### requireTextLengthGreaterThanOrEqualTo(number)
`requireTextLengthGreaterThanOrEqualTo(number: Integer): ParagraphTextValidationBuilder`

Requires response length to be greater than or equal to value.

### requireTextLengthLessThanOrEqualTo(number)
`requireTextLengthLessThanOrEqualTo(number: Integer): ParagraphTextValidationBuilder`

Requires response length to be less than value.

### requireTextMatchesPattern(pattern)
`requireTextMatchesPattern(pattern: String): ParagraphTextValidationBuilder`

Requires response to match pattern.
