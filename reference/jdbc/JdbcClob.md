# JdbcClob

A JDBC `Clob`. For documentation of this class, see `java.sql.Clob` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html).

## Methods

### free()

Returns: `void`

For documentation of this method, see `java.sql.Clob#truncate(long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#free()).

---

### getAppsScriptBlob()

Returns: `Blob`

Gets the content of this JdbcClob as an Apps Script blob.

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

### getSubString(position, length)

Returns: `String`

For documentation of this method, see `java.sql.Clob#getSubString(long, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#getSubString(long,%20int)).

**Parameters:**
- `position` (Integer): The index of the first character of the substring to extract. The first character is at index 1.
- `length` (Integer): The number of consecutive characters to copy (must be 0 or greater).

**Returns:** `String` — The retrieved substring.

---

### length()

Returns: `Integer`

For documentation of this method, see `java.sql.Clob#length()` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#length()).

**Returns:** `Integer` — The length (in characters) of this clob.

---

### position(search, start)

Returns: `Integer`

For documentation of this method, see `java.sql.Clob#position(Clob, long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#position(java.sql.Clob,%20long)).

**Parameters:**
- `search` (JdbcClob): The clob object to search for.
- `start` (Integer): The position at which to begin searching; the first position is 1.

**Returns:** `Integer` — The position at which the specifed clob appears, or -1 if it is not present.

---

### position(search, start)

Returns: `Integer`

For documentation of this method, see `java.sql.Clob#position(String, long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#position(java.lang.String,%20long)).

**Parameters:**
- `search` (String): The substring to search for.
- `start` (Integer): The position at which to begin searching; the first position is 1.

**Returns:** `Integer` — The position at which the specifed substring appears, or -1 if it is not present.

---

### setString(position, blobSource)

Returns: `Integer`

Convenience method for writing a `JdbcClob` to a clob.

**Parameters:**
- `position` (Integer): The position at which writing to the clob starts; the first position is 1.
- `blobSource` (BlobSource): The blob source to write.

**Returns:** `Integer` — The number of characters written.

---

### setString(position, blobSource, offset, len)

Returns: `Integer`

Convenience method for writing a `JdbcClob` to a clob.

**Parameters:**
- `position` (Integer): The position at which writing to the clob starts; the first position is 1.
- `blobSource` (BlobSource): The blob source to write.
- `offset` (Integer): The offset into the provided string where reading characters to write starts.
- `len` (Integer): The number of characters to write.

**Returns:** `Integer` — The number of characters written.

---

### setString(position, value)

Returns: `Integer`

For documentation of this method, see `java.sql.Clob#setString(long, String)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#setString(long,%20java.lang.String)).

**Parameters:**
- `position` (Integer): The position at which writing to the clob starts; the first position is 1.
- `value` (String): The string to write.

**Returns:** `Integer` — The number of characters written.

---

### setString(position, value, offset, len)

Returns: `Integer`

For documentation of this method, see `java.sql.Clob#setString(long, String, int, int)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#setString(long,%20java.lang.String,%20int,%20int)).

**Parameters:**
- `position` (Integer): The position at which writing to the clob starts; the first position is 1.
- `value` (String): The string to write.
- `offset` (Integer): The offset into the provided string where reading characters to write starts.
- `len` (Integer): The number of characters to write.

**Returns:** `Integer` — The number of characters written.

---

### truncate(length)

Returns: `void`

For documentation of this method, see `java.sql.Clob#truncate(long)` (https://docs.oracle.com/javase/6/docs/api/java/sql/Clob.html#truncate(long)).

**Parameters:**
- `length` (Integer): The size (in bytes) of this clob after truncation.

## Properties

None.
