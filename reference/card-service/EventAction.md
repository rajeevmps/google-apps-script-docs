# EventAction

An EventAction to run when a CEL expression validation condition is met.

An EventAction to run when a CEL expression validation condition is met. Only available for Google Workspace add-ons that extend Google Workspace Studio.

```javascript
const eventAction = CardService.newEventAction()
  .setActionRuleId("CEL_TEXTBOX_EVALUATION_RULE_ID")
  .setExpressionDataAction(expressionDataAction)
  .addPostEventTrigger(trigger_success)
  .addPostEventTrigger(trigger_failure);
```

## Methods

### addPostEventTrigger(trigger: Trigger): EventAction

Adds a CEL expression validation condition to evaluate after the event action runs.

### setActionRuleId(actionRuleId: String): EventAction

Sets a unique identifier for the event action.

### setCommonWidgetAction(commonWidgetAction: CommonWidgetAction): EventAction

Set the common widget action for widgets.

### setExpressionDataAction(expressionDataAction: ExpressionDataAction): EventAction

Sets the CEL expression validation data action for widgets.
