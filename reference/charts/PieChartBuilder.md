# PieChartBuilder

A builder for pie charts.

A builder for pie charts. For more details, see the Google Charts documentation. The class provides methods to create and customize pie charts, including options for three-dimensional rendering, data source configuration, styling, and legend positioning.

## Methods

### build()

Returns: `Chart`

Builds the chart and returns a Chart object that can be embedded into documents, UI elements, or used as a static image.

### reverseCategories()

Returns: `PieChartBuilder`

Reverses the drawing of series in the domain axis. For pie charts, this draws slices counterclockwise.

### set3D()

Returns: `PieChartBuilder`

Sets the chart to be three-dimensional.

### setBackgroundColor(cssValue)

Returns: `PieChartBuilder`

Sets the background color for the chart, using CSS color values like "blue" or "#00f".

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValue | String | The CSS value for the background color. |

### setColors(cssValues)

Returns: `PieChartBuilder`

Sets the colors for the lines in the chart. The nth array element represents the nth line's color.

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValues | String[] | An array of colors to use for the chart lines. |

### setDataSourceUrl(url)

Returns: `PieChartBuilder`

Sets the data source URL that is used to pull data in from an external source, such as Google Sheets.

**Parameters**

| Name | Type | Description |
|---|---|---|
| url | String | The data source URL. |

### setDataTable(tableBuilder)

Returns: `PieChartBuilder`

Sets the data table to use for the chart using a DataTableBuilder, without needing to call build().

**Parameters**

| Name | Type | Description |
|---|---|---|
| tableBuilder | DataTableBuilder | A data table builder. |

### setDataTable(table)

Returns: `PieChartBuilder`

Sets the data table which contains the lines for the chart, as well as the X-axis labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| table | DataTableSource | The data table to use for the chart. |

### setDataViewDefinition(dataViewDefinition)

Returns: `PieChartBuilder`

Sets the data view definition to use for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| dataViewDefinition | DataViewDefinition | The data view definition to use. |

### setDimensions(width, height)

Returns: `PieChartBuilder`

Sets the dimensions for the chart, in pixels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| width | Integer | The width of the chart, in pixels. |
| height | Integer | The height of the chart, in pixels. |

### setLegendPosition(position)

Returns: `PieChartBuilder`

Sets the position of the legend with respect to the chart. By default, there is no legend.

**Parameters**

| Name | Type | Description |
|---|---|---|
| position | Position | The position of the legend. |

### setLegendTextStyle(textStyle)

Returns: `PieChartBuilder`

Sets the text style of the chart legend.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart legend. |

### setOption(option, value)

Returns: `PieChartBuilder`

Sets advanced options for this chart from available Google Charts options.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The name of the option. |
| value | Object | The value of the option. |

### setTitle(chartTitle)

Returns: `PieChartBuilder`

Sets the title of the chart. The title is displayed centered above the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| chartTitle | String | The title of the chart. |

### setTitleTextStyle(textStyle)

Returns: `PieChartBuilder`

Sets the text style of the chart title.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart title. |

## Properties

None.
