# CheckboxValidation

A DataValidation for a CheckboxItem.

A `DataValidation` for a `CheckboxItem` that allows developers to configure validation requirements for checkbox selections, including setting help text and specifying exact selection counts. Instances are created via `CheckboxValidationBuilder.build()` and applied with `CheckboxItem.setValidation(validation)`.

## Code Sample

```javascript
const checkBoxValidation = FormApp.createCheckboxValidation()
                               .setHelpText('Select two condiments.')
                               .requireSelectExactly(2)
                               .build();
```

## Methods

This class has no public methods of its own beyond those inherited as a built validation object; validation rules are configured on the corresponding `CheckboxValidationBuilder` (via `setHelpText(helpText)`, `requireSelectAtLeast(number)`, `requireSelectAtMost(number)`, `requireSelectExactly(number)`) and finalized with `build()`, which returns a `CheckboxValidation` instance.
