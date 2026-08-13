# CheckboxGridValidation

A DataValidation for a CheckboxGridItem.

A `DataValidation` for a `CheckboxGridItem`. This class enables validation rules for checkbox grid form items, allowing developers to enforce constraints such as requiring one response per column in a checkbox grid. Instances of this class are created via `CheckboxGridValidationBuilder.build()` and applied to an item with `CheckboxGridItem.setValidation(validation)`.

## Code Sample

```javascript
const checkboxGridValidation = FormApp.createCheckboxGridValidation()
                                   .setHelpText('Select one item per column.')
                                   .requireLimitOneResponsePerColumn()
                                   .build();
```

## Methods

This class has no public methods of its own beyond those inherited as a built validation object; validation rules are configured on the corresponding `CheckboxGridValidationBuilder` (via `setHelpText(helpText)` and `requireLimitOneResponsePerColumn()`) and finalized with `build()`, which returns a `CheckboxGridValidation` instance.
