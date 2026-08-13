# LookerDataSourceSpec

Access the existing Looker data source specification.

LookerDataSourceSpec is a DataSourceSpec used to access existing Looker data source specifications. You can obtain a Looker data source specification from a sheet with a Looker connection using `getDataSources()` and `asLooker()`. The `copy()` method creates a DataSourceSpecBuilder based on the current data source settings. Methods like `getExploreName()`, `getInstanceUrl()`, and `getModelName()` retrieve specific details about the Looker data source. `getParameters()` gets the data source parameters, which is only available for BigQuery data sources, and `getType()` gets the data source type.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `copy()` | `DataSourceSpecBuilder` | Creates a DataSourceSpecBuilder based on this data source's settings. |
| `getExploreName()` | `String` | Gets the name of the Looker explore in the model. |
| `getInstanceUrl()` | `String` | Gets the URL of the Looker instance. |
| `getModelName()` | `String` | Gets the name of the Looker model in the instance. |
| `getParameters()` | `DataSourceParameter[]` | Gets the parameters of the data source. This method is only available for BigQuery data sources. |
| `getType()` | `DataSourceType` | Gets the type of the data source. |
