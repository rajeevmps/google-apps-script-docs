# LineChartBuilder

Builder for line charts.

Builder for line charts. For more details, see the Google Charts documentation.

## Methods

### build()

Returns: `Chart`

Builds the chart.

### reverseCategories()

Returns: `LineChartBuilder`

Reverses the drawing of series in the domain axis. For vertical-range charts (such as line, area or column charts), this means the horizontal axis is drawn from right to left.

### setBackgroundColor(cssValue)

Returns: `LineChartBuilder`

Sets the background color for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValue | String | The CSS value for the background color. |

### setColors(cssValues)

Returns: `LineChartBuilder`

Sets the colors for the lines in the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValues | String[] | An array of colors to use for the chart lines. |

### setCurveStyle(style)

Returns: `LineChartBuilder`

Sets the style to use for curves in the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| style | CurveStyle | The style for the curve. |

### setDataSourceUrl(url)

Returns: `LineChartBuilder`

Sets the data source URL that is used to pull data in from an external source, such as Google Sheets.

**Parameters**

| Name | Type | Description |
|---|---|---|
| url | String | The data source URL. |

### setDataTable(tableBuilder)

Returns: `LineChartBuilder`

Sets the data table to use for the chart using a DataTableBuilder. This is a convenience method for setting the data table without needing to call build().

**Parameters**

| Name | Type | Description |
|---|---|---|
| tableBuilder | DataTableBuilder | A data table builder. |

### setDataTable(table)

Returns: `LineChartBuilder`

Sets the data table which contains the lines for the chart, as well as the X-axis labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| table | DataTableSource | The data table to use for the chart. |

### setDataViewDefinition(dataViewDefinition)

Returns: `LineChartBuilder`

Sets the data view definition to use for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| dataViewDefinition | DataViewDefinition | The data view definition to use. |

### setDimensions(width, height)

Returns: `LineChartBuilder`

Sets the dimensions for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| width | Integer | The width of the chart, in pixels. |
| height | Integer | The height of the chart, in pixels. |

### setLegendPosition(position)

Returns: `LineChartBuilder`

Sets the position of the legend with respect to the chart. By default, there is no legend.

**Parameters**

| Name | Type | Description |
|---|---|---|
| position | Position | The position of the legend. |

### setLegendTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the text style of the chart legend.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart legend. |

### setOption(option, value)

Returns: `LineChartBuilder`

Sets advanced options for this chart. This method has no effect if the given option is invalid.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The name of the option. |
| value | Object | The value of the option. |

### setPointStyle(style)

Returns: `LineChartBuilder`

Sets the style for points in the line. By default, points have no particular styles, and only the line is visible.

**Parameters**

| Name | Type | Description |
|---|---|---|
| style | PointStyle | The style to use for points in the line. |

### setRange(start, end)

Returns: `LineChartBuilder`

Sets the range for the chart. If any data points fall outside the range, the range is expanded to include those data points.

**Parameters**

| Name | Type | Description |
|---|---|---|
| start | Number | The value for the lowest grid line of the range axis. |
| end | Number | The value for the highest grid line of the range axis. |

### setTitle(chartTitle)

Returns: `LineChartBuilder`

Sets the title of the chart. The title is displayed centered above the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| chartTitle | String | The title of the chart. |

### setTitleTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the text style of the chart title.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart title. |

### setXAxisTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the horizontal axis text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the horizontal axis title. |

### setXAxisTitle(title)

Returns: `LineChartBuilder`

Adds a title to the horizontal axis. The title is centered and appears below the axis value labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| title | String | The title for the X-axis. |

### setXAxisTitleTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the horizontal axis title text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the horizontal axis title. |

### setYAxisTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the vertical axis text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the vertical axis title. |

### setYAxisTitle(title)

Returns: `LineChartBuilder`

Adds a title to the vertical axis. The title is centered and appears to the left of the value labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| title | String | The title for the Y-axis. |

### setYAxisTitleTextStyle(textStyle)

Returns: `LineChartBuilder`

Sets the vertical axis title text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the vertical axis title. |

### useLogScale()

Returns: `LineChartBuilder`

Makes the range axis into a logarithmic scale (requires all values to be positive).

## Properties

None.
