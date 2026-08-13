# Charts

Entry point for creating Charts in scripts.

Entry point for creating Charts in scripts. The Charts service enables creation of various chart types including Area, Bar, Column, Line, Pie, Scatter, and Table charts. Data for charts is held in a `DataTable`, which can be built manually. Charts can be added to a web page as an image.

```javascript
function doGet() {
  const data = Charts.newDataTable()
                   .addColumn(Charts.ColumnType.STRING, 'Month')
                   .addColumn(Charts.ColumnType.NUMBER, 'In Store')
                   .addColumn(Charts.ColumnType.NUMBER, 'Online')
                   .addRow(['January', 10, 1])
                   .addRow(['February', 12, 1])
                   .addRow(['March', 20, 2])
                   .addRow(['April', 25, 3])
                   .addRow(['May', 30, 4])
                   .build();

  const chart = Charts.newAreaChart()
                    .setDataTable(data)
                    .setStacked()
                    .setRange(0, 40)
                    .setTitle('Sales per Month')
                    .build();

  const htmlOutput = HtmlService.createHtmlOutput().setTitle('My Chart');
  const imageData = Utilities.base64Encode(chart.getAs('image/png').getBytes());
  const imageUrl = `data:image/png;base64,${encodeURI(imageData)}`;
  htmlOutput.append('Render chart server side: <br/>');
  htmlOutput.append(`<img border="1" src="${imageUrl}">`);
  return htmlOutput;
}
```

## Methods

### newAreaChart()

Returns: `AreaChartBuilder`

Starts building an area chart, as described in the Google Chart Tools documentation.

### newBarChart()

Returns: `BarChartBuilder`

Starts building a bar chart, as described in the Google Chart Tools documentation.

### newColumnChart()

Returns: `ColumnChartBuilder`

Starts building a column chart, as described in the Google Chart Tools documentation.

### newDataTable()

Returns: `DataTableBuilder`

Creates an empty data table, which can have its values set manually. Data tables hold the data for all chart types.

### newDataViewDefinition()

Returns: `DataViewDefinitionBuilder`

Creates a new data view definition. Use setters to define the different properties of the data view.

### newLineChart()

Returns: `LineChartBuilder`

Starts building a line chart, as described in the Google Chart Tools documentation.

### newPieChart()

Returns: `PieChartBuilder`

Starts building a pie chart, as described in the Google Chart Tools documentation.

### newScatterChart()

Returns: `ScatterChartBuilder`

Starts building a scatter chart, as described in the Google Chart Tools documentation.

### newTableChart()

Returns: `TableChartBuilder`

Starts building a table chart, as described in the Google Chart Tools documentation.

### newTextStyle()

Returns: `TextStyleBuilder`

Creates a new text style builder. To change the default values, use the setter functions.

## Properties

| Property | Type | Description |
|---|---|---|
| ChartHiddenDimensionStrategy | [ChartHiddenDimensionStrategy](ChartHiddenDimensionStrategy.md) | An enumeration of how hidden dimensions in a source are expressed in a chart. |
| ChartMergeStrategy | [ChartMergeStrategy](ChartMergeStrategy.md) | An enumeration of how multiple ranges in the source are expressed in a chart. |
| ChartType | [ChartType](ChartType.md) | The chart types supported by the Charts service. |
| ColumnType | [ColumnType](ColumnType.md) | The valid data types for columns in a DataTable. |
| CurveStyle | [CurveStyle](CurveStyle.md) | The styles for curves in a chart. |
| MatchType | [MatchType](MatchType.md) | How a string value should be matched. |
| Orientation | [Orientation](Orientation.md) | The orientation of an object. |
| PickerValuesLayout | [PickerValuesLayout](PickerValuesLayout.md) | How to display selected values in a picker widget. |
| PointStyle | [PointStyle](PointStyle.md) | The styles of points in a line. |
| Position | [Position](Position.md) | Legend positions within a chart. |
