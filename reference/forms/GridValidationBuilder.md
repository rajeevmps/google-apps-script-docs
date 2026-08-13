# GridValidationBuilder

A DataValidationBuilder for a GridValidation.

A `DataValidationBuilder` for a `GridValidation` in Google Apps Script forms. It enables developers to set validation rules for grid items, such as enforcing response limits per column. Obtained via `FormApp.createGridValidation()`.

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

### requireLimitOneResponsePerColumn()
`requireLimitOneResponsePerColumn(): GridValidationBuilder`

Enforces a restriction that allows only one response selection per column within a grid item.
