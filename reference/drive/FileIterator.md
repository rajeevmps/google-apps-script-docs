# FileIterator

An iterator that allows scripts to iterate over a potentially large collection of files.

An iterator that allows scripts to iterate over a potentially large collection of files. File iterators can be accessed from `DriveApp` or a `Folder`.

```javascript
// Log the name of every file in the user's Drive.
const files = DriveApp.getFiles();
while (files.hasNext()) {
  const file = files.next();
  Logger.log(file.getName());
}
```

## Methods

### getContinuationToken()
**Return type:** `String`

Gets a token that can be used to resume this iteration at a later time. This method is useful if processing an iterator in one execution exceeds the maximum execution time. Continuation tokens are generally valid for one week.

Returns: A continuation token that can be used to resume this iteration with the items that remained in the iterator when the token was generated.

### hasNext()
**Return type:** `Boolean`

Determines whether calling `next()` returns an item.

Returns: `true` if `next()` returns an item; `false` if not.

### next()
**Return type:** `File`

Gets the next item in the collection of files or folders. Throws an exception if no items remain.

Returns: The next item in the collection.
