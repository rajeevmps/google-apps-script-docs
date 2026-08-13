# JdbcBlob

A JDBC `Blob`. For documentation of this class, see `java.sql.Blob` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html).

## Methods

### free()

Returns: `void`

For documentation of this method, see `java.sql.Blob#free()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#free()).

---

### getAppsScriptBlob()

Returns: `Blob`

Gets the content of this JdbcBlob as an Apps Script blob.

**Returns:** `Blob` — A `Blob` that can be used directly by other Apps Script APIs.

---

### getAs(contentType)

Returns: `Blob`

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes "ShoppingList.12.25.pdf".

To view the daily quotas for conversions, see Quotas for Google Services (https://developers.google.com/apps-script/guides/services/quotas). Newly created Google Workspace domains might be temporarily subject to stricter quotas.

**Parameters:**
- `contentType` (String): The MIME type to convert to. For most blobs, `'application/pdf'` is the only valid option. For images in BMP, GIF, JPEG, or PNG format, any of `'image/bmp'`, `'image/gif'`, `'image/jpeg'`, or `'image/png'` are also valid. For a Google Docs document, `'text/markdown'` is also valid.

**Returns:** `Blob` — The data as a blob.

---

### getBytes(position, length)

Returns: `Byte[]`

For documentation of this method, see `java.sql.Blob#getBytes(long, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#getBytes(long,%20int)).

**Parameters:**
- `position` (Integer): The ordinal position of the first byte in the blob value to be extracted; the first byte is at position 1.
- `length` (Integer): The number of consecutive bytes to copy; the value for length must be zero or greater.

**Returns:** `Byte[]` — A byte array containing up to the specified number of consecutive bytes from the blob value.

---

### length()

Returns: `Integer`

For documentation of this method, see `java.sql.Blob#length()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#length()).

**Returns:** `Integer` — The number of bytes in this blob.

---

### position(pattern, start)

Returns: `Integer`

For documentation of this method, see `java.sql.Blob#position(byte[], long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#position(byte[],%20long)).

**Parameters:**
- `pattern` (Byte[]): The byte array to search for.
- `start` (Integer): The position in the blob value where to beging searching; the first position is 1.

**Returns:** `Integer` — The position at which the specified pattern begins, or else -1 if the pattern is not found.

---

### position(pattern, start)

Returns: `Integer`

For documentation of this method, see `java.sql.Blob#position(blob, long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#position(java.sql.Blob,%20long)).

**Parameters:**
- `pattern` (JdbcBlob): The `JdbcBlob` indicating the value to search for.
- `start` (Integer): The position in the blob value where to beging searching; the first position is 1.

**Returns:** `Integer` — The position at which the specified pattern begins, or else -1 if the pattern is not found.

---

### setBytes(position, blobSource)

Returns: `Integer`

Convenience method for writing a `JdbcBlob` to this blob.

**Parameters:**
- `position` (Integer): The position in the blob at which to start writing; the first position is 1.
- `blobSource` (BlobSource): The source of data to write to this blob.

**Returns:** `Integer` — The number of bytes written.

---

### setBytes(position, blobSource, offset, length)

Returns: `Integer`

Convenience method for writing a `JdbcBlob` to this blob.

**Parameters:**
- `position` (Integer): The position in the blob at which to start writing; the first position is 1.
- `blobSource` (BlobSource): The source of data to write to this blob.
- `offset` (Integer): The offset into the provided byte array at which to start reading bytes to set.
- `length` (Integer): The number of bytes to write to the blob.

**Returns:** `Integer` — The number of bytes written.

---

### setBytes(position, bytes)

Returns: `Integer`

For documentation of this method, see `java.sql.Blob#setBytes(long, byte[])` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#setBytes(long,%20byte[])).

**Parameters:**
- `position` (Integer): The position in the blob at which to start writing; the first position is 1.
- `bytes` (Byte[]): The array of bytes to write to this blob.

**Returns:** `Integer` — The number of bytes written.

---

### setBytes(position, bytes, offset, length)

Returns: `Integer`

For documentation of this method, see `java.sql.Blob#setBytes(long, byte[], int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#setBytes(long,%20byte[],%20int,%20int)).

**Parameters:**
- `position` (Integer): The position in the blob at which to start writing; the first position is 1.
- `bytes` (Byte[]): The array of bytes to write to this blob.
- `offset` (Integer): The offset into the provided byte array at which to start reading bytes to set.
- `length` (Integer): The number of bytes to write to the blob.

**Returns:** `Integer` — The number of bytes written.

---

### truncate(length)

Returns: `void`

For documentation of this method, see `java.sql.Blob#truncate(long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Blob.html#truncate(long)).

**Parameters:**
- `length` (Integer): The size (in bytes) of this blob after truncation.

## Properties

None.
