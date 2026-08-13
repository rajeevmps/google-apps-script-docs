# TableChartBuilder

A builder for table charts.

A builder for table charts. For more details, see the Google Charts documentation. The class enables creation of table charts with data imported from external sources like Google spreadsheets. Various aspects can be configured including dimensions, paging, sorting, and data sources.

## Methods

### build()

Returns: `Chart`

Builds the chart and returns a Chart object that can be embedded into documents or UI elements.

### enablePaging(enablePaging)

Returns: `TableChartBuilder`

Sets whether to enable paging through the data. The default behavior is paging disabled. If paging is enabled the default page size is 10.

**Parameters**

| Name | Type | Description |
|---|---|---|
| enablePaging | Boolean | `true` to enable paging. |

### enablePaging(pageSize)

Returns: `TableChartBuilder`

Enables paging and sets the number of rows in each page. The default page size is 10.

**Parameters**

| Name | Type | Description |
|---|---|---|
| pageSize | Integer | The number of rows in each page. |

### enablePaging(pageSize, startPage)

Returns: `TableChartBuilder`

Enables paging, sets the number of rows in each page and the first table page to display (page numbers are zero based).

**Parameters**

| Name | Type | Description |
|---|---|---|
| pageSize | Integer | The number of rows in each page. |
| startPage | Integer | The first table page to display (page numbers are zero-based). |

### enableRtlTable(rtlEnabled)

Returns: `TableChartBuilder`

Adds basic support for right-to-left languages (such as Arabic or Hebrew) by reversing the column order of the table.

**Parameters**

| Name | Type | Description |
|---|---|---|
| rtlEnabled | Boolean | `true` to support right-to-left languages. |

### enableSorting(enableSorting)

Returns: `TableChartBuilder`

Sets whether to sort columns when the user clicks a column heading.

**Parameters**

| Name | Type | Description |
|---|---|---|
| enableSorting | Boolean | `true` to enable sorting. |

### setDataSourceUrl(url)

Returns: `TableChartBuilder`

Sets the data source URL that is used to pull data in from an external source, such as Google Sheets.

**Parameters**

| Name | Type | Description |
|---|---|---|
| url | String | The data source URL. |

### setDataTable(tableBuilder)

Returns: `TableChartBuilder`

Sets the data table to use for the chart using a DataTableBuilder. This is a convenience method for setting the data table without needing to call `build()`.

**Parameters**

| Name | Type | Description |
|---|---|---|
| tableBuilder | DataTableBuilder | A data table builder. |

### setDataTable(table)

Returns: `TableChartBuilder`

Sets the data table which contains the lines for the chart, as well as the X-axis labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| table | DataTableSource | The data table to use for the chart. |

### setDataViewDefinition(dataViewDefinition)

Returns: `TableChartBuilder`

Sets the data view definition to use for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| dataViewDefinition | DataViewDefinition | The data view definition to use. |

### setDimensions(width, height)

Returns: `TableChartBuilder`

Sets the dimensions for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| width | Integer | The width of the chart, in pixels. |
| height | Integer | The height of the chart, in pixels. |

### setFirstRowNumber(number)

Returns: `TableChartBuilder`

Sets the row number for the first row in the data table. The default row number of the first row is 1.

**Parameters**

| Name | Type | Description |
|---|---|---|
| number | Integer | The row number for the first row. |

### setInitialSortingAscending(column)

Returns: `TableChartBuilder`

Sets the index of the column according to which the table should be initially sorted (ascending).

**Parameters**

| Name | Type | Description |
|---|---|---|
| column | Integer | The index of the column according to which to sort. |

### setInitialSortingDescending(column)

Returns: `TableChartBuilder`

Sets the index of the column according to which the table should be initially sorted (descending).

**Parameters**

| Name | Type | Description |
|---|---|---|
| column | Integer | The index of the column according to which to sort. |

### setOption(option, value)

Returns: `TableChartBuilder`

Sets advanced options for this chart. See the available options for this chart. This method has no effect if the given option is invalid.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The name of the option. |
| value | Object | The value of the option. |

### showRowNumberColumn(showRowNumber)

Returns: `TableChartBuilder`

Sets whether to show the row number as the first column of the table.

**Parameters**

| Name | Type | Description |
|---|---|---|
| showRowNumber | Boolean | `true` to show the row number column. |

### useAlternatingRowStyle(alternate)

Returns: `TableChartBuilder`

Sets whether alternating color style is assigned to odd and even rows of a table chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| alternate | Boolean | `true` to use alternating row style. |

## Properties

None.
