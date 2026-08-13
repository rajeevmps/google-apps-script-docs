# DataTableBuilder

Builder of DataTable objects.

Builder of DataTable objects. Building a data table consists of first specifying its columns, and then adding its rows, one at a time.

## Methods

### addColumn(type, label)

Returns: `DataTableBuilder`

Adds a column to the data table. Columns will be added from 0 to n. The first column is often used by charts for labels (for instance, X-axis labels on line charts, or slice labels in pie charts). The other columns are often used for data and therefore often require numeric values.

**Parameters**

| Name | Type | Description |
|---|---|---|
| type | ColumnType | type of data in the column (number, string, or date) |
| label | String | label of the column (it's used for chart legends) |

### addRow(values)

Returns: `DataTableBuilder`

Adds a row to the data table.

**Parameters**

| Name | Type | Description |
|---|---|---|
| values | Object[] | values for the row, specified in the same order that the columns are entered |

### build()

Returns: `DataTable`

Builds and returns a data table. Throws an Error if the data table is empty or otherwise malformed.

### setValue(row, column, value)

Returns: `DataTableBuilder`

Sets a specific value in the table. You may set a value before adding the column to the data table. However, unless the column is added at some point, the value will be ignored. Not all column values need to be filled in. Those missing will be considered null.

**Parameters**

| Name | Type | Description |
|---|---|---|
| row | Integer | the row index (the first row has index 0) |
| column | Integer | the column index (the first column has index 0) |
| value | Object | the value of the table cell (should have the right type for the column) |

## Properties

None.
