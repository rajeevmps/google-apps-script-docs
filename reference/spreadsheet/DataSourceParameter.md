# DataSourceParameter

Access existing data source parameters.

Access existing data source parameters. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getName()` | `String` | Gets the parameter name. Returns the name assigned to the data source parameter. |
| `getSourceCell()` | `String\|null` | Gets the source cell the parameter is valued based on, or `null` if the parameter type is not `DataSourceParameterType.CELL`. Retrieves the cell reference in A1 notation that provides the parameter value, or returns null when the parameter type is not CELL-based. |
| `getType()` | `DataSourceParameterType` | Gets the parameter type. Returns the parameter type using the `DataSourceParameterType` enumeration. |
