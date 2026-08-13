# CheckboxGridValidationBuilder

A DataValidationBuilder for a CheckboxGridValidation.

A `DataValidationBuilder` for a `CheckboxGridValidation`. It enables developers to enforce validation constraints on checkbox grid responses, such as limiting selections to one per column. Obtained via `FormApp.createCheckboxGridValidation()`.

## Code Sample

```javascript
const form = FormApp.openById('123abc');
const checkboxGridItem = form.addCheckboxGridItem();
checkboxGridItem.setTitle('Where did you celebrate New Years?')
    .setRows(['New York', 'San Francisco', 'London'])
    .setColumns(['2014', '2015', '2016', '2017']);
const checkboxGridValidation = FormApp.createCheckboxGridValidation()
                                   .setHelpText('Select one item per column.')
                                   .requireLimitOneResponsePerColumn()
                                   .build();
checkboxGridItem.setValidation(checkboxGridValidation);
```

## Methods

### requireLimitOneResponsePerColumn()
`requireLimitOneResponsePerColumn(): CheckboxGridValidationBuilder`

Requires limit of one response per column for a grid item. This method ensures that users select only one response per column in a checkbox grid item.
