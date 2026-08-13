# CheckboxValidationBuilder

A DataValidationBuilder for a CheckboxValidation.

A `DataValidationBuilder` for a `CheckboxValidation`. This builder enables developers to establish validation constraints for checkbox form items, specifically controlling how many selections users must make. Obtained via `FormApp.createCheckboxValidation()`.

## Code Sample

```javascript
const checkBoxValidation = FormApp.createCheckboxValidation()
                               .setHelpText('Select two condiments.')
                               .requireSelectExactly(2)
                               .build();
```

## Methods

### requireSelectAtLeast(number)
`requireSelectAtLeast(number: Integer): CheckboxValidationBuilder`

Require at least this many choices to be selected.

### requireSelectAtMost(number)
`requireSelectAtMost(number: Integer): CheckboxValidationBuilder`

Require at most this many choices to be selected.

### requireSelectExactly(number)
`requireSelectExactly(number: Integer): CheckboxValidationBuilder`

Require exactly this many choices to be selected.
