# ContainerInfo

Access the chart's position within a sheet.

Access the chart's position within a sheet. Can be updated using the `EmbeddedChart.modify()` function. ContainerInfo is used to access and update a chart's position within a sheet. The position can be modified using the `EmbeddedChart.modify()` function. Methods are available to get the anchor column and row, and the X and Y offsets in pixels.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getAnchorColumn()` | `Integer` | The chart's left side is anchored in this column. Returns a 1-indexed column (that is, column C is 3). |
| `getAnchorRow()` | `Integer` | The chart's top side is anchored in this row. Returns a 1-indexed row (that is, row 5 returns 5). |
| `getOffsetX()` | `Integer` | The chart's upper left hand corner is offset from the anchor column by this many pixels. Returns the horizontal offset in pixels for the upper left hand corner of the chart. |
| `getOffsetY()` | `Integer` | The chart's upper left hand corner is offset from the anchor row by this many pixels. Returns the vertical offset in pixels for the upper left hand corner of the chart. |

## Code Samples

```javascript
const sheet = SpreadsheetApp.getActiveSheet();
const chart = sheet.getCharts()[0];
const modifiedChart = chart.modify().setPosition(5, 5, 0, 0).build();
sheet.updateChart(modifiedChart);
```
