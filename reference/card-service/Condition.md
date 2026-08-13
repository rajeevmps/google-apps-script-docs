# Condition

A condition used to run an event action as part of CEL expression validation.

A condition used to run an event action as part of CEL expression validation. Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const condition = CardService.newCondition()
  .setActionRuleId("CEL_TEXTBOX_SUCCESS_RULE_ID")
  .setExpressionDataCondition(CardService.newExpressionDataCondition()
    .setConditionType(CardService.ExpressionDataConditionType.EXPRESSION_EVALUATION_SUCCESS));
```

## Methods

### setActionRuleId(actionRuleId: String): Condition

The unique ID of the action rule to run in response to the condition.

### setExpressionDataCondition(expressionDataCondition: ExpressionDataCondition): Condition

Sets the CEL expression validation condition used to determine whether the event action should run.
