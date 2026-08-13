# ChartHiddenDimensionStrategy

An enumeration of how hidden dimensions in a source are expressed in a chart.

An enumeration of how hidden dimensions in a source are expressed in a chart. To call an enum, reference its parent class, name, and property (e.g., `Charts.ChartHiddenDimensionStrategy.IGNORE_ROWS`).

## Methods

None.

## Properties

| Property | Type | Description |
|---|---|---|
| IGNORE_BOTH | Enum | Default; charts skips any hidden columns and hidden rows. |
| IGNORE_ROWS | Enum | Charts skips hidden rows only. |
| IGNORE_COLUMNS | Enum | Charts skips hidden columns only. |
| SHOW_BOTH | Enum | Charts does not skip hidden columns or hidden rows. |
