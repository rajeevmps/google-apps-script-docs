# Advanced Sheets Service

Source: https://developers.google.com/apps-script/advanced/sheets

## Overview

The Advanced Sheets Service enables Google Apps Script to access the Sheets API for reading, editing, formatting, and presenting data in Google Sheets. As noted in the documentation, "this API lets scripts read, edit, format and present data in Google Sheets."

This is an advanced service requiring enablement before use. While the built-in Google Sheets service is often simpler, this advanced option provides additional capabilities not available through standard methods.

## Key Features

- Access to Sheets API v4
- Read and write operations on spreadsheet ranges
- Sheet creation and management
- Pivot table creation
- Uses identical objects, methods, and parameters as the public Sheets API

## Sample Code Examples

### Reading Data from a Range

```javascript
function readRange(spreadsheetId = yourspreadsheetId) {
  try {
    const response = Sheets.Spreadsheets.Values.get(
      spreadsheetId,
      "Sheet1!A1:D5",
    );
    if (response.values) {
      console.log(response.values);
      return;
    }
    console.log("Failed to get range of values from spreadsheet");
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Writing to Multiple Ranges

```javascript
function writeToMultipleRanges(spreadsheetId = yourspreadsheetId) {
  const columnAValues = [["Item", "Wheel", "Door", "Engine"]];
  const rowValues = [
    ["Cost", "Stocked", "Ship Date"],
    ["$20.50", "4", "3/1/2016"],
  ];

  const request = {
    valueInputOption: "USER_ENTERED",
    data: [
      {
        range: "Sheet1!A1:A4",
        majorDimension: "COLUMNS",
        values: columnAValues,
      },
      {
        range: "Sheet1!B1:D2",
        majorDimension: "ROWS",
        values: rowValues,
      },
    ],
  };
  try {
    const response = Sheets.Spreadsheets.Values.batchUpdate(
      request,
      spreadsheetId,
    );
    if (response) {
      console.log(response);
      return;
    }
    console.log("response null");
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Adding a New Sheet

```javascript
function addSheet(spreadsheetId = yourspreadsheetId) {
  const requests = [
    {
      addSheet: {
        properties: {
          title: "Deposits",
          gridProperties: {
            rowCount: 20,
            columnCount: 12,
          },
          tabColor: {
            red: 1.0,
            green: 0.3,
            blue: 0.4,
          },
        },
      },
    },
  ];
  try {
    const response = Sheets.Spreadsheets.batchUpdate(
      { requests: requests },
      spreadsheetId,
    );
    console.log(
      `Created sheet with ID: ${response.replies[0].addSheet.properties.sheetId}`,
    );
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

### Creating a Pivot Table

```javascript
function addPivotTable(
  spreadsheetId = yourspreadsheetId,
  pivotSourceDataSheetId = yourpivotSourceDataSheetId,
  destinationSheetId = yourdestinationSheetId,
) {
  const requests = [
    {
      updateCells: {
        rows: {
          values: [
            {
              pivotTable: {
                source: {
                  sheetId: pivotSourceDataSheetId,
                  startRowIndex: 0,
                  startColumnIndex: 0,
                  endRowIndex: 20,
                  endColumnIndex: 7,
                },
                rows: [
                  {
                    sourceColumnOffset: 0,
                    showTotals: true,
                    sortOrder: "ASCENDING",
                    valueBucket: {
                      buckets: [
                        {
                          stringValue: "West",
                        },
                      ],
                    },
                  },
                  {
                    sourceColumnOffset: 1,
                    showTotals: true,
                    sortOrder: "DESCENDING",
                    valueBucket: {},
                  },
                ],
                columns: [
                  {
                    sourceColumnOffset: 4,
                    sortOrder: "ASCENDING",
                    showTotals: true,
                    valueBucket: {},
                  },
                ],
                values: [
                  {
                    summarizeFunction: "SUM",
                    sourceColumnOffset: 3,
                  },
                ],
                valueLayout: "HORIZONTAL",
              },
            },
          ],
        },
        start: {
          sheetId: destinationSheetId,
          rowIndex: 49,
          columnIndex: 0,
        },
        fields: "pivotTable",
      },
    },
  ];
  try {
    const response = Sheets.Spreadsheets.batchUpdate(
      { requests: requests },
      spreadsheetId,
    );
  } catch (e) {
    console.log("Failed with error %s", e.message);
  }
}
```

## Resources

- [Sheets API Reference Documentation](https://developers.google.com/sheets/api/reference/rest) (external — not scraped)
- [Sheets Support Guide](https://developers.google.com/sheets/api/support) (external — not scraped)
- [GitHub Sample Repository](https://github.com/googleworkspace/apps-script-samples/blob/main/advanced/sheets.gs)
</content>
