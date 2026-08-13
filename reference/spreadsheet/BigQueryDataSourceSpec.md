# BigQueryDataSourceSpec

Access the existing BigQuery data source specification.

Access the existing BigQuery data source specification. To create a new data source specification, use `SpreadsheetApp.newDataSourceSpec()`. BigQueryDataSourceSpec allows you to work with existing BigQuery data source specifications within SpreadsheetApp. The class provides methods to retrieve configuration details from a BigQuery data source.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copy()` | `DataSourceSpecBuilder` | Creates a `DataSourceSpecBuilder` based on this data source's settings. |
| `getDatasetId()` | `String` | Gets the BigQuery dataset ID. Returns the dataset ID, or an empty string if the data source spec is defined by a raw query. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. This method is only available for BigQuery data sources. Returns the parameter list. |
| `getProjectId()` | `String` | Gets the billing project ID. Returns the project ID. |
| `getRawQuery()` | `String` | Gets the raw query string. Returns the raw query string. |
| `getTableId()` | `String` | Gets the BigQuery table ID. Returns the table ID, or an empty string if the data source spec is defined by a raw query. |
| `getTableProjectId()` | `String` | Gets the BigQuery project ID for the table. Returns the table project ID, or an empty string if the data source spec is defined by a raw query. |
| `getType()` | `DataSourceType` | Gets the type of the data source. Returns the data source type. |

## Code Samples

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const newSpec = spec.copy();
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const parameters = spec.getParameters();
```

```javascript
const ss = SpreadsheetApp.openByUrl(
    'https://docs.google.com/spreadsheets/d/abc123456/edit',
);
const spec = ss.getDataSources()[0].getSpec();
const type = spec.getType();
```
