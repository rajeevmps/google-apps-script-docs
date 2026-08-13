# EmbeddedPieChartBuilder

Builder for pie charts.

Builder for pie charts. For more details, see the Gviz documentation. The EmbeddedPieChartBuilder is specifically designed for creating and customizing pie charts within Google Sheets. It enables developers to add or remove data ranges, modify visual appearance, and convert to other chart types.

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
| `build()` | `EmbeddedChart` | Builds the chart to reflect all changes made to it. This method does not automatically draw the chart on top of the spreadsheet. |
| `clearRanges()` | `EmbeddedChartBuilder` | Removes all ranges from the chart this builder modifies. |
| `getChartType()` | `ChartType` | Returns the current chart type. |
| `getContainer()` | `ContainerInfo` | Return the chart ContainerInfo, which encapsulates where the chart appears on the sheet. |
| `getRanges()` | `Range[]` | Returns a copy of the list of ranges currently providing data for this chart. |
| `removeRange(range: Range)` | `EmbeddedChartBuilder` | Removes the specified range from the chart this builder modifies. |
| `reverseCategories()` | `EmbeddedPieChartBuilder` | Reverses the drawing of series in the domain axis. For pie charts, this means slices are drawn counterclockwise. |
| `set3D()` | `EmbeddedPieChartBuilder` | Sets the chart to be three-dimensional. |
| `setBackgroundColor(cssValue: String)` | `EmbeddedPieChartBuilder` | Sets the background color for the chart. |
| `setChartType(type: ChartType)` | `EmbeddedChartBuilder` | Changes the type of chart. Not all embedded chart types are currently supported. |
| `setColors(cssValues: String[])` | `EmbeddedPieChartBuilder` | Sets the colors for the lines in the chart. |
| `setHiddenDimensionStrategy(strategy: ChartHiddenDimensionStrategy)` | `EmbeddedChartBuilder` | Sets the strategy to use for hidden rows and columns. Defaults to IGNORE_ROWS. |
| `setLegendPosition(position: ChartLegendPosition)` | `EmbeddedPieChartBuilder` | Sets the position of the legend with respect to the chart. By default, there is no legend. |
| `setLegendTextStyle(textStyle: TextStyle)` | `EmbeddedPieChartBuilder` | Sets the text style of the chart legend. |
| `setMergeStrategy(mergeStrategy: ChartMergeStrategy)` | `EmbeddedChartBuilder` | Sets the merge strategy when multiple ranges exist. Defaults to MERGE_COLUMNS. |
| `setNumHeaders(headers: Integer)` | `EmbeddedChartBuilder` | Sets the number of rows or columns of the range that should be treated as headers. |
| `setOption(option: String, value: Object)` | `EmbeddedChartBuilder` | Sets advanced options for this chart. See chart configuration options documentation. |
| `setPosition(anchorRowPos: Integer, anchorColPos: Integer, offsetX: Integer, offsetY: Integer)` | `EmbeddedChartBuilder` | Sets the position, changing where the chart appears on the sheet. |
| `setTitle(chartTitle: String)` | `EmbeddedPieChartBuilder` | Sets the title of the chart. |
| `setTitleTextStyle(textStyle: TextStyle)` | `EmbeddedPieChartBuilder` | Sets the text style of the chart title. |
| `setTransposeRowsAndColumns(transpose: Boolean)` | `EmbeddedChartBuilder` | Sets whether the chart's rows and columns are transposed. |
