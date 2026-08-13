# SpreadsheetApp

Access and create Google Sheets files; the parent class for the Spreadsheet service.

The `SpreadsheetApp` class is used to access and create Google Sheets files and serves as the parent class for the Spreadsheet service.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `create(name: String)` | `Spreadsheet` | Creates a new spreadsheet with the given name. |
| `create(name: String, rows: Integer, columns: Integer)` | `Spreadsheet` | Creates a new spreadsheet with the given name and the specified number of rows and columns. |
| `enableAllDataSourcesExecution()` | `void` | Turns data execution on for all types of data sources. Data execution throws an exception if the data source type isn't turned on. Use this method to turn data execution on for all data source types. |
| `enableBigQueryExecution()` | `void` | Turns data execution on for BigQuery data sources. Data execution for BigQuery data source throws an exception if not turned on. |
| `enableLookerExecution()` | `void` | Turns data execution on for Looker data sources. Data execution for Looker data source throws an exception if not turned on. |
| `flush()` | `void` | Applies all pending Spreadsheet changes. Spreadsheet operations are sometimes bundled together to improve performance, such as when doing multiple calls to Range.getValue(). However, sometimes you may want to make sure that all pending changes are made right away, for instance to show users data as a script is executing. |
| `getActive()` | `Spreadsheet` | Returns the currently active spreadsheet, or null if there is none. Functions that are run in the context of a spreadsheet can get a reference to the corresponding Spreadsheet object by calling this function. |
| `getActiveRange()` | `Range` | Returns the selected range in the active sheet, or null if there is no active range. If multiple ranges are selected this method returns only the last selected range. This generally means the range that a user has selected in the active sheet, but in a custom function it refers to the cell being actively recalculated. |
| `getActiveRangeList()` | `RangeList\|null` | Returns the list of active ranges in the active sheet or null if there are no ranges selected. The active range containing the current highlighted cell is placed last in the list. If there is a single range selected, this behaves as a getActiveRange() call. |
| `getActiveSheet()` | `Sheet` | Gets the active sheet in a spreadsheet. The active sheet in a spreadsheet is the sheet that is being displayed in the spreadsheet UI. |
| `getActiveSpreadsheet()` | `Spreadsheet` | Returns the currently active spreadsheet, or null if there is none. Functions that are run in the context of a spreadsheet can get a reference to the corresponding Spreadsheet object by calling this function. |
| `getCurrentCell()` | `Range\|null` | Returns the current (highlighted) cell that is selected in one of the active ranges in the active sheet or null if there is no current cell. |
| `getSelection()` | `Selection` | Returns the current Selection in the spreadsheet. |
| `getUi()` | `Ui` | Returns an instance of the spreadsheet's user-interface environment that allows the script to add features like menus, dialogs, and sidebars. A script can only interact with the UI for the current instance of an open spreadsheet, and only if the script is bound to the spreadsheet. |
| `newCellImage()` | `CellImageBuilder` | Creates a builder for a CellImage. |
| `newColor()` | `ColorBuilder` | Creates a builder for a Color. |
| `newConditionalFormatRule()` | `ConditionalFormatRuleBuilder` | Creates a builder for a conditional formatting rule. |
| `newDataSourceSpec()` | `DataSourceSpecBuilder` | Creates a builder for a DataSourceSpec. |
| `newDataValidation()` | `DataValidationBuilder` | Creates a builder for a data validation rule. |
| `newFilterCriteria()` | `FilterCriteriaBuilder` | Creates a builder for a FilterCriteria. |
| `newRichTextValue()` | `RichTextValueBuilder` | Creates a builder for a Rich Text value. |
| `newTextStyle()` | `TextStyleBuilder` | Creates a builder for a text style. |
| `open(file: File)` | `Spreadsheet` | Opens the spreadsheet that corresponds to the given File object. |
| `openById(id: String)` | `Spreadsheet` | Opens the spreadsheet with the given ID. |
| `openByUrl(url: String)` | `Spreadsheet` | Opens the spreadsheet with the given URL. |
| `setActiveRange(range: Range)` | `Range` | Sets the specified range as the active range, with the top left cell in the range as the current cell. |
| `setActiveRangeList(rangeList: RangeList)` | `RangeList` | Sets the specified list of ranges as the active ranges. |
| `setActiveSheet(sheet: Sheet)` | `Sheet` | Sets the active sheet in a spreadsheet. |
| `setActiveSheet(sheet: Sheet, restoreSelection: Boolean)` | `Sheet` | Sets the active sheet in a spreadsheet, with the option to restore the most recent selection within that sheet. |
| `setActiveSpreadsheet(newActiveSpreadsheet: Spreadsheet)` | `void` | Sets the active spreadsheet. |
| `setCurrentCell(cell: Range)` | `Range` | Sets the specified cell as the current cell. |

## Properties (Enum accessors)

