# ExpressionDataAction

Actions for CEL expression validation. Use `START_EXPRESSION_EVALUATION` for CEL validation. Only available for Google Workspace add-ons that extend Google Workspace Studio.

## Methods

### setActionType(type: ExpressionDataActionType): ExpressionDataAction

Sets the type of the expression data action.

Parameters:
- `type` (ExpressionDataActionType) - The type of the expression data action.

Returns: This object, for chaining.

```javascript
const expressionDataAction = CardService.newExpressionDataAction()
.setActionType(CardService.ExpressionDataActionType.START_EXPRESSION_EVALUATION);
```
