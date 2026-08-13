# Spreadsheet Service Reference

Offline local markdown copy of the Google Apps Script **Spreadsheet** service reference documentation (`https://developers.google.com/apps-script/reference/spreadsheet`). 108 classes and enums, one file per class/enum.

## Core Classes

| Class | Description |
|---|---|
| [SpreadsheetApp](./SpreadsheetApp.md) | Access and create Google Sheets files; the parent class for the Spreadsheet service. |
| [Spreadsheet](./Spreadsheet.md) | Access and modify Google Sheets files. |
| [Sheet](./Sheet.md) | Access and modify spreadsheet sheets. |
| [Range](./Range.md) | Access and modify spreadsheet ranges. |
| [RangeList](./RangeList.md) | A collection of one or more Range instances in the same sheet. |
| [Selection](./Selection.md) | Access the current active selection in the active sheet. |
| [NamedRange](./NamedRange.md) | Create, access and modify named ranges in a spreadsheet. |
| [Group](./Group.md) | Access and modify spreadsheet groups (collapsible row/column groupings). |

## Formatting & Style

| Class | Description |
|---|---|
| [Color](./Color.md) | Represents a color. |
| [ColorBuilder](./ColorBuilder.md) | Builder for Color. |
| [ThemeColor](./ThemeColor.md) | A representation for a theme color. |
| [SpreadsheetTheme](./SpreadsheetTheme.md) | Access and modify existing spreadsheet themes. |
| [Banding](./Banding.md) | Access and modify bandings, the color patterns applied to rows or columns of a range. |
| [BooleanCondition](./BooleanCondition.md) | Access the boolean criteria and formatting of a conditional format rule. |
| [ConditionalFormatRule](./ConditionalFormatRule.md) | Access conditional formatting rules. |
| [ConditionalFormatRuleBuilder](./ConditionalFormatRuleBuilder.md) | Builder for conditional formatting rules. |
| [GradientCondition](./GradientCondition.md) | Access gradient color conditions in ConditionalFormatRules. |
| [RichTextValue](./RichTextValue.md) | A stylized text string used to represent cell text. |
| [RichTextValueBuilder](./RichTextValueBuilder.md) | A builder for Rich Text values. |
| [TextRotation](./TextRotation.md) | Access the text rotation settings for a cell. |
| [TextStyle](./TextStyle.md) | The rendered style of text in a cell. |
| [TextStyleBuilder](./TextStyleBuilder.md) | A builder for text styles. |

## Data Validation & Finding/Filtering

| Class | Description |
|---|---|
| [DataValidation](./DataValidation.md) | Access data validation rules. |
| [DataValidationBuilder](./DataValidationBuilder.md) | Builder for data validation rules. |
| [Filter](./Filter.md) | Modify existing filters on Grid sheets. |
| [FilterCriteria](./FilterCriteria.md) | Get information about or copy the criteria on existing filters. |
| [FilterCriteriaBuilder](./FilterCriteriaBuilder.md) | Builder for filter criteria. |
| [TextFinder](./TextFinder.md) | Find or replace text within a range, sheet or spreadsheet. |
| [Slicer](./Slicer.md) | Represents a slicer, used to filter ranges, tables, and pivot tables in a non-collaborative way. |
| [SortSpec](./SortSpec.md) | The sorting specification for a sort operation. |

## Images & Drawings

| Class | Description |
|---|---|
| [CellImage](./CellImage.md) | Represents an image value in a cell. |
| [CellImageBuilder](./CellImageBuilder.md) | Builder for CellImage. |
| [OverGridImage](./OverGridImage.md) | Represents an image floating over the grid in a spreadsheet. |
| [Drawing](./Drawing.md) | Represents a drawing over a sheet in a spreadsheet. |
| [ContainerInfo](./ContainerInfo.md) | Access a chart's position within a sheet. |

## Embedded Chart Builders

