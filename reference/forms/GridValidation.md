# GridValidation

A DataValidation for a GridItem.

A `DataValidation` for a `GridItem`. `GridValidation` is specifically designed for grid-type form items in Google Forms, enabling developers to set validation rules such as requiring one response per column and including custom help text to guide user input. Instances are created via `GridValidationBuilder.build()` and applied with `GridItem.setValidation(validation)`.

## Code Sample

```javascript
const form = FormApp.create('My Form');
const gridItem = form.addGridItem();
gridItem.setTitle('Rate your interests')
    .setRows(['Cars', 'Computers', 'Celebrities'])
    .setColumns(['Boring', 'So-so', 'Interesting']);
const gridValidation = FormApp.createGridValidation()
                           .setHelpText('Select one item per column.')
                           .requireLimitOneResponsePerColumn()
                           .build();
gridItem.setValidation(gridValidation);
```

## Methods

This class has no public methods of its own beyond those inherited as a built validation object; validation rules are configured on the corresponding `GridValidationBuilder` (via `setHelpText(helpText)` and `requireLimitOneResponsePerColumn()`) and finalized with `build()`, which returns a `GridValidation` instance.
