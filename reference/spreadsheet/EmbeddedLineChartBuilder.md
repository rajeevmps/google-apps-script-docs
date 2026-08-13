# EmbeddedLineChartBuilder

Builder for line charts.

Builder for line charts. For more details, see the Gviz documentation (http://code.google.com/apis/visualization/documentation/gallery/linechart.html). The EmbeddedLineChartBuilder serves as a specialized constructor for line charts within Google Visualization. It enables developers to configure data ranges, customize visual properties including colors and backgrounds, establish titles and text styling, and manipulate chart behavior through legend positioning, dimension handling, and scaling options. The resulting chart configuration must be explicitly inserted or updated within the spreadsheet via dedicated methods.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `addRange(range: Range)` | `EmbeddedChartBuilder` | Adds a range to the chart this builder modifies. Does not add the range if it has already been added to the chart. |
| `removeRange(range: Range)` | `EmbeddedChartBuilder` | Removes the specified range from the chart this builder modifies. Does not throw an error if the range is not in this chart. The range removed must match up with a range added via addRange(range); otherwise no change is made to the chart. |
| `clearRanges()` | `EmbeddedChartBuilder` | Removes all ranges from the chart this builder modifies. |
| `getRanges()` | `Range[]` | Returns a copy of the list of ranges currently providing data for this chart. Use addRange(range) and removeRange(range) to modify this list. |
| `setRange(start: Number, end: Number)` | `EmbeddedLineChartBuilder` | Sets the range for the chart. |
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
| `getChartType()` | `ChartType` | Returns the current chart type. |
| `setChartType(type: ChartType)` | `EmbeddedChartBuilder` | Changes the type of chart. Not all embedded chart types are currently supported. |
| `setBackgroundColor(cssValue: String)` | `EmbeddedLineChartBuilder` | Sets the background color for the chart. |
| `setColors(cssValues: String[])` | `EmbeddedLineChartBuilder` | Sets the colors for the lines in the chart. The nth element in the array represents the color of the nth line in the chart. |
| `setTitle(chartTitle: String)` | `EmbeddedLineChartBuilder` | Sets the title of the chart. |
| `setTitleTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the text style of the chart title. |
| `setXAxisTitle(title: String)` | `EmbeddedLineChartBuilder` | Adds a title to the horizontal axis. |
| `setXAxisTitleTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the horizontal axis title text style. |
| `setXAxisTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the horizontal axis text style. |
| `setYAxisTitle(title: String)` | `EmbeddedLineChartBuilder` | Adds a title to the vertical axis. |
| `setYAxisTitleTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the vertical axis title text style. |
| `setYAxisTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the vertical axis text style. |
| `setLegendPosition(position: Position)` | `EmbeddedLineChartBuilder` | Sets the position of the legend with respect to the chart. By default, there is no legend. |
| `setLegendTextStyle(textStyle: TextStyle)` | `EmbeddedLineChartBuilder` | Sets the text style of the chart legend. |
| `setCurveStyle(style: CurveStyle)` | `EmbeddedLineChartBuilder` | Sets the style to use for curves in the chart. |
| `setPointStyle(style: PointStyle)` | `EmbeddedLineChartBuilder` | Sets the style for points in the line. |
| `useLogScale()` | `EmbeddedLineChartBuilder` | Makes the range axis into a logarithmic scale (requires all values to be positive). |
| `reverseCategories()` | `EmbeddedLineChartBuilder` | Reverses the drawing of series in the domain axis. For vertical-range charts (such as line, area or column charts), this means the horizontal axis is drawn from right to left. |
| `setPosition(anchorRowPos: Integer, anchorColPos: Integer, offsetX: Integer, offsetY: Integer)` | `EmbeddedChartBuilder` | Sets the position, changing where the chart appears on the sheet. |
| `getContainer()` | `ContainerInfo` | Return the chart ContainerInfo, which encapsulates where the chart appears on the sheet. |
| `setHiddenDimensionStrategy(strategy: ChartHiddenDimensionStrategy)` | `EmbeddedChartBuilder` | Sets the strategy to use for hidden rows and columns. Defaults to IGNORE_ROWS. |
| `setMergeStrategy(mergeStrategy: ChartMergeStrategy)` | `EmbeddedChartBuilder` | Sets the merge strategy to use when more than one range exists. If MERGE_ROWS, rows are merged; if MERGE_COLUMNS, columns are merged. Defaults to MERGE_COLUMNS. |
| `setNumHeaders(headers: Integer)` | `EmbeddedChartBuilder` | Sets the number of rows or columns of the range that should be treated as headers. |
| `setTransposeRowsAndColumns(transpose: Boolean)` | `EmbeddedChartBuilder` | Sets whether the chart's rows and columns are transposed. |
| `setOption(option: String, value: Object)` | `EmbeddedChartBuilder` | Sets advanced options for this chart. |

## Code Samples

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const chart = sheet.newChart()
                  .setChartType(Charts.ChartType.BAR)
                  .addRange(sheet.getRange('A1:B8'))
                  .setPosition(5, 5, 0, 0)
                  .build();

sheet.insertChart(chart);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const range = sheet.getRange('A1:B5');
const chart = sheet.newChart()
                  .setChartType(Charts.ChartType.BAR)
                  .addRange(range)
                  .setPosition(5, 5, 0, 0)
                  .build();

sheet.insertChart(chart);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const chart = sheet.getCharts()[0];
const newChart = chart.modify()
                     .clearRanges()
                     .addRange(sheet.getRange('A1:A5'))
                     .addRange(sheet.getRange('B1:B5'))
                     .build();
sheet.updateChart(newChart);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const chartBuilder = sheet.newChart()
                         .setChartType(Charts.ChartType.BAR)
                         .addRange(sheet.getRange('A1:B8'))
                         .setPosition(5, 5, 0, 0);

const containerInfo = chartBuilder.getContainer();

Logger.log(
    'Anchor Column: %s\r\nAnchor Row %s\r\nOffset X %s\r\nOffset Y %s',
    containerInfo.getAnchorColumn(),
    containerInfo.getAnchorRow(),
    containerInfo.getOffsetX(),
    containerInfo.getOffsetY(),
);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const chartBuilder = sheet.newChart()
                         .setChartType(Charts.ChartType.BAR)
                         .addRange(sheet.getRange('A1:B8'))
                         .setPosition(5, 5, 0, 0);

const ranges = chartBuilder.getRanges();

for (const i in ranges) {
  const range = ranges[i];
  Logger.log(range.getA1Notation());
}
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const firstRange = sheet.getRange('A1:B5');
const secondRange = sheet.getRange('A6:B8');

const chartBuilder = sheet.newChart()
                         .setChartType(Charts.ChartType.BAR)
                         .addRange(firstRange)
                         .addRange(secondRange)
                         .setPosition(5, 5, 0, 0);

chartBuilder.removeRange(firstRange);
chartBuilder.removeRange(sheet.getRange('A6:B8'));

const chart = chartBuilder.build();

sheet.insertChart(chart);
```

```javascript
const builder = Charts.newPieChart();
builder.reverseCategories();
```

```javascript
const builder = Charts.newLineChart();
builder.setBackgroundColor('gray');
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const range = sheet.getRange('A1:B5');
const chart = sheet.newChart()
                  .setChartType(Charts.ChartType.BAR)
                  .addRange(range)
                  .setPosition(5, 5, 0, 0)
                  .build();

sheet.insertChart(chart);
```

```javascript
const builder = Charts.newLineChart();
builder.setColors(['green', 'red']);
```

```javascript
const builder = Charts.newLineChart();
builder.setCurveStyle(Charts.CurveStyle.SMOOTH);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const range = sheet.getRange('A1:B5');
const chart = sheet.newChart()
                  .setChartType(Charts.ChartType.BAR)
                  .addRange(range)
                  .setHiddenDimensionStrategy(
                      Charts.ChartHiddenDimensionStrategy.IGNORE_COLUMNS,
                      )
                  .setPosition(5, 5, 0, 0)
                  .build();

sheet.insertChart(chart);
```

```javascript
const builder = Charts.newLineChart();
builder.setLegendPosition(Charts.Position.RIGHT);
```

```javascript
const textStyleBuilder =
    Charts.newTextStyle().setColor('#0000FF').setFontSize(26);
const style = textStyleBuilder.build();
const builder = Charts.newLineChart();
builder.setLegendTextStyle(style);
```

```javascript
const ss = SpreadsheetApp.getActiveSpreadsheet();
const sheet = ss.getSheets()[0];

const range = sheet.getRange('A1:B10');
const range2 = sheet.getRange('C:C10');
const chart = sheet.newChart()
                  .setChartType(Charts.ChartType.BAR)
                  .addRange(range)
                  .addRange(range2)
                  .setMergeStrategy(Charts.ChartMergeStrategy.MERGE_ROWS)
                  .setPosition(5, 5, 0, 0)
                  .build();

sheet.insertChart(chart);
```
