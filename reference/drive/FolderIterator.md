# FolderIterator

An object that allows scripts to iterate over a potentially large collection of folders.

An object that allows scripts to iterate over a potentially large collection of folders. Folder iterators can be accessed from `DriveApp`, a `File`, or a `Folder`.

```javascript
// Log the name of every folder in the user's Drive.
const folders = DriveApp.getFolders();
while (folders.hasNext()) {
  const folder = folders.next();
  Logger.log(folder.getName());
}
```

## Methods

### getContinuationToken()
**Return type:** `String`

Gets a token that can be used to resume this iteration at a later time. This method is useful if processing an iterator in one execution exceeds the maximum execution time. Continuation tokens are generally valid for one week.

Returns: A continuation token that can be used to resume this iteration at a later time with the items that remained in the iterator when the token was generated.

### hasNext()
**Return type:** `Boolean`

Determines whether calling `next()` returns an item.

Returns: `true` if `next()` returns an item; `false` if not.

### next()
**Return type:** `Folder`

Gets the next item in the collection of files or folders. Throws an exception if no items remain.

Returns: The next item in the collection.
