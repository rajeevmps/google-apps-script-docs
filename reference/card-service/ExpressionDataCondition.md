# ExpressionDataCondition

Represents a CEL expression validation result. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setConditionType(type: ExpressionDataConditionType): ExpressionDataCondition

Sets condition type for a CEL expression validation to indicate whether the expression evaluated successfully.

Parameters:
- `type` (ExpressionDataConditionType) - The type of the expression data condition.

Returns: This object, for chaining.

```javascript
const expressionDataCondition = CardService.newExpressionDataCondition()
.setConditionType(CardService.ExpressionDataConditionType.EXPRESSION_EVALUATION_SUCCESS);
```
