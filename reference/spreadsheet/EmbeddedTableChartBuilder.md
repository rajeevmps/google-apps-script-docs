# EmbeddedTableChartBuilder

Builder for table charts.

Builder for table charts. For more details, see the Gviz documentation (http://developers.google.com/chart/interactive/docs/gallery/table.html).

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
| `build()` | `EmbeddedChart` | Builds the chart to reflect all changes made to it. This method does not automatically draw the chart on top of the spreadsheet. A new chart must be inserted via sheet.insertChart(chart), and an existing chart should be updated via sheet.updateChart(chart). |
| `clearRanges()` | `EmbeddedChartBuilder` | Removes all ranges from the chart this builder modifies. |
| `enablePaging(enablePaging: Boolean)` | `EmbeddedTableChartBuilder` | Sets whether to enable paging through the data. The default behavior is paging disabled. If paging is enabled the default page size is 10. |
| `enablePaging(pageSize: Integer)` | `EmbeddedTableChartBuilder` | Enables paging and sets the number of rows in each page. The default page size is 10. |
| `enablePaging(pageSize: Integer, startPage: Integer)` | `EmbeddedTableChartBuilder` | Enables paging, sets the number of rows in each page and the first table page to display (page numbers are zero based). The default page size is 10, and the default start page is 0. |
| `enableRtlTable(rtlEnabled: Boolean)` | `EmbeddedTableChartBuilder` | Adds basic support for right-to-left languages (such as Arabic or Hebrew) by reversing the column order of the table, so that column zero is the right-most column, and the last column is the left-most column. This does not affect the column index in the underlying data, only the order of display. Full bi-directional (BiDi) language display is not supported by the table visualization even with this option. This option is ignored if you enable paging (using the page option), or if the table has scroll bars because you have specified height and width options smaller than the required table size. The default behavior is RTL support disabled. |
| `enableSorting(enableSorting: Boolean)` | `EmbeddedTableChartBuilder` | Sets whether to sort columns when the user clicks a column heading. If sorting is enabled, when users click on the column header the rows are automatically sorted. The default behavior is sorting enabled. |
| `getChartType()` | `ChartType` | Returns the current chart type. |
| `getContainer()` | `ContainerInfo` | Return the chart ContainerInfo, which encapsulates where the chart appears on the sheet. |
| `getRanges()` | `Range[]` | Returns a copy of the list of ranges currently providing data for this chart. Use addRange(range) and removeRange(range) to modify this list. |
| `removeRange(range: Range)` | `EmbeddedChartBuilder` | Removes the specified range from the chart this builder modifies. Does not throw an error if the range is not in this chart. The range removed must match up with a range added via addRange(range); otherwise no change is made to the chart. This method cannot be used to partially remove values from a range. |
| `setChartType(type: ChartType)` | `EmbeddedChartBuilder` | Changes the type of chart. Not all embedded chart types are currently supported. See ChartType. |
| `setFirstRowNumber(number: Integer)` | `EmbeddedTableChartBuilder` | Sets the row number for the first row in the data table. The default row number of the first row is 1. |
| `setHiddenDimensionStrategy(strategy: ChartHiddenDimensionStrategy)` | `EmbeddedChartBuilder` | Sets the strategy to use for hidden rows and columns. Defaults to IGNORE_ROWS. |
| `setInitialSortingAscending(column: Integer)` | `EmbeddedTableChartBuilder` | Sets the index of the column according to which the table should be initially sorted (ascending). The column os sorted in ascending order and is marked with a small arrow indicating that. |
| `setInitialSortingDescending(column: Integer)` | `EmbeddedTableChartBuilder` | Sets the index of the column according to which the table should be initially sorted (descending). The column os sorted in descending order and is marked with a small arrow indicating that. |
| `setMergeStrategy(mergeStrategy: ChartMergeStrategy)` | `EmbeddedChartBuilder` | Sets the merge strategy to use when more than one range exists. If MERGE_ROWS, rows are merged; if MERGE_COLUMNS, columns are merged. Defaults to MERGE_COLUMNS. |
| `setNumHeaders(headers: Integer)` | `EmbeddedChartBuilder` | Sets the number of rows or columns of the range that should be treated as headers. |
| `setOption(option: String, value: Object)` | `EmbeddedChartBuilder` | Sets advanced options for this chart. |
| `setPosition(anchorRowPos: Integer, anchorColPos: Integer, offsetX: Integer, offsetY: Integer)` | `EmbeddedChartBuilder` | Sets the position, changing where the chart appears on the sheet. |
| `setTransposeRowsAndColumns(transpose: Boolean)` | `EmbeddedChartBuilder` | Sets whether the chart's rows and columns are transposed. |
| `showRowNumberColumn(showRowNumber: Boolean)` | `EmbeddedTableChartBuilder` | Sets whether to show the row number as the first column of the table. |
| `useAlternatingRowStyle(alternate: Boolean)` | `EmbeddedTableChartBuilder` | Sets whether alternating color style is assigned to odd and even rows of a table chart. |
