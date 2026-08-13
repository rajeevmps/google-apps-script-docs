# GmailAttachment

A GmailAttachment is a Blob with an extra getSize() method.

A GmailAttachment is a Blob with an extra `getSize()` method that is faster and does not count against the Gmail read quota.

```javascript
const threads = GmailApp.getInboxThreads(0, 100);
const msgs = GmailApp.getMessagesForThreads(threads);
for (let i = 0; i < msgs.length; i++) {
  for (let j = 0; j < msgs[i].length; j++) {
    const attachments = msgs[i][j].getAttachments();
    for (let k = 0; k < attachments.length; k++) {
      Logger.log(
          'Message "%s" contains the attachment "%s" (%s bytes)',
          msgs[i][j].getSubject(),
          attachments[k].getName(),
          attachments[k].getSize(),
      );
    }
  }
}
```

## Methods

### copyBlob()
**Return type:** `Blob`

Returns a copy of this blob.

### getAs(contentType)
**Parameters:** `contentType` (String)
**Return type:** `Blob`

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. For most blobs, `'application/pdf'` is valid. For images in BMP, GIF, JPEG, or PNG format, corresponding MIME types are valid. For Google Docs, `'text/markdown'` is also valid.

### getBytes()
**Return type:** `Byte[]`

Gets the data stored in this blob.

### getContentType()
**Return type:** `String|null`

Gets the content type of the bytes in this blob.

### getDataAsString()
**Return type:** `String`

Gets the data of this blob as a String with UTF-8 encoding.

### getDataAsString(charset)
**Parameters:** `charset` (String)
**Return type:** `String`

Gets the data of this blob as a string with the specified encoding.

### getHash()
**Return type:** `String`

Gets the SHA1 content hash for this attachment. This method does not count against the Gmail read quota.

### getName()
**Return type:** `String|null`

Gets the name of this blob.

### getSize()
**Return type:** `Integer`

Gets the size of this attachment. This method is faster than calling `getBytes().length` and does not count against the Gmail read quota.

### isGoogleType()
**Return type:** `Boolean`

Returns whether this blob is a Google Workspace file (Sheets, Docs, etc.).

### setBytes(data)
**Parameters:** `data` (Byte[])
**Return type:** `Blob`

Sets the data stored in this blob.

### setContentType(contentType)
**Parameters:** `contentType` (String)
**Return type:** `Blob`

Sets the content type of the bytes in this blob.

### setContentTypeFromExtension()
**Return type:** `Blob`

Sets the content type of the bytes in this blob based on the file extension. The contentType is `null` if it cannot be guessed from its extension.

### setDataFromString(string)
**Parameters:** `string` (String)
**Return type:** `Blob`

Sets the data of this blob from a string with UTF-8 encoding.

### setDataFromString(string, charset)
**Parameters:** `string` (String), `charset` (String)
**Return type:** `Blob`

Sets the data of this blob from a string with the specified encoding.

### setName(name)
**Parameters:** `name` (String)
**Return type:** `Blob`

Sets the name of this blob.

### getAllBlobs() — Deprecated
**Return type:** `Blob[]`

Gets all the blobs that are contained within this (possibly composite) blob.
