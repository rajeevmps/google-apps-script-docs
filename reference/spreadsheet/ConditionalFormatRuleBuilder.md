# ConditionalFormatRuleBuilder

Builder for conditional formatting rules.

The `ConditionalFormatRuleBuilder` class serves as a builder for constructing conditional format rules in Google Sheets. It enables developers to programmatically define formatting that applies based on specific conditions, such as cell values, dates, formulas, or text patterns.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `build()` | `ConditionalFormatRule` | Constructs a conditional format rule from the settings applied to the builder. |
| `copy()` | `ConditionalFormatRuleBuilder` | Returns a rule builder preset with this rule's settings. |
| `getBooleanCondition()` | `BooleanCondition\|null` | Retrieves the rule's `BooleanCondition` information if this rule uses boolean condition criteria. Otherwise returns `null`. Boolean conditions contain formatting settings such as font weight, font color, and background color. |
| `getGradientCondition()` | `GradientCondition\|null` | Retrieves the rule's `GradientCondition` information, if this rule uses gradient condition criteria. Otherwise returns `null`. |
| `getRanges()` | `Range[]` | Retrieves the ranges to which this conditional format rule is applied. |
| `setBackground(color: String)` | `ConditionalFormatRuleBuilder` | Sets the background color for the conditional format rule's format. Passing in `null` removes the background color format setting from the rule. |
| `setBackgroundObject(color: Color)` | `ConditionalFormatRuleBuilder` | Sets the background color for the conditional format rule's format. Passing in `null` removes the background color format setting from the rule. |
| `setBold(bold: Boolean)` | `ConditionalFormatRuleBuilder` | Sets text bolding for the conditional format rule's format. If `bold` is `true`, the rule bolds text if the condition is met; if `false`, the rule removes any existing bolding if the condition is met. Passing in `null` removes the bold format setting from the rule. |
| `setFontColor(color: String)` | `ConditionalFormatRuleBuilder` | Sets the font color for the conditional format rule's format. Passing in `null` removes the font color format setting from the rule. |
| `setFontColorObject(color: Color)` | `ConditionalFormatRuleBuilder` | Sets the font color for the conditional format rule's format. Passing in `null` removes the font color format setting from the rule. |
| `setGradientMaxpoint(color: String)` | `ConditionalFormatRuleBuilder` | Clears the conditional format rule's gradient maxpoint value, and instead uses the maximum value in the rule's ranges. Also sets the gradient's maxpoint color to the input color. |
| `setGradientMaxpointObject(color: Color)` | `ConditionalFormatRuleBuilder` | Clears the conditional format rule's gradient maxpoint value, and instead uses the maximum value in the rule's ranges. Also sets the gradient's maxpoint color to the input color. |
| `setGradientMaxpointObjectWithValue(color: Color, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient maxpoint fields. |
| `setGradientMaxpointWithValue(color: String, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient maxpoint fields. |
| `setGradientMidpointObjectWithValue(color: Color, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient midpoint fields. |
| `setGradientMidpointWithValue(color: String, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient midpoint fields. |
| `setGradientMinpoint(color: String)` | `ConditionalFormatRuleBuilder` | Clears the conditional format rule's gradient minpoint value, and instead uses the minimum value in the rule's ranges. |
| `setGradientMinpointObject(color: Color)` | `ConditionalFormatRuleBuilder` | Clears the conditional format rule's gradient minpoint value, and instead uses the minimum value in the rule's ranges. |
| `setGradientMinpointObjectWithValue(color: Color, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient minpoint fields. |
| `setGradientMinpointWithValue(color: String, type: InterpolationType, value: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule's gradient minpoint fields. |
| `setItalic(italic: Boolean)` | `ConditionalFormatRuleBuilder` | Sets text italics for the conditional format rule's format. |
| `setRanges(ranges: Range)` | `ConditionalFormatRuleBuilder` | Sets one or more ranges to which this conditional format rule is applied. |
| `setStrikethrough(strikethrough: Boolean)` | `ConditionalFormatRuleBuilder` | Sets text strikethrough for the conditional format rule's format. |
| `setUnderline(underline: Boolean)` | `ConditionalFormatRuleBuilder` | Sets text underlining for the conditional format rule's format. |
| `whenCellEmpty()` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when the cell is empty. |
| `whenCellNotEmpty()` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when the cell is not empty. |
| `whenDateAfter(date: Date)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is after the given value. |
| `whenDateAfter(date: RelativeDate)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is after the given relative date. |
| `whenDateBefore(date: Date)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is before the given date. |
| `whenDateBefore(date: RelativeDate)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is before the given relative date. |
| `whenDateEqualTo(date: Date)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is equal to the given date. |
| `whenDateEqualTo(date: RelativeDate)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a date is equal to the given relative date. |
| `whenFormulaSatisfied(formula: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the given formula evaluates to `true`. |
| `whenNumberBetween(start: Number, end: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number falls between, or is either of, two specified values. |
| `whenNumberEqualTo(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number is equal to the given value. |
| `whenNumberGreaterThan(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number is greater than the given value. |
| `whenNumberGreaterThanOrEqualTo(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number is greater than or equal to the given value. |
| `whenNumberLessThan(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number less than the given value. |
| `whenNumberLessThanOrEqualTo(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number less than or equal to the given value. |
| `whenNumberNotBetween(start: Number, end: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number does not fall between, and is neither of, two specified values. |
| `whenNumberNotEqualTo(number: Number)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when a number is not equal to the given value. |
| `whenTextContains(text: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the input contains the given value. |
| `whenTextDoesNotContain(text: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the input does not contain the given value. |
| `whenTextEndsWith(text: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the input ends with the given value. |
| `whenTextEqualTo(text: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the input is equal to the given value. |
| `whenTextStartsWith(text: String)` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to trigger when that the input starts with the given value. |
| `withCriteria(criteria: BooleanCriteria, args: Object[])` | `ConditionalFormatRuleBuilder` | Sets the conditional format rule to criteria defined by `BooleanCriteria` values, typically taken from the `criteria` and `arguments` of an existing rule. |

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const range = sheet.getRange('A1:B3');
const rule = SpreadsheetApp.newConditionalFormatRule()
    .whenNumberBetween(1, 10)
    .setBackground('#FF0000')
    .setRanges([range])
    .build();
const rules = sheet.getConditionalFormatRules();
rules.push(rule);
sheet.setConditionalFormatRules(rules);
```
