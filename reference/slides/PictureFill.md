# PictureFill

A fill that renders an image that's stretched to the dimensions of its container.

"A fill that renders an image that's stretched to the dimensions of its container."

PictureFill is a fill implementation that stretches images to match container dimensions. It enables retrieval of image data in multiple formats and provides access to both temporary and original source URLs.

## Methods

### getAs(contentType)

`Blob`

Return the data inside this object as a blob converted to the specified content type.

**Parameters**

- `contentType` (`String`) — The MIME type to convert to.

**Returns**

`Blob` — Blob containing the converted data.

### getBlob()

`Blob`

Return the data inside this object as a converted blob.

**Returns**

`Blob` — The data as a blob.

### getContentUrl()

`String`

Gets a URL to the image. This URL is tagged with the account of the requester, so anyone with the URL effectively accesses the image as the original requester. Access to the image may be lost if the presentation's sharing settings change. The URL expires after a short period of time.

**Returns**

`String` — URL to the image.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSourceUrl()

`String|null`

Gets the image's source URL, if available. When an image is inserted by URL, returns the URL provided during image insertion.

**Returns**

`String|null` — the image URL, or null if unavailable.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

None.
