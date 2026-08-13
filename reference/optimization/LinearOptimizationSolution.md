# LinearOptimizationSolution

A LinearOptimizationSolution represents the solution of a linear program.

A `LinearOptimizationSolution` represents the solution of a linear program. The solution provides methods to get the objective value, the value of specific variables, the status of the solution, and to check its validity.

## Methods

### getObjectiveValue()

Returns: `Number`

Gets the value of the objective function in the current solution.

### getStatus()

Returns: `Status`

Gets the status of the solution. Before solving a problem, the status will be `NOT_SOLVED`.

### getVariableValue(variableName)

Returns: `Number`

Gets the value of a variable in the solution created by the last call to `LinearOptimizationEngine.solve()`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| variableName | String | the name of the variable |

### isValid()

Returns: `Boolean`

Determines whether the solution is either feasible or optimal. Returns `true` if the solution is valid (`Status.FEASIBLE` or `Status.OPTIMAL`); `false` if not.

## Properties

None.
