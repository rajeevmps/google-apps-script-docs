# BooleanCondition

Access the boolean criteria and formatting of a conditional format rule.

A `BooleanCondition` is accessed within `ConditionalFormatRules` and each rule can have one boolean condition. The boolean condition contains criteria and formatting settings applied when the criteria evaluates true for a cell. Methods retrieve background color, font color, bold, italic, strikethrough, underline settings, criteria type, and criteria values.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getBackgroundObject()` | `Color\|null` | Gets the background color for this boolean condition. Returns `null` if not set. |
| `getBold()` | `Boolean\|null` | Returns `true` if this boolean condition bolds the text and returns `false` if this boolean condition removes bolding from the text. Returns `null` if bolding is unaffected. |
| `getCriteriaType()` | `BooleanCriteria` | Gets the rule's criteria type as defined in the `BooleanCriteria` enum. To get the arguments for the criteria, use `getCriteriaValues()`. |
| `getCriteriaValues()` | `Object[]` | Gets an array of arguments for the rule's criteria. To get the criteria type, use `getCriteriaType()`. |
| `getFontColorObject()` | `Color\|null` | Gets the font color for this boolean condition. Returns `null` if not set. |
| `getItalic()` | `Boolean\|null` | Returns `true` if this boolean condition italicises the text and returns `false` if this boolean condition removes italics from the text. Returns `null` if italics are unaffected. |
| `getStrikethrough()` | `Boolean\|null` | Returns `true` if this boolean condition strikes through the text and returns `false` if this boolean condition removes strikethrough from the text. Returns `null` if strikethrough is unaffected. |
| `getUnderline()` | `Boolean\|null` | Returns `true` if this boolean condition underlines the text and returns `false` if this boolean condition removes underlining from the text. Returns `null` if underlining is unaffected. |

### Deprecated Methods

| Method | Return Type | Description |
|---|---|---|
| `getBackground()` | `String\|null` | Gets the background color string for this boolean condition. Returns `null` if not set. |
| `getFontColor()` | `String\|null` | Gets the font color string for this boolean condition. Returns `null` if not set. |

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const color = rule.getBooleanCondition().getBackgroundObject();
  Logger.log(`Background color: ${color.asRgbColor().asHexString()}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const bold = rule.getBooleanCondition().getBold();
  Logger.log(`Bold: ${bold}`);
}
```

```javascript
const formats = SpreadsheetApp.getActiveSheet.getConditionalFormats();
SpreadsheetApp.getActiveSheet.getConditionalFormats().forEach((format) => {
  const booleanCondition = format.getBooleanCondition();
  if (booleanCondition) {
    const criteria = booleanCondition.getCriteriaType();
    const args = booleanCondition.getCriteriaValues();
    Logger.log(`The conditional format rule is ${criteria} ${args}`);
  }
});
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const color = rule.getBooleanCondition().getFontColorObject();
  Logger.log(`Font color: ${color.asRgbColor().asHexString()}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const italic = rule.getBooleanCondition().getItalic();
  Logger.log(`Italic: ${italic}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const strikethrough = rule.getBooleanCondition().getStrikethrough();
  Logger.log(`Strikethrough: ${strikethrough}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const underline = rule.getBooleanCondition().getUnderline();
  Logger.log(`Underline: ${underline}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  const color = rule.getBooleanCondition().getBackground();
  Logger.log(`Background color: ${color}`);
}
```

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const rules = sheet.getConditionalFormatRules();
for (const rule of rules) {
  Logger.log(`Font color: ${rule.getBooleanCondition().getFontColor()}`);
}
```