| Property | Type | Description |
|---|---|---|
| `AutoFillSeries` | `AutoFillSeries` | An enumeration of the types of series used to calculate auto-filled values. |
| `BandingTheme` | `BandingTheme` | An enumeration of the possible banding themes. |
| `BooleanCriteria` | `BooleanCriteria` | An enumeration of conditional formatting boolean criteria. |
| `BorderStyle` | `BorderStyle` | An enumeration of the valid styles for setting borders on a Range. |
| `ColorType` | `ColorType` | An enumeration of possible color types. |
| `CopyPasteType` | `CopyPasteType` | An enumeration of the possible paste types. |
| `DataExecutionErrorCode` | `DataExecutionErrorCode` | An enumeration of the possible data execution error codes. |
| `DataExecutionState` | `DataExecutionState` | An enumeration of the possible data execution states. |
| `DataSourceParameterType` | `DataSourceParameterType` | An enumeration of the possible data source parameter types. |
| `DataSourceRefreshScope` | `DataSourceRefreshScope` | An enumeration of possible data source refresh scopes. |
| `DataSourceType` | `DataSourceType` | An enumeration of the possible data source types. |
| `DataValidationCriteria` | `DataValidationCriteria` | An enumeration representing the data validation criteria. |
| `DateTimeGroupingRuleType` | `DateTimeGroupingRuleType` | An enumeration of date time grouping rule. |
| `DeveloperMetadataLocationType` | `DeveloperMetadataLocationType` | An enumeration of possible developer metadata location types. |
| `DeveloperMetadataVisibility` | `DeveloperMetadataVisibility` | An enumeration of the possible developer metadata visibilities. |
| `Dimension` | `Dimension` | An enumeration of the possible dimensions of a spreadsheet. |
| `Direction` | `Direction` | A enumeration of the possible directions that one can move within a spreadsheet using the arrow keys. |
| `FrequencyType` | `FrequencyType` | An enumeration of possible frequency types. |
| `GroupControlTogglePosition` | `GroupControlTogglePosition` | An enumeration of the positions that the group control toggle can be in. |
| `InterpolationType` | `InterpolationType` | An enumeration of conditional format gradient interpolation types. |
| `PivotTableSummarizeFunction` | `PivotTableSummarizeFunction` | An enumeration of the functions that may be used to summarize values in a pivot table. |
| `PivotValueDisplayType` | `PivotValueDisplayType` | An enumeration of the ways that a pivot value may be displayed. |
| `ProtectionType` | `ProtectionType` | An enumeration representing the parts of a spreadsheet that can be protected. |
| `RecalculationInterval` | `RecalculationInterval` | An enumeration of the possible intervals that can be used in spreadsheet recalculation. |
| `RelativeDate` | `RelativeDate` | An enumeration of relative date options for calculating a value to be used in date-based BooleanCriteria. |
| `SheetType` | `SheetType` | An enumeration of the different types of sheets that can exist in a spreadsheet. |
| `SortOrder` | `SortOrder` | An enumeration of sort order. |
| `TextDirection` | `TextDirection` | An enumeration of valid text directions. |
| `TextToColumnsDelimiter` | `TextToColumnsDelimiter` | An enumeration of the preset delimiters for split text to columns. |
| `ThemeColorType` | `ThemeColorType` | An enumeration of possible theme color types. |
| `ValueType` | `ValueType` | An enumeration of value types returned by Range.getValue() and Range.getValues(). |
| `WrapStrategy` | `WrapStrategy` | An enumeration of the strategies used for wrapping cells. |

## Code Samples

```javascript
const ssNew = SpreadsheetApp.create('Finances');
Logger.log(ssNew.getUrl());
```

```javascript
const ssNew = SpreadsheetApp.create('Finances', 50, 5);
Logger.log(ssNew.getUrl());
```

```javascript
SpreadsheetApp.enableAllDataSourcesExecution();
const ss = SpreadsheetApp.openById('abc123456');
ss.getDataSourceSheets()[0].refreshData();
```

```javascript
SpreadsheetApp.enableBigQueryExecution();
const ss = SpreadsheetApp.openById('abc123456');
ss.getDataSourceSheets()[0].refreshData();
```

```javascript
SpreadsheetApp.enableLookerExecution();
const ss = SpreadsheetApp.openById('abc123456');
ss.getDataSourceSheets()[0].refreshData();
```

```javascript
function colors() {
  const sheet = SpreadsheetApp.getActiveSheet();
  for (let i = 0; i < 20; i++) {
    if (i % 2 === 0) {
      sheet.getRange('A1').setBackground('green');
      sheet.getRange('B1').setBackground('red');
    } else {
      sheet.getRange('A1').setBackground('red');
      sheet.getRange('B1').setBackground('green');
    }
    SpreadsheetApp.flush();
  }
}
```

```javascript
Logger.log(SpreadsheetApp.getActive().getUrl());
```

```javascript
const colorObject = SpreadsheetApp.getActiveRange().getBackgroundObject();
Logger.log(colorObject.asRgbColor().asHexString());
```

```javascript
const rangeList = SpreadsheetApp.getActiveRangeList();
```

```javascript
Logger.log(SpreadsheetApp.getActiveSheet().getName());
```

```javascript
Logger.log(SpreadsheetApp.getActiveSpreadsheet().getUrl());
```

```javascript
const currentCell = SpreadsheetApp.getCurrentCell();
```

```javascript
const selection = SpreadsheetApp.getSelection();
const currentCell = selection.getCurrentCell();
```

```javascript
function onOpen(e) {
  SpreadsheetApp.getUi()
      .createMenu('My Menu')
      .addItem('My menu item', 'myFunction')
      .addSeparator()
      .addSubMenu(
          SpreadsheetApp.getUi()
              .createMenu('My sub-menu')
              .addItem('One sub-menu item', 'mySecondFunction')
              .addItem('Another sub-menu item', 'myThirdFunction'),
          )
      .addToUi();
}
```
