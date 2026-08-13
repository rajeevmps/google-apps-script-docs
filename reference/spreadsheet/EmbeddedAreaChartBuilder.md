# EmbeddedAreaChartBuilder

Builder for area charts.

Builder for area charts. For more details, see the Gviz documentation (http://code.google.com/apis/visualization/documentation/gallery/areachart.html).

## Methods

| Method | Return Type | Description |
|---|---|---|
| `addRange(range: Range)` | `EmbeddedChartBuilder` | Adds a range to the chart this builder modifies. Does not add the range if it has already been added to the chart. |
| `asAreaChart()` | `EmbeddedAreaChartBuilder` | Sets the chart type to AreaChart and returns an EmbeddedAreaChartBuilder. |
| `asBarChart()` | `EmbeddedBarChartBuilder` | Sets the chart type to BarChart and returns an EmbeddedBarChartBuilder. |
| `asColumnChart()` | `EmbeddedColumnChartBuilder` | Sets the chart type to ColumnChart and returns an EmbeddedColumnChartBuilder. |
| `asComboChart()` | `EmbeddedComboChartBuilder` | Sets the chart type to ComboChart and returns an EmbeddedComboChartBuilder. |
| `asHistogramChart()` | `EmbeddedHistogramChartBuilder` | Sets the chart type to HistogramChart and returns an EmbeddedHistogramChartBuilder. |
| `asLineChart()` | `EmbeddedLineChartBuilder` | Sets the chart type to LineChart and returns an EmbeddedLineChartBuilder. |
| `asPieChart()` | `EmbeddedPieChartBuilder` | Sets the chart type to PieChart and returns an EmbeddedPieChartBuilder. |
| `asScatterChart()` | `EmbeddedScatterChartBuilder` | Sets the chart type to ScatterChart and returns an EmbeddedScatterChartBuilder. |
| `asTableChart()` | `EmbeddedTableChartBuilder` | Sets the chart type to TableChart and returns an EmbeddedTableChartBuilder. |
| `build()` | `EmbeddedChart` | Builds the chart to reflect all changes made to it. This method does not automatically draw the chart on top of the spreadsheet. A new chart must be inserted via `sheet.insertChart(chart)`, and an existing chart should be updated via `sheet.updateChart(chart)`. |
| `clearRanges()` | `EmbeddedChartBuilder` | Removes all ranges from the chart this builder modifies. |
| `getChartType()` | `ChartType` | Returns the current chart type. |
| `getContainer()` | `ContainerInfo` | Return the chart ContainerInfo, which encapsulates where the chart appears on the sheet. |
| `getRanges()` | `Range[]` | Returns a copy of the list of ranges currently providing data for this chart. Use addRange(range) and removeRange(range) to modify this list. |
| `removeRange(range: Range)` | `EmbeddedChartBuilder` | Removes the specified range from the chart this builder modifies. Does not throw an error if the range is not in this chart. |
| `reverseCategories()` | `EmbeddedAreaChartBuilder` | Reverses the drawing of series in the domain axis. For vertical-range charts (such as line, area or column charts), this means the horizontal axis is drawn from right to left. For horizontal-range charts (such as bar charts), this means the vertical axis is drawn from top to bottom. For pie charts, this means the slices are drawn counterclockwise. |
| `setBackgroundColor(cssValue: String)` | `EmbeddedAreaChartBuilder` | Sets the background color for the chart. `cssValue` is the CSS value for the color (such as "blue" or "#00f"). |
| `setChartType(type: ChartType)` | `EmbeddedChartBuilder` | Changes the type of chart. Not all embedded chart types are currently supported. |
| `setColors(cssValues: String[])` | `EmbeddedAreaChartBuilder` | Sets the colors for the lines in the chart. `cssValues` is an array of color CSS values, such as ["red", "#acf"]. The nth element in the array represents the color of the nth line in the chart. |
| `setHiddenDimensionStrategy(strategy: ChartHiddenDimensionStrategy)` | `EmbeddedChartBuilder` | Sets the strategy to use for hidden rows and columns. Defaults to IGNORE_ROWS. |
| `setLegendPosition(position: ChartLegendPosition)` | `EmbeddedAreaChartBuilder` | Sets the position of the legend with respect to the chart. By default, there is no legend. |
| `setLegendTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the text style of the chart legend. |
| `setMergeStrategy(mergeStrategy: ChartMergeStrategy)` | `EmbeddedChartBuilder` | Sets the merge strategy to use when more than one range exists. Defaults to MERGE_COLUMNS. |
| `setNumHeaders(headers: Integer)` | `EmbeddedChartBuilder` | Sets the number of rows or columns of the range that should be treated as headers. |
| `setOption(option: String, value: Object)` | `EmbeddedChartBuilder` | Sets advanced options for this chart. |
| `setPointStyle(style: PointStyle)` | `EmbeddedAreaChartBuilder` | Sets the style for points in the line. |
| `setPosition(anchorRowPos: Integer, anchorColPos: Integer, offsetX: Integer, offsetY: Integer)` | `EmbeddedChartBuilder` | Sets the position, changing where the chart appears on the sheet. |
| `setRange(start: Number, end: Number)` | `EmbeddedAreaChartBuilder` | Sets the range for the chart. |
| `setStacked()` | `EmbeddedAreaChartBuilder` | Uses stacked lines, meaning that line and bar values are stacked (accumulated). |
| `setTitle(chartTitle: String)` | `EmbeddedAreaChartBuilder` | Sets the title of the chart. |
| `setTitleTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the text style of the chart title. |
| `setTransposeRowsAndColumns(transpose: Boolean)` | `EmbeddedChartBuilder` | Sets whether the chart's rows and columns are transposed. |
| `setXAxisTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the horizontal axis text style. |
| `setXAxisTitle(title: String)` | `EmbeddedAreaChartBuilder` | Adds a title to the horizontal axis. |
| `setXAxisTitleTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the horizontal axis title text style. |
| `setYAxisTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the vertical axis text style. |
| `setYAxisTitle(title: String)` | `EmbeddedAreaChartBuilder` | Adds a title to the vertical axis. |
| `setYAxisTitleTextStyle(textStyle: TextStyle)` | `EmbeddedAreaChartBuilder` | Sets the vertical axis title text style. |
| `useLogScale()` | `EmbeddedAreaChartBuilder` | Makes the range axis into a logarithmic scale (requires all values to be positive). |
