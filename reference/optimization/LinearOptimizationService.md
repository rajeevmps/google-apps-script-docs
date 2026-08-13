# LinearOptimizationService

The linear optimization service, used to model and solve linear and mixed-integer linear programs.

The linear optimization service, used to model and solve linear and mixed-integer linear programs. This service enables developers to add variables with upper and lower bounds via `addVariable()`, add constraints on linear expressions using `addConstraint()`, set objective functions with `setObjectiveCoefficient()`, `setMaximization()`, and `setMinimization()`, and create optimization engine instances through `createEngine()`.

## Methods

### createEngine()

Returns: `LinearOptimizationEngine`

Creates an engine to to solve linear programs (potentially mixed-integer programs).

```javascript
const engine = LinearOptimizationService.createEngine();

engine.addVariable('x', 0, 10);
engine.addVariable('y', 0, 5);

let constraint = engine.addConstraint(0, 10);
constraint.setCoefficient('x', 2);
constraint.setCoefficient('y', 5);

constraint = engine.addConstraint(0, 20);
constraint.setCoefficient('x', 10);
constraint.setCoefficient('y', 3);

engine.setObjectiveCoefficient('x', 1);
engine.setObjectiveCoefficient('y', 1);
engine.setMaximization();

const solution = engine.solve();
if (!solution.isValid()) {
  Logger.log(`No solution ${solution.getStatus()}`);
} else {
  Logger.log(`Value of x: ${solution.getVariableValue('x')}`);
  Logger.log(`Value of y: ${solution.getVariableValue('y')}`);
}
```

## Properties

| Property | Type | Description |
|---|---|---|
| Status | [Status](Status.md) | An enum representing the status of the solution to a linear program. |
| VariableType | [VariableType](VariableType.md) | An enum representing the type of variables created by the engine. |
