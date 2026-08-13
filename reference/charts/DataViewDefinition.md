# DataViewDefinition

A data view definition for visualizing chart data.

A data view definition for visualizing chart data. Data view definition can be set for charts to visualize a view derived from the given data table and not the data table itself. When a view definition is applied to a chart, only the specified columns from the data table are used during rendering. For instance, if column indices are set to `[0, 3]`, only the first and third columns display. Use `DataViewDefinitionBuilder` (via `Charts.newDataViewDefinition()`) to construct instances of this class.

## Methods

None. This class has no methods of its own — instances are constructed via `DataViewDefinitionBuilder` and passed to chart builders' `setDataViewDefinition()` method.

## Properties

None.
