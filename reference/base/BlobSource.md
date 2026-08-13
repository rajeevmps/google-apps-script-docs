# BlobSource

Interface for objects that can export their data as a Blob.

Interface for objects that can export their data as a `Blob`.

## Methods

### getAs(contentType: String) → Blob

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes "ShoppingList.12.25.pdf".

To view the daily quotas for conversions, see Quotas for Google Services. Newly created Google Workspace domains might be temporarily subject to stricter quotas.

**Parameters:**
- `contentType` (String): The MIME type to convert to. For most blobs, `'application/pdf'` is the only valid option. For images in BMP, GIF, JPEG, or PNG format, any of `'image/bmp'`, `'image/gif'`, `'image/jpeg'`, or `'image/png'` are also valid. For a Google Docs document, `'text/markdown'` is also valid.

**Return:** `Blob` — The data as a blob.

### getBlob() → Blob

Return the data inside this object as a blob.

**Return:** `Blob` — The data as a blob.
