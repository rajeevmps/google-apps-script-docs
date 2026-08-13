# EmbeddedChart

Represents a chart that has been embedded into a spreadsheet.

Represents a chart that has been embedded into a spreadsheet. It provides methods for accessing and modifying chart properties, enabling developers to work with charts programmatically within Google Sheets.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `asDataSourceChart()` | `DataSourceChart\|null` | Casts to a data source chart instance if the chart is a data source chart, or `null` otherwise. |
| `getAs(contentType: String)` | `Blob` | Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". |
| `getBlob()` | `Blob` | Return the data inside this object as a blob. |
| `getChartId()` | `Integer\|null` | Returns a stable identifier for the chart that is unique across the spreadsheet containing the chart or `null` if the chart is not in a spreadsheet. |
| `getContainerInfo()` | `ContainerInfo` | Returns information about where the chart is positioned within a sheet. |
| `getHiddenDimensionStrategy()` | `ChartHiddenDimensionStrategy` | Returns the strategy to use for handling hidden rows and columns. Defaults to `IGNORE_ROWS`. |
| `getMergeStrategy()` | `ChartMergeStrategy` | Returns the merge strategy used when more than one range exists. If `MERGE_ROWS`, row are merged; if `MERGE_COLUMNS`, columns are merged. |
| `getNumHeaders()` | `Integer` | Returns the number of rows or columns the range that are treated as headers. |
| `getOptions()` | `ChartOptions` | Returns the options for this chart, such as height, colors, and axes. The returned options are immutable. |
| `getRanges()` | `Range[]` | Returns the ranges that this chart uses as a data source. |
| `getTransposeRowsAndColumns()` | `Boolean` | If `true`, the rows and columns used to populate the chart are switched. Defaults to `false`. |
| `modify()` | `EmbeddedChartBuilder` | Returns an `EmbeddedChartBuilder` that can be used to modify this chart. Invoke `sheet.updateChart(chart)` to save any changes. |

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const range = sheet.getRange('A2:B8');
let chart = sheet.getCharts()[0];
chart = chart.modify()
            .addRange(range)
            .setOption('title', 'Updated!')
            .setOption('animation.duration', 500)
            .setPosition(2, 2, 0, 0)
            .build();
sheet.updateChart(chart);
```

```javascript
function newChart(range) {
  const sheet = SpreadsheetApp.getActiveSheet();
  const chartBuilder = sheet.newChart();
  chartBuilder.addRange(range)
      .setChartType(Charts.ChartType.LINE)
      .setOption('title', 'My Line Chart!');
  sheet.insertChart(chartBuilder.build());
}
```
