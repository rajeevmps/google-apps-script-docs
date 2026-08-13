# DataValidation

Access data validation rules.

Access data validation rules. To create a new rule, use `SpreadsheetApp.newDataValidation()` and `DataValidationBuilder`. You can use `Range.setDataValidation(rule)` to set the validation rule for a range.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copy()` | `DataValidationBuilder` | Creates a builder for a data validation rule based on this rule's settings. |
| `getAllowInvalid()` | `Boolean` | Returns `true` if the rule shows a warning when input fails data validation, or `false` if it rejects the input entirely. The default for new data validation rules is `true`. Returns `true` if the rule allows input that fails data validation; `false` if not. |
| `getCriteriaType()` | `DataValidationCriteria` | Gets the rule's criteria type as defined in the `DataValidationCriteria` enum. To get the arguments for the criteria, use `getCriteriaValues()`. To use these values to create or modify a data validation rule, see `DataValidationBuilder.withCriteria(criteria, args)`. |
| `getCriteriaValues()` | `Object[]` | Gets an array of arguments for the rule's criteria. To get the criteria type, use `getCriteriaType()`. To use these values to create or modify a data validation rule, see `DataValidationBuilder.withCriteria(criteria, args)`. Returns an array of arguments appropriate to the rule's criteria type; the number of arguments and their type match the corresponding `require...()` method of the `DataValidationBuilder` class. |
| `getHelpText()` | `String` | Gets the rule's help text, or `null` if no help text is set. |

## Code Samples

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule = cell.getDataValidation();
if (rule != null) {
  const criteria = rule.getCriteriaType();
  const args = rule.getCriteriaValues();
  Logger.log('The data validation rule is %s %s', criteria, args);
} else {
  Logger.log('The cell does not have a data validation rule.');
}
```