| Class | Description |
|---|---|
| [EmbeddedChart](./EmbeddedChart.md) | Represents a chart that has been embedded into a spreadsheet. |
| [EmbeddedChartBuilder](./EmbeddedChartBuilder.md) | Builder used to edit an EmbeddedChart. |
| [EmbeddedAreaChartBuilder](./EmbeddedAreaChartBuilder.md) | Builder for area charts. |
| [EmbeddedBarChartBuilder](./EmbeddedBarChartBuilder.md) | Builder for bar charts. |
| [EmbeddedColumnChartBuilder](./EmbeddedColumnChartBuilder.md) | Builder for column charts. |
| [EmbeddedComboChartBuilder](./EmbeddedComboChartBuilder.md) | Builder for combo charts. |
| [EmbeddedHistogramChartBuilder](./EmbeddedHistogramChartBuilder.md) | Builder for histogram charts. |
| [EmbeddedLineChartBuilder](./EmbeddedLineChartBuilder.md) | Builder for line charts. |
| [EmbeddedPieChartBuilder](./EmbeddedPieChartBuilder.md) | Builder for pie charts. |
| [EmbeddedScatterChartBuilder](./EmbeddedScatterChartBuilder.md) | Builder for scatter charts. |
| [EmbeddedTableChartBuilder](./EmbeddedTableChartBuilder.md) | Builder for table charts. |

## Pivot Tables

| Class | Description |
|---|---|
| [PivotTable](./PivotTable.md) | Access and modify pivot tables. |
| [PivotFilter](./PivotFilter.md) | Access and modify pivot table filters. |
| [PivotGroup](./PivotGroup.md) | Access and modify pivot table breakout (row/column) groups. |
| [PivotGroupLimit](./PivotGroupLimit.md) | Access and modify a pivot table group limit. |
| [PivotValue](./PivotValue.md) | Access and modify value groups in pivot tables. |
| [DateTimeGroupingRule](./DateTimeGroupingRule.md) | Access an existing date-time grouping rule on a pivot group. |

## Data Source Classes (BigQuery / Looker connected sheets)

| Class | Description |
|---|---|
| [DataSource](./DataSource.md) | Access and modify an existing data source. |
| [DataSourceChart](./DataSourceChart.md) | Access and modify an existing data source chart. |
| [DataSourceColumn](./DataSourceColumn.md) | Access and modify a data source column. |
| [DataSourceFormula](./DataSourceFormula.md) | Access and modify existing data source formulas. |
| [DataSourceParameter](./DataSourceParameter.md) | Access existing data source parameters. |
| [DataSourcePivotTable](./DataSourcePivotTable.md) | Access and modify an existing data source pivot table. |
| [DataSourceRefreshSchedule](./DataSourceRefreshSchedule.md) | Access and modify an existing refresh schedule. |
| [DataSourceRefreshScheduleFrequency](./DataSourceRefreshScheduleFrequency.md) | Access a refresh schedule's frequency. |
| [DataSourceSheet](./DataSourceSheet.md) | Access and modify an existing data source sheet. |
| [DataSourceSheetFilter](./DataSourceSheetFilter.md) | Access and modify an existing data source sheet filter. |
| [DataSourceSpec](./DataSourceSpec.md) | Access the general settings of an existing data source spec. |
| [DataSourceSpecBuilder](./DataSourceSpecBuilder.md) | Builder for the general settings of a data source spec. |
| [DataSourceTable](./DataSourceTable.md) | Access and modify an existing data source table. |
| [DataSourceTableColumn](./DataSourceTableColumn.md) | Access and modify an existing column in a DataSourceTable. |
| [DataSourceTableFilter](./DataSourceTableFilter.md) | Access and modify an existing data source table filter. |
| [DataExecutionStatus](./DataExecutionStatus.md) | Access the status of a data execution. |
| [BigQueryDataSourceSpec](./BigQueryDataSourceSpec.md) | Access an existing BigQuery data source specification. |
| [BigQueryDataSourceSpecBuilder](./BigQueryDataSourceSpecBuilder.md) | Builder for a BigQuery data source specification. |
| [LookerDataSourceSpec](./LookerDataSourceSpec.md) | Access an existing Looker data source specification. |
| [LookerDataSourceSpecBuilder](./LookerDataSourceSpecBuilder.md) | Builder for a Looker data source specification. |

