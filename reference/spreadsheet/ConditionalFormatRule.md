# ConditionalFormatRule

Access conditional formatting rules.

Access conditional formatting rules. To create a new rule, use `SpreadsheetApp.newConditionalFormatRule()` and `ConditionalFormatRuleBuilder`. You can use `Sheet.setConditionalFormatRules(rules)` to set the rules for a given sheet.

For rules that use boolean condition criteria, you can access the formatting settings by calling `getBooleanCondition()` and using the methods on the returned `BooleanCondition` object.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copy()` | `ConditionalFormatRuleBuilder` | Returns a rule builder preset with this rule's settings. |
| `getBooleanCondition()` | `BooleanCondition\|null` | Retrieves the rule's `BooleanCondition` information if this rule uses boolean condition criteria. Otherwise returns `null`. Boolean conditions contain formatting settings such as font weight, font color, and background color. |
| `getGradientCondition()` | `GradientCondition\|null` | Retrieves the rule's `GradientCondition` information, if this rule uses gradient condition criteria. Otherwise returns `null`. |
| `getRanges()` | `Range[]` | Retrieves the ranges to which this conditional format rule is applied. |

## Code Samples

```javascript
const rule = SpreadsheetApp.getActiveSheet().getConditionalFormatRules()[0];
const booleanCondition = rule.getBooleanCondition();
if (booleanCondition != null) {
  Logger.log(booleanCondition.getCriteriaType());
}
```

```javascript
const rule = SpreadsheetApp.getActiveSheet().getConditionalFormatRules()[0];
const gradientCondition = rule.getGradientCondition();
if (gradientCondition != null) {
  Logger.log(gradientCondition.getMinColorObject().asRgbColor().asHexString());
}
```

```javascript
const rule = SpreadsheetApp.getActiveSheet().getConditionalFormatRules()[0];
const ranges = rule.getRanges();
for (let i = 0; i < ranges.length; i++) {
  Logger.log(ranges[i].getA1Notation());
}
```
