# Chart

A Chart object, which can be converted to a static image.

A Chart object, which can be converted to a static image. For charts embedded in spreadsheets, see `EmbeddedChart`.

## Methods

### getAs(contentType)

Returns: `Blob`

Converts the chart data to a blob in a specified content type, automatically adding the appropriate file extension. The method assumes any filename suffix after the last period is an existing extension to be replaced. For most blobs, PDF is the primary option; images in BMP, GIF, JPEG, or PNG formats accept corresponding MIME types, and Google Docs documents support text/markdown.

**Parameters**

| Name | Type | Description |
|---|---|---|
| contentType | String | The MIME type to convert to. |

### getBlob()

Returns: `Blob`

Retrieves the chart data as a blob in its current format.

### getOptions()

Returns: `ChartOptions`

Provides the immutable configuration options for the chart, including dimensions, color schemes, and axis settings.

## Properties

None.