## Protection & Developer Metadata

| Class | Description |
|---|---|
| [Protection](./Protection.md) | Access and modify protected ranges and sheets. |
| [PageProtection](./PageProtection.md) | Deprecated. Access and modify protected sheets in the older version of Google Sheets; use `Protection` instead. |
| [DeveloperMetadata](./DeveloperMetadata.md) | Access and modify developer metadata. |
| [DeveloperMetadataFinder](./DeveloperMetadataFinder.md) | Search for developer metadata in a spreadsheet. |
| [DeveloperMetadataLocation](./DeveloperMetadataLocation.md) | Access information about the location of developer metadata. |

## Enums

| Enum | Description |
|---|---|
| [AutoFillSeries](./AutoFillSeries.md) | Types of series used to calculate auto-filled values. |
| [BandingTheme](./BandingTheme.md) | The possible banding themes. |
| [BooleanCriteria](./BooleanCriteria.md) | Conditional formatting / data validation boolean criteria. |
| [BorderStyle](./BorderStyle.md) | Styles that can be set on a range border. |
| [CopyPasteType](./CopyPasteType.md) | Possible special paste types. |
| [DataExecutionErrorCode](./DataExecutionErrorCode.md) | Possible data execution error codes. |
| [DataExecutionState](./DataExecutionState.md) | Possible data execution states. |
| [DataSourceParameterType](./DataSourceParameterType.md) | Possible data source parameter types. |
| [DataSourceRefreshScope](./DataSourceRefreshScope.md) | Possible data source refresh scopes. |
| [DataSourceType](./DataSourceType.md) | Possible data source types (e.g. BigQuery, Looker). |
| [DataValidationCriteria](./DataValidationCriteria.md) | The data validation criteria that can be set on a range. |
| [DateTimeGroupingRuleType](./DateTimeGroupingRuleType.md) | Types of date-time grouping rules. |
| [DeveloperMetadataLocationType](./DeveloperMetadataLocationType.md) | Possible developer metadata location types. |
| [DeveloperMetadataVisibility](./DeveloperMetadataVisibility.md) | Possible developer metadata visibilities. |
| [Dimension](./Dimension.md) | Possible directions along which data can be stored in a spreadsheet (ROWS/COLUMNS). |
| [Direction](./Direction.md) | Possible directions of movement within a spreadsheet using the arrow keys. |
| [FrequencyType](./FrequencyType.md) | Possible frequency types for data source refresh schedules. |
| [GroupControlTogglePosition](./GroupControlTogglePosition.md) | Possible positions of a group control toggle. |
| [InterpolationType](./InterpolationType.md) | Gradient interpolation options for a GradientCondition. |
| [PivotTableSummarizeFunction](./PivotTableSummarizeFunction.md) | Functions that can summarize pivot table values. |
| [PivotValueDisplayType](./PivotValueDisplayType.md) | Ways a pivot value can be displayed as a function of another value. |
| [ProtectionType](./ProtectionType.md) | Parts of a spreadsheet that can be protected from edits. |
| [RecalculationInterval](./RecalculationInterval.md) | Possible intervals used in spreadsheet recalculation. |
| [RelativeDate](./RelativeDate.md) | Relative date options for date-based BooleanCriteria. |
| [SheetType](./SheetType.md) | The different types of sheets that can exist in a spreadsheet. |
| [SortOrder](./SortOrder.md) | Sort order (ascending/descending). |
| [TextDirection](./TextDirection.md) | Valid text directions. |
| [TextToColumnsDelimiter](./TextToColumnsDelimiter.md) | Preset delimiters for splitting a column of text into multiple columns. |
| [ThemeColorType](./ThemeColorType.md) | Color entries supported in themes. |
| [ValueType](./ValueType.md) | Value types returned by `Range.getValue()` and `Range.getValues()`. |
| [WrapStrategy](./WrapStrategy.md) | Strategies used to handle cell text wrapping. |
