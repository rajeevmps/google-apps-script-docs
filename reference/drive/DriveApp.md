# DriveApp

Allows scripts to create, find, and modify files and folders in Google Drive.

Allows scripts to create, find, and modify files and folders in Google Drive. Although the built-in Drive service is easier to use, it has some limitations. For the most up-to-date features and support, and to access files or folders in shared drives, use the advanced Drive service.

## Methods

### continueFileIterator(continuationToken)
**Parameters:** `continuationToken` (String)
**Return type:** `FileIterator`

Resumes a file iteration using a continuation token from a previous iterator. This method is useful if processing an iterator in one execution exceeds the maximum execution time. Continuation tokens are generally valid for one week.

```javascript
const previousIterator = DriveApp.getFilesByName('Untitled document');
const continuationToken = previousIterator.getContinuationToken();
const newIterator = DriveApp.continueFileIterator(continuationToken);
if (newIterator.hasNext()) {
  const file = newIterator.next();
  console.log(file.getName());
}
```

### continueFolderIterator(continuationToken)
**Parameters:** `continuationToken` (String)
**Return type:** `FolderIterator`

Resumes a folder iteration using a continuation token from a previous iterator. This method is useful if processing an iterator in one execution exceeds the maximum execution time. Continuation tokens are generally valid for one week.

```javascript
const previousIterator = DriveApp.getFolders();
const continuationToken = previousIterator.getContinuationToken();
const newIterator = DriveApp.continueFolderIterator(continuationToken);
if (newIterator.hasNext()) {
  const folder = newIterator.next();
  console.log(folder.getName());
}
```

### createFile(blob)
**Parameters:** `blob` (BlobSource)
**Return type:** `File`

Creates a file in the root of the user's Drive from a given Blob of arbitrary data.

### createFile(name, content)
**Parameters:** `name` (String), `content` (String)
**Return type:** `File`

Creates a text file in the root of the user's Drive with the given name and contents. Throws an exception if content is larger than 50 MB.

```javascript
DriveApp.createFile('New Text File', 'Hello, world!');
```

### createFile(name, content, mimeType)
**Parameters:** `name` (String), `content` (String), `mimeType` (String)
**Return type:** `File`

Creates a file in the root of the user's Drive with the given name, contents, and MIME type. Throws an exception if content is larger than 10MB.

```javascript
DriveApp.createFile('New HTML File', '<b>Hello, world!</b>', MimeType.HTML);
```

### createFolder(name)
**Parameters:** `name` (String)
**Return type:** `Folder`

Creates a folder in the root of the user's Drive with the given name.

### createShortcut(targetId)
**Parameters:** `targetId` (String)
**Return type:** `File`

Creates a shortcut to the provided Drive item ID, and returns it.

### createShortcutForTargetIdAndResourceKey(targetId, targetResourceKey)
**Parameters:** `targetId` (String), `targetResourceKey` (String)
**Return type:** `File`

Creates a shortcut to the provided Drive item ID and resource key, and returns it. A resource key is an additional parameter that needs to be passed to access the target file or folder that has been shared using a link.

```javascript
const folders = DriveApp.getFoldersByName('Test-Folder');
while (folders.hasNext()) {
  const folder = folders.next();
  DriveApp.createShortcutForTargetIdAndResourceKey(
      folder.getId(),
      folder.getResourceKey(),
  );
}
```

### enforceSingleParent(value)
**Parameters:** `value` (Boolean)
**Return type:** `void`

Enables or disables enforceSingleParent behavior for all calls affecting item parents.

```javascript
DriveApp.enforceSingleParent(true);
```

### getFileById(id)
**Parameters:** `id` (String)
**Return type:** `File`

Gets the file with the given ID. Throws a scripting exception if the file does not exist or the user does not have permission to access it.

```javascript
const files = DriveApp.getFilesByName('Test');
if (files.hasNext()) {
  const fileId = files.next().getId();
  console.log(DriveApp.getFileById(fileId).getName());
}
```

