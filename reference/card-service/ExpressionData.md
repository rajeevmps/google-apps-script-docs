# ExpressionData

The expression data that is used to evaluate an expression. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### addCondition(condition: Condition): ExpressionData

Adds a condition to the current expression data.

Parameters:
- `condition` (Condition) - The Condition to add.

Returns: This ExpressionData, for chaining.

### addEventAction(eventAction: EventAction): ExpressionData

Adds an event action to the current expression data.

Parameters:
- `eventAction` (EventAction) - The EventAction to add.

Returns: This ExpressionData, for chaining.

### setExpression(expression: String): ExpressionData

Sets the expression data value.

Parameters:
- `expression` (String) - The uncompiled CEL expression.

Returns: This ExpressionData, for chaining.

### setId(id: String): ExpressionData

Sets the expression data id.

Parameters:
- `id` (String) - The unique identifier of the ExpressionData.

Returns: This ExpressionData, for chaining.

```javascript
const expressionData = CardService.newExpressionData();
```
