# ExpressionDataActionType

An enum that represents the type of the expression data action.

An enum that represents the type of the expression data action. Only available through the Gemini Alpha program for Google Workspace add-ons that extend Google Workspace Flows.

## Properties

### ACTION_TYPE_UNSPECIFIED
The unspecified action type.

### START_EXPRESSION_EVALUATION
The action to start the CEL expression validation.

## Code Sample

```javascript
const expressionDataAction = CardService.newExpressionDataAction()
.setActionType(CardService.ExpressionDataActionType.START_EXPRESSION_EVALUATION);
```