### getFileByIdAndResourceKey(id, resourceKey)
**Parameters:** `id` (String), `resourceKey` (String)
**Return type:** `File`

Gets the file with the given ID and resource key. Resource keys are an additional parameter which need to be passed to access files that have been shared using a link. Throws a scripting exception if the file doesn't exist or the user doesn't have permission to access it.

```javascript
const files = DriveApp.getFilesByName('Test');
if (files.hasNext()) {
  const file = files.next();
  const key = file.getResourceKey();
  const id = file.getId();
  console.log(DriveApp.getFileByIdAndResourceKey(id, key).getName());
}
```

### getFiles()
**Return type:** `FileIterator`

Gets a collection of all files in the user's Drive.

### getFilesByName(name)
**Parameters:** `name` (String)
**Return type:** `FileIterator`

Gets a collection of all files in the user's Drive that have the given name.

### getFilesByType(mimeType)
**Parameters:** `mimeType` (String)
**Return type:** `FileIterator`

Gets a collection of all files in the user's Drive that have the given MIME type.

### getFolderById(id)
**Parameters:** `id` (String)
**Return type:** `Folder`

Gets the folder with the given ID. Throws a scripting exception if the folder does not exist or the user does not have permission to access it.

### getFolderByIdAndResourceKey(id, resourceKey)
**Parameters:** `id` (String), `resourceKey` (String)
**Return type:** `Folder`

Gets the folder with the given ID and resource key. Resource keys are an additional parameter which need to be passed to access folders that have been shared using a link. Throws a scripting exception if the folder doesn't exist or the user doesn't have permission to access it.

### getFolders()
**Return type:** `FolderIterator`

Gets a collection of all folders in the user's Drive.

### getFoldersByName(name)
**Parameters:** `name` (String)
**Return type:** `FolderIterator`

Gets a collection of all folders in the user's Drive that have the given name.

### getRootFolder()
**Return type:** `Folder`

Gets the folder at the root of the user's Drive.

```javascript
console.log(DriveApp.getRootFolder().getName());
console.log(DriveApp.getRootFolder().getOwner().getName());
```

### getStorageLimit()
**Return type:** `Integer`

Gets the number of bytes the user is allowed to store in Drive.

```javascript
console.log(DriveApp.getStorageLimit());
```

### getStorageUsed()
**Return type:** `Integer`

Gets the number of bytes the user is currently storing in Drive.

```javascript
console.log(DriveApp.getStorageUsed());
```

### getTrashedFiles()
**Return type:** `FileIterator`

Gets a collection of all the files in the trash of the user's Drive.

```javascript
const trashFiles = DriveApp.getTrashedFiles();
while (trashFiles.hasNext()) {
  const file = trashFiles.next();
  console.log(file.getName());
}
```

### getTrashedFolders()
**Return type:** `FolderIterator`

Gets a collection of all the folders in the trash of the user's Drive.

### searchFiles(params)
**Parameters:** `params` (String)
**Return type:** `FileIterator`

Gets a collection of all files in the user's Drive that match the given search criteria.

### searchFolders(params)
**Parameters:** `params` (String)
**Return type:** `FolderIterator`

Gets a collection of all folders in the user's Drive that match the given search criteria.

### addFile(child) — Deprecated
**Parameters:** `child` (File)
**Return type:** `Folder`

Adds the given file to the root of the user's Drive.

### addFolder(child) — Deprecated
**Parameters:** `child` (Folder)
**Return type:** `Folder`

Adds the given folder to the root of the user's Drive.

### removeFile(child) — Deprecated
**Parameters:** `child` (File)
**Return type:** `Folder`

Removes the given file from the root of the user's Drive.

### removeFolder(child) — Deprecated
**Parameters:** `child` (Folder)
**Return type:** `Folder`

Removes the given folder from the root of the user's Drive.

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `Access` | `Access` | An enum representing classes of users who can access a file or folder, besides any individual users who have been explicitly given access. |
| `Permission` | `Permission` | An enum representing the permissions granted to users who can access a file or folder, besides any individual users who have been explicitly given access. |
