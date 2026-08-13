# ScatterChartBuilder

Builder for scatter charts.

Builder for scatter charts. For more details, see the Google Charts documentation.

## Methods

### build()

Returns: `Chart`

Builds the chart. Returns a Chart object that can be embedded into documents, UI elements, or used as a static image.

### setBackgroundColor(cssValue)

Returns: `ScatterChartBuilder`

Sets the background color for the chart. Accepts CSS color values like "blue" or "#00f".

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValue | String | The CSS value for the background color. |

### setColors(cssValues)

Returns: `ScatterChartBuilder`

Sets the colors for the lines in the chart. Takes an array of CSS color values where the nth element represents the nth line's color.

**Parameters**

| Name | Type | Description |
|---|---|---|
| cssValues | String[] | An array of colors to use for the chart lines. |

### setDataSourceUrl(url)

Returns: `ScatterChartBuilder`

Sets the data source URL that is used to pull data in from an external source, such as Google Sheets. Data source URL is ignored if a DataTable is also provided.

**Parameters**

| Name | Type | Description |
|---|---|---|
| url | String | The data source URL. |

### setDataTable(tableBuilder)

Returns: `ScatterChartBuilder`

Sets the data table to use for the chart using a DataTableBuilder. A convenience method creating a data table instantly.

**Parameters**

| Name | Type | Description |
|---|---|---|
| tableBuilder | DataTableBuilder | A data table builder. |

### setDataTable(table)

Returns: `ScatterChartBuilder`

Sets the data table which contains the lines for the chart, as well as the X-axis labels. First column should be string; subsequent columns must be numeric.

**Parameters**

| Name | Type | Description |
|---|---|---|
| table | DataTableSource | The data table to use for the chart. |

### setDataViewDefinition(dataViewDefinition)

Returns: `ScatterChartBuilder`

Sets the data view definition to use for the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| dataViewDefinition | DataViewDefinition | The data view definition to use. |

### setDimensions(width, height)

Returns: `ScatterChartBuilder`

Sets the dimensions for the chart. Width and height specified in pixels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| width | Integer | The width of the chart, in pixels. |
| height | Integer | The height of the chart, in pixels. |

### setLegendPosition(position)

Returns: `ScatterChartBuilder`

Sets the position of the legend with respect to the chart. By default, no legend appears.

**Parameters**

| Name | Type | Description |
|---|---|---|
| position | Position | The position of the legend. |

### setLegendTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the text style of the chart legend.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart legend. |

### setOption(option, value)

Returns: `ScatterChartBuilder`

Sets advanced options for this chart. See available scatter chart options in the Google Charts documentation.

**Parameters**

| Name | Type | Description |
|---|---|---|
| option | String | The name of the option. |
| value | Object | The value of the option. |

### setPointStyle(style)

Returns: `ScatterChartBuilder`

Sets the style for points in the line. By default, points have no particular styles.

**Parameters**

| Name | Type | Description |
|---|---|---|
| style | PointStyle | The style to use for points in the line. |

### setTitle(chartTitle)

Returns: `ScatterChartBuilder`

Sets the title of the chart. Title displays centered above the chart.

**Parameters**

| Name | Type | Description |
|---|---|---|
| chartTitle | String | The title of the chart. |

### setTitleTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the text style of the chart title.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the chart title. |

### setXAxisLogScale()

Returns: `ScatterChartBuilder`

Makes the horizontal axis into a logarithmic scale (requires all values to be positive).

### setXAxisRange(start, end)

Returns: `ScatterChartBuilder`

Sets the range for the horizontal axis of the chart. Range expands automatically if data points fall outside it.

**Parameters**

| Name | Type | Description |
|---|---|---|
| start | Number | The value for the lowest grid line of the horizontal axis. |
| end | Number | The value for the highest grid line of the horizontal axis. |

### setXAxisTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the horizontal axis text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the horizontal axis title. |

### setXAxisTitle(title)

Returns: `ScatterChartBuilder`

Adds a title to the horizontal axis. Title is centered and appears below axis value labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| title | String | The title for the X-axis. |

### setXAxisTitleTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the horizontal axis title text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the horizontal axis title. |

### setYAxisLogScale()

Returns: `ScatterChartBuilder`

Makes the vertical axis into a logarithmic scale (requires all values to be positive).

### setYAxisRange(start, end)

Returns: `ScatterChartBuilder`

Sets the range for the vertical axis of the chart. Range expands if data points fall outside.

**Parameters**

| Name | Type | Description |
|---|---|---|
| start | Number | The value for the lowest grid line of the vertical axis. |
| end | Number | The value for the highest grid line of the vertical axis. |

### setYAxisTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the vertical axis text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the vertical axis title. |

### setYAxisTitle(title)

Returns: `ScatterChartBuilder`

Adds a title to the vertical axis. Title is centered, appearing left of value labels.

**Parameters**

| Name | Type | Description |
|---|---|---|
| title | String | The title for the Y-axis. |

### setYAxisTitleTextStyle(textStyle)

Returns: `ScatterChartBuilder`

Sets the vertical axis title text style.

**Parameters**

| Name | Type | Description |
|---|---|---|
| textStyle | TextStyle | The text style to use for the vertical axis title. |

## Properties

None.
