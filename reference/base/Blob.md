# Blob

A data interchange object for Apps Script services.

A data interchange object for Apps Script services. Note: `Blob` implements `BlobSource`.

## Methods

### copyBlob() → Blob

Returns a copy of this blob.

### getAs(contentType: String) → Blob

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced.

**Parameters:**
- `contentType` (String): the MIME type to convert to

### getBytes() → Byte[]

Gets the data stored in this blob.

### getContentType() → String|null

Gets the content type of the bytes in this blob.

### getDataAsString() → String

Gets the data of this blob as a String with UTF-8 encoding.

### getDataAsString(charset: String) → String

Gets the data of this blob as a string with the specified encoding.

**Parameters:**
- `charset` (String): the charset to use in encoding the data in this blob as a string

### getName() → String|null

Gets the name of this blob.

### isGoogleType() → Boolean

Returns whether this blob is a Google Workspace file (Sheets, Docs, etc.).

### setBytes(data: Byte[]) → Blob

Sets the data stored in this blob.

**Parameters:**
- `data` (Byte[]): the new data

### setContentType(contentType: String) → Blob

Sets the content type of the bytes in this blob.

**Parameters:**
- `contentType` (String): the new contentType

### setContentTypeFromExtension() → Blob

Sets the content type of the bytes in this blob based on the file extension. The contentType is `null` if it cannot be guessed from its extension.

### setDataFromString(string: String) → Blob

Sets the data of this blob from a string with UTF-8 encoding.

**Parameters:**
- `string` (String): the new data

### setDataFromString(string: String, charset: String) → Blob

Sets the data of this blob from a string with the specified encoding.

**Parameters:**
- `string` (String): the new data
- `charset` (String): the charset to use in interpreting the string as bytes

### setName(name: String) → Blob

Sets the name of this blob.

**Parameters:**
- `name` (String): the new name

## Deprecated Methods

### getAllBlobs() → Blob[]

Deprecated. Gets all the blobs that are contained within this (possibly composite) blob.
