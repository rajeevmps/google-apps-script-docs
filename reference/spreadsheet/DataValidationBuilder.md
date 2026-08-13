# DataValidationBuilder

Builder for data validation rules.

The DataValidationBuilder is used to construct data validation rules in a spreadsheet. You can define rules to require specific data types like dates, numbers, text, or values from a list or range. Builders can be copied to easily modify existing data validation rules. You can configure whether invalid input results in a warning or is rejected entirely. Help text can be set to appear when a user hovers over a cell with data validation.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `DataValidation` | Constructs a data validation rule from the settings applied to the builder. |
| `copy()` | `DataValidationBuilder` | Creates a builder for a data validation rule based on this rule's settings. |
| `getAllowInvalid()` | `Boolean` | Returns `true` if the rule shows a warning when input fails data validation, or `false` if it rejects the input entirely. The default for new data validation rules is `true`. |
| `getCriteriaType()` | `DataValidationCriteria` | Gets the rule's criteria type as defined in the `DataValidationCriteria` enum. To get the arguments for the criteria, use `getCriteriaValues()`. To use these values to create or modify a data validation rule, see `withCriteria(criteria, args)`. |
| `getCriteriaValues()` | `Object[]` | Gets an array of arguments for the rule's criteria. To get the criteria type, use `getCriteriaType()`. To use these values to create or modify a data validation rule, see `withCriteria(criteria, args)`. |
| `getHelpText()` | `String` | Gets the rule's help text, or `null` if no help text is set. |
| `requireCheckbox()` | `DataValidationBuilder` | Sets the data validation rule to require that the input is a boolean value; this value is rendered as a checkbox. |
| `requireCheckbox(checkedValue: Object)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is the specified value or blank. When the input matches the specified value the cell is rendered as a checked checkbox. When the input is blank the cell is rendered as an unchecked checkbox. |
| `requireCheckbox(checkedValue: Object, uncheckedValue: Object)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is one of the specified values. When the input is `checkedValue` the cell is rendered as a checked checkbox. When the input is `uncheckedValue` the cell is rendered as an unchecked checkbox. |
| `requireDate()` | `DataValidationBuilder` | Sets the data validation rule to require a date. |
| `requireDateAfter(date: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date after the given value. The time fields of the `Date` object are ignored; only the day, month, and year fields are used. |
| `requireDateBefore(date: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date before the given value. The time fields of the `Date` object are ignored; only the day, month, and year fields are used. |
| `requireDateBetween(start: Date, end: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date that falls between, or is either of, two specified dates. The time fields of the `Date` objects are ignored; only the day, month, and year fields are used. |
| `requireDateEqualTo(date: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date equal to the given value. The time fields of the `Date` object are ignored; only the day, month, and year fields are used. |
| `requireDateNotBetween(start: Date, end: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date that does not fall between, and is neither of, two specified dates. The time fields of the `Date` objects are ignored; only the day, month, and year fields are used. |
| `requireDateOnOrAfter(date: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date on or after the given value. The time fields of the `Date` object are ignored; only the day, month, and year fields are used. |
| `requireDateOnOrBefore(date: Date)` | `DataValidationBuilder` | Sets the data validation rule to require a date on or before the given value. The time fields of the `Date` object are ignored; only the day, month, and year fields are used. |
| `requireFormulaSatisfied(formula: String)` | `DataValidationBuilder` | Sets the data validation rule to require that the given formula evaluates to `true`. |
| `requireNumberBetween(start: Number, end: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number that falls between, or is either of, two specified numbers. |
| `requireNumberEqualTo(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number equal to the given value. |
| `requireNumberGreaterThan(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number greater than the given value. |
| `requireNumberGreaterThanOrEqualTo(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number greater than or equal to the given value. |
| `requireNumberLessThan(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number less than the given value. |
| `requireNumberLessThanOrEqualTo(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number less than or equal to the given value. |
| `requireNumberNotBetween(start: Number, end: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number that does not fall between, and is neither of, two specified numbers. |
| `requireNumberNotEqualTo(number: Number)` | `DataValidationBuilder` | Sets the data validation rule to require a number not equal to the given value. |
| `requireTextContains(text: String)` | `DataValidationBuilder` | Sets the data validation rule to require that the input contains the given value. |
| `requireTextDoesNotContain(text: String)` | `DataValidationBuilder` | Sets the data validation rule to require that the input does not contain the given value. |
| `requireTextEqualTo(text: String)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is equal to the given value. |
| `requireTextIsEmail()` | `DataValidationBuilder` | Sets the data validation rule to require that the input is in the form of an email address. |
| `requireTextIsUrl()` | `DataValidationBuilder` | Sets the data validation rule to require that the input is in the form of a URL. |
| `requireValueInList(values: String[])` | `DataValidationBuilder` | Sets the data validation rule to require that the input is equal to one of the given values. |
| `requireValueInList(values: String[], showDropdown: Boolean)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is equal to one of the given values, with an option to hide the dropdown menu. |
| `requireValueInRange(range: Range)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is equal to a value in the given range. |
| `requireValueInRange(range: Range, showDropdown: Boolean)` | `DataValidationBuilder` | Sets the data validation rule to require that the input is equal to a value in the given range, with an option to hide the dropdown menu. |
| `setAllowInvalid(allowInvalidData: Boolean)` | `DataValidationBuilder` | Sets whether to show a warning when input fails data validation or whether to reject the input entirely. |
| `setHelpText(helpText: String)` | `DataValidationBuilder` | Sets the help text that appears when the user hovers over the cell on which data validation is set. |
| `withCriteria(criteria: DataValidationCriteria, args: Object[])` | `DataValidationBuilder` | Sets the data validation rule to criteria defined by `DataValidationCriteria` values, typically taken from the `criteria` and `arguments` of an existing rule. |

## Code Samples

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const range = SpreadsheetApp.getActive().getRange('B1:B10');
const rule =
    SpreadsheetApp.newDataValidation().requireValueInRange(range).build();
cell.setDataValidation(rule);
```

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule = SpreadsheetApp.newDataValidation().requireCheckbox().build();
cell.setDataValidation(rule);
```

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule = SpreadsheetApp.newDataValidation()
                 .requireCheckbox('APPROVED', 'PENDING')
                 .build();
cell.setDataValidation(rule);
```

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule =
    SpreadsheetApp.newDataValidation()
        .requireDateBetween(new Date('1/1/2013'), new Date('12/31/2013'))
        .build();
cell.setDataValidation(rule);
```

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule =
    SpreadsheetApp.newDataValidation().requireNumberBetween(1, 10).build();
cell.setDataValidation(rule);
```

```javascript
const cell = SpreadsheetApp.getActive().getRange('A1');
const rule = SpreadsheetApp.newDataValidation()
                 .requireFormulaSatisfied('=EQ(A1,B1)')
                 .build();
cell.setDataValidation(rule);
```
