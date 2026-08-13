# LinearOptimizationEngine

The engine used to model and solve a linear program.

The engine used to model and solve a linear program. It enables users to define variables with specified bounds and types, add constraints with defined bounds, set objective function coefficients, and determine optimization direction (maximization or minimization) before solving.

## Methods

### addConstraint(lowerBound, upperBound)

Returns: `LinearOptimizationConstraint`

Adds a new linear constraint in the model. The upper and lower bound of the constraint are defined at creation time. Coefficients for the variables are defined via calls to `LinearOptimizationConstraint.setCoefficient(variableName, coefficient)`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| lowerBound | Number | lower bound of the constraint |
| upperBound | Number | upper bound of the constraint |

### addConstraints(lowerBounds, upperBounds, variableNames, coefficients)

Returns: `LinearOptimizationEngine`

Adds constraints in batch to the model.

**Parameters**

| Name | Type | Description |
|---|---|---|
| lowerBounds | Number[] | lower bounds of the constraints |
| upperBounds | Number[] | upper bounds of the constraints |
| variableNames | String[][] | variable names referenced by each constraint |
| coefficients | Number[][] | coefficients for the variables referenced by each constraint |

### addVariable(name, lowerBound, upperBound)

Returns: `LinearOptimizationEngine`

Adds a new continuous variable to the model. The variable is referenced by its name. The type is set to `VariableType.CONTINUOUS`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| name | String | the name of the variable |
| lowerBound | Number | lower bound of the variable |
| upperBound | Number | upper bound of the variable |

### addVariable(name, lowerBound, upperBound, type)

Returns: `LinearOptimizationEngine`

Adds a new variable to the model. The variable is referenced by its name.

**Parameters**

| Name | Type | Description |
|---|---|---|
| name | String | the name of the variable |
| lowerBound | Number | lower bound of the variable |
| upperBound | Number | upper bound of the variable |
| type | VariableType | the type of the variable |

### addVariable(name, lowerBound, upperBound, type, objectiveCoefficient)

Returns: `LinearOptimizationEngine`

Adds a new variable to the model. The variable is referenced by its name.

**Parameters**

| Name | Type | Description |
|---|---|---|
| name | String | the name of the variable |
| lowerBound | Number | lower bound of the variable |
| upperBound | Number | upper bound of the variable |
| type | VariableType | the type of the variable |
| objectiveCoefficient | Number | the coefficient of the variable in the objective function |

### addVariables(names, lowerBounds, upperBounds, types, objectiveCoefficients)

Returns: `LinearOptimizationEngine`

Adds variables in batch to the model. The variables are referenced by their names.

**Parameters**

| Name | Type | Description |
|---|---|---|
| names | String[] | the names of the variables |
| lowerBounds | Number[] | lower bounds of the variables |
| upperBounds | Number[] | upper bounds of the variables |
| types | VariableType[] | the types of the variables |
| objectiveCoefficients | Number[] | the coefficients of the variables in the objective function |

### setMaximization()

Returns: `LinearOptimizationEngine`

Sets the optimization direction to maximizing the linear objective function.

### setMinimization()

Returns: `LinearOptimizationEngine`

Sets the optimization direction to minimizing the linear objective function.

### setObjectiveCoefficient(variableName, coefficient)

Returns: `LinearOptimizationEngine`

Sets the coefficient of a variable in the linear objective function.

**Parameters**

| Name | Type | Description |
|---|---|---|
| variableName | String | the name of the variable for which the coefficient is being set |
| coefficient | Number | coefficient being set |

### solve()

Returns: `LinearOptimizationSolution`

Solves the current linear program with the default deadline of 30 seconds. Returns the solution found.

### solve(seconds)

Returns: `LinearOptimizationSolution`

Solves the current linear program. Returns the solution found, and if it is an optimal solution. Maximum deadline is 300 seconds.

**Parameters**

| Name | Type | Description |
|---|---|---|
| seconds | Number | maximum amount of time allotted to solve the problem, in seconds |

## Properties

None.
