# Trigger

A trigger that runs CEL expression validation widget event actions according to the action rule ID.

A trigger that runs CEL expression validation widget event actions according to the action rule ID. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setActionRuleId(actionRuleId: String): Trigger

Sets the action rule id for the trigger.

Parameters:
- `actionRuleId` (String): The uuid that uniquely identifies an action.

Return: This object, for chaining.

```javascript
const trigger_success = CardService.newTrigger()
  .setActionRuleId("CEL_TEXTINPUT_SUCCESS_RULE_ID");

const trigger_failure = CardService.newTrigger()
  .setActionRuleId("CEL_TEXTINPUT_FAILURE_RULE_ID");

const eventAction = CardService.newEventAction()
  .setActionRuleId("CEL_TEXTINPUT_EVALUATION_RULE_ID")
  .setExpressionDataAction(expressionDataAction)
  .addPostEventTrigger(trigger_success)
  .addPostEventTrigger(trigger_failure);
```
