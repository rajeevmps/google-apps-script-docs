# ExpressionDataConditionType

An enum that represents whether a CEL expression evaluated successfully.

An enum that represents whether a CEL (Common Expression Language) expression evaluated successfully. Only available through the Gemini Alpha program for Google Workspace add-ons that extend Google Workspace Flows.

## Properties

### CONDITION_TYPE_UNSPECIFIED
The unspecified condition type.

### EXPRESSION_EVALUATION_SUCCESS
The CEL expression evaluated to a successful result.

### EXPRESSION_EVALUATION_FAILURE
The CEL expression evaluated to a failure result.

## Code Sample

```javascript
const expressionDataCondition = CardService.newExpressionDataCondition()
.setConditionType(CardService.ExpressionDataConditionType.EXPRESSION_EVALUATION_SUCCESS);
```
