# Status

Status of the solution.

Status of the solution. Before solving a problem the status will be `NOT_SOLVED`; afterwards it will take any of the other values depending if it successfully found a solution and if the solution is optimal.

## Methods

None.

## Properties

| Property | Type | Description |
|---|---|---|
| OPTIMAL | Enum | Status when an optimal solution has been found. |
| FEASIBLE | Enum | Status when a feasible (not necessarily optimal) solution has been found. |
| INFEASIBLE | Enum | Status when the current model is unfeasible (has no solution). |
| UNBOUNDED | Enum | Status when the current model is unbound. |
| ABNORMAL | Enum | Status when it failed to find a solution for unexpected reasons. |
| MODEL_INVALID | Enum | Status when the model is invalid. |
| NOT_SOLVED | Enum | Status when `LinearOptimizationEngine.solve()` has not been called yet. |
