# LinearOptimizationConstraint

A LinearOptimizationConstraint object represents a linear constraint of the model.

A `LinearOptimizationConstraint` object represents a linear constraint of the form `lowerBound ≤ Sum(a(i) x(i)) ≤ upperBound`, where lower and upper bounds are constants, coefficients (a(i)) are constant values, and variables (x(i)) represent unknowns.

## Methods

### setCoefficient(variableName, coefficient)

Returns: `LinearOptimizationConstraint`

Sets the coefficient of a variable in the constraint. By default, variables have a coefficient of 0.

**Parameters**

| Name | Type | Description |
|---|---|---|
| variableName | String | the name of variable for which the coefficient is being set |
| coefficient | Number | coefficient being set |

```javascript
const engine = LinearOptimizationService.createEngine();
// Create a linear constraint with the bounds 0 and 10
const constraint = engine.addConstraint(0, 10);
// Create a variable so we can add it to the constraint
engine.addVariable('x', 0, 5);
// Set the coefficient of the variable in the constraint. The constraint is now:
// 0 <= 2 * x <= 5
constraint.setCoefficient('x', 2);
```

## Properties

None.
