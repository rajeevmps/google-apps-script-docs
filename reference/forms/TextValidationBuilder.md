# TextValidationBuilder

A DataValidationBuilder for a TextValidation.

A `DataValidationBuilder` used for creating text validation rules in Google Forms. It provides methods to require text items to meet various criteria including numeric ranges, pattern matching, email/URL formats, and text length constraints. The builder supports method chaining to apply multiple validation rules. Obtained via `FormApp.createTextValidation()`.

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

### Numeric Validation Methods

#### requireNumber()
`requireNumber(): TextValidationBuilder`

Requires text item to be a number.

#### requireWholeNumber()
`requireWholeNumber(): TextValidationBuilder`

Requires text item to be a whole number.

#### requireNumberEqualTo(number)
`requireNumberEqualTo(number: Number): TextValidationBuilder`

Requires text item to be a number equal to value specified.

#### requireNumberNotEqualTo(number)
`requireNumberNotEqualTo(number: Number): TextValidationBuilder`

Requires text item to be a number not equal to the value specified.

#### requireNumberGreaterThan(number)
`requireNumberGreaterThan(number: Number): TextValidationBuilder`

Requires text item to be a number greater than the value specified.

#### requireNumberGreaterThanOrEqualTo(number)
`requireNumberGreaterThanOrEqualTo(number: Number): TextValidationBuilder`

Requires text item to be a number greater than or equal to the value specified.

#### requireNumberLessThan(number)
`requireNumberLessThan(number: Number): TextValidationBuilder`

Requires text item to be a number less than the value specified.

#### requireNumberLessThanOrEqualTo(number)
`requireNumberLessThanOrEqualTo(number: Number): TextValidationBuilder`

Requires text item to be a number less than or equal to the value specified.

#### requireNumberBetween(start, end)
`requireNumberBetween(start: Number, end: Number): TextValidationBuilder`

Requires text item to be a number between start and end, inclusive.

#### requireNumberNotBetween(start, end)
`requireNumberNotBetween(start: Number, end: Number): TextValidationBuilder`

Requires text item to be a number not between start and end, inclusive.

### Format Validation Methods

#### requireTextIsEmail()
`requireTextIsEmail(): TextValidationBuilder`

Requires text item to be an email address.

#### requireTextIsUrl()
`requireTextIsUrl(): TextValidationBuilder`

Requires text item to be a URL.

### Pattern Matching Methods

#### requireTextMatchesPattern(pattern)
`requireTextMatchesPattern(pattern: String): TextValidationBuilder`

Requires response to match pattern.

#### requireTextDoesNotMatchPattern(pattern)
`requireTextDoesNotMatchPattern(pattern: String): TextValidationBuilder`

Requires response to not match pattern.

#### requireTextContainsPattern(pattern)
`requireTextContainsPattern(pattern: String): TextValidationBuilder`

Requires response to contain pattern.

#### requireTextDoesNotContainPattern(pattern)
`requireTextDoesNotContainPattern(pattern: String): TextValidationBuilder`

Requires response to not contain pattern.

### Text Length Methods

#### requireTextLengthGreaterThanOrEqualTo(number)
`requireTextLengthGreaterThanOrEqualTo(number: Integer): TextValidationBuilder`

Requires response length to be greater than or equal to value.

#### requireTextLengthLessThanOrEqualTo(number)
`requireTextLengthLessThanOrEqualTo(number: Integer): TextValidationBuilder`

Requires response length to be less than value.
