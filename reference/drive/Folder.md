# Folder

A folder in Google Drive.

A folder in Google Drive. Folders can be accessed or created from `DriveApp`.

## Methods

### addEditor(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Adds the given user to the list of editors for the `Folder`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditor(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Adds the given user to the list of editors for the `Folder`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditors(emailAddresses)
**Parameters:** `emailAddresses` (String[])
**Return type:** `Folder`

Adds the given array of users to the list of editors for the `Folder`. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

### addViewer(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Adds the given user to the list of viewers for the `Folder`. If the user was already on the list of editors, this method has no effect.

### addViewer(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Adds the given user to the list of viewers for the `Folder`. If the user was already on the list of editors, this method has no effect.

### addViewers(emailAddresses)
**Parameters:** `emailAddresses` (String[])
**Return type:** `Folder`

Adds the given array of users to the list of viewers for the `Folder`. If any of the users were already on the list of editors, this method has no effect for them.

### createFile(blob)
**Parameters:** `blob` (BlobSource)
**Return type:** `File`

Creates a file in the current folder from a given `Blob` of arbitrary data.

### createFile(name, content)
**Parameters:** `name` (String), `content` (String)
**Return type:** `File`

Creates a text file in the current folder with the given name and contents. Throws an exception if `content` is larger than 50 MB.

### createFile(name, content, mimeType)
**Parameters:** `name` (String), `content` (String), `mimeType` (String)
**Return type:** `File`

Creates a file in the current folder with the given name, contents, and MIME type. Throws an exception if `content` is larger than 10MB.

### createFolder(name)
**Parameters:** `name` (String)
**Return type:** `Folder`

Creates a folder in the current folder with the given name.

### createShortcut(targetId)
**Parameters:** `targetId` (String)
**Return type:** `File`

Creates a shortcut to the provided Drive item ID, and returns it.

### createShortcutForTargetIdAndResourceKey(targetId, targetResourceKey)
**Parameters:** `targetId` (String), `targetResourceKey` (String)
**Return type:** `File`

Creates a shortcut to the provided Drive item ID and resource key, and returns it. A resource key is an additional parameter that needs to be passed to access the target file or folder that has been shared using a link.

### getAccess(email)
**Parameters:** `email` (String)
**Return type:** `Permission`

Gets the permission granted to a specific user. The method doesn't support returning permissions for a Google Group or permissions inherited through Google Groups.

### getAccess(user)
**Parameters:** `user` (User)
**Return type:** `Permission`

Gets the permission granted to a specific user. The method doesn't support returning permissions for a Google Group or permissions inherited through Google Groups.

### getDateCreated()
**Return type:** `Date`

Gets the date the `Folder` was created.

### getDescription()
**Return type:** `String`

Gets the description for the `Folder`.

### getEditors()
**Return type:** `User[]`

Gets the list of editors for this `Folder`. If the user who executes the script does not have edit access to the `Folder`, this method returns an empty array.

### getFiles()
**Return type:** `FileIterator`

Gets a collection of all files that are children of the current folder.

### getFilesByName(name)
**Parameters:** `name` (String)
**Return type:** `FileIterator`

Gets a collection of all files that are children of the current folder and have the given name.

### getFilesByType(mimeType)
**Parameters:** `mimeType` (String)
**Return type:** `FileIterator`

Gets a collection of all files that are children of the current folder and have the given MIME type.

### getFolders()
**Return type:** `FolderIterator`

Gets a collection of all folders that are children of the current folder.

### getFoldersByName(name)
**Parameters:** `name` (String)
**Return type:** `FolderIterator`

Gets a collection of all folders that are children of the current folder and have the given name.

### getId()
**Return type:** `String`

Gets the ID of the `Folder`.

### getLastUpdated()
**Return type:** `Date`

Gets the date the `Folder` was last updated.

### getName()
**Return type:** `String`

Gets the name of the `Folder`.

### getOwner()
**Return type:** `User`

Gets the owner of this `Folder`.

### getParents()
**Return type:** `FolderIterator`

Gets a collection of folders that are immediate parents of the `Folder`.

### getResourceKey()
**Return type:** `String`

Gets the resource key of the `Folder` that is required to access items that have been shared using a link.

### getSecurityUpdateEligible()
**Return type:** `Boolean`

Gets whether this `Folder` is eligible to apply the security update that requires a resource key for access when it's shared using a link.

### getSecurityUpdateEnabled()
**Return type:** `Boolean`

Gets whether this `Folder` requires a resource key for access when it's shared using a link.

### getSharingAccess()
**Return type:** `Access`

Gets which class of users can access the `Folder`, besides any individual users who have been explicitly given access.

### getSharingPermission()
**Return type:** `Permission`

Gets the permission granted to those users who can access the `Folder`, besides any individual users who have been explicitly given access.

### getSize()
**Return type:** `Integer`

Gets the number of bytes used to store the `Folder` in Drive.

### getUrl()
**Return type:** `String`

Gets the URL that can be used to open the `Folder` in a Google App like Drive or Docs.

### getViewers()
**Return type:** `User[]`

Gets the list of viewers and commenters for this `Folder`.

### isShareableByEditors()
**Return type:** `Boolean`

Determines whether users with edit permissions to the `Folder` are allowed to share with other users or change the permissions.

### isStarred()
**Return type:** `Boolean`

Determines whether the `Folder` has been starred in the user's Drive.

### isTrashed()
**Return type:** `Boolean`

Determines whether the `Folder` is in the trash of the user's Drive.

### moveTo(destination)
**Parameters:** `destination` (Folder)
**Return type:** `Folder`

Moves this item to the provided destination folder.

### removeEditor(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Removes the given user from the list of editors for the `Folder`.

### removeEditor(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Removes the given user from the list of editors for the `Folder`.

### removeViewer(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Removes the given user from the list of viewers and commenters for the `Folder`.

### removeViewer(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Removes the given user from the list of viewers and commenters for the `Folder`.

### revokePermissions(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Revokes the access to the `Folder` granted to the given user.

### revokePermissions(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Revokes the access to the `Folder` granted to the given user.

### searchFiles(params)
**Parameters:** `params` (String)
**Return type:** `FileIterator`

Gets a collection of all files that are children of the current folder and match the given search criteria.

### searchFolders(params)
**Parameters:** `params` (String)
**Return type:** `FolderIterator`

Gets a collection of all folders that are children of the current folder and match the given search criteria.

### setDescription(description)
**Parameters:** `description` (String)
**Return type:** `Folder`

Sets the description for the `Folder`.

### setName(name)
**Parameters:** `name` (String)
**Return type:** `Folder`

Sets the name of the `Folder`.

### setOwner(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `Folder`

Changes the owner of the `Folder`.

### setOwner(user)
**Parameters:** `user` (User)
**Return type:** `Folder`

Changes the owner of the `Folder`.

### setSecurityUpdateEnabled(enabled)
**Parameters:** `enabled` (Boolean)
**Return type:** `Folder`

Sets whether the `Folder` requires a resource key for access when it's shared using a link.

### setShareableByEditors(shareable)
**Parameters:** `shareable` (Boolean)
**Return type:** `Folder`

Sets whether users with edit permissions to the `Folder` are allowed to share with other users or change the permissions.

### setSharing(accessType, permissionType)
**Parameters:** `accessType` (Access), `permissionType` (Permission)
**Return type:** `Folder`

Sets which class of users can access the `Folder` and what permissions those users are granted, besides any individual users who have been explicitly given access.

### setStarred(starred)
**Parameters:** `starred` (Boolean)
**Return type:** `Folder`

Sets whether the `Folder` is starred in the user's Drive.

### setTrashed(trashed)
**Parameters:** `trashed` (Boolean)
**Return type:** `Folder`

Sets whether the `Folder` is in the trash of the user's Drive.

### addFile(child) — Deprecated
**Parameters:** `child` (File)
**Return type:** `Folder`

Adds the given file to the current folder.

### addFolder(child) — Deprecated
**Parameters:** `child` (Folder)
**Return type:** `Folder`

Adds the given folder to the current folder.

### removeFile(child) — Deprecated
**Parameters:** `child` (File)
**Return type:** `Folder`

Removes the given file from the current folder.

### removeFolder(child) — Deprecated
**Parameters:** `child` (Folder)
**Return type:** `Folder`

Removes the given folder from the current folder.

## Code Samples

```javascript
const folders = DriveApp.getFolders();
while (folders.hasNext()) {
  const folder = folders.next();
  Logger.log(folder.getName());
}
```

```javascript
DriveApp.getRootFolder().createFile('New Text File', 'Hello, world!');
```

```javascript
DriveApp.getRootFolder().createFile('New HTML File', '<b>Hello, world!</b>', MimeType.HTML);
```

```javascript
const folder = DriveApp.getFolderById('1234567890abcdefghijklmnopqrstuvwxyz');
const editors = folder.getEditors();
for (const editor of editors) {
  console.log(editor.getName());
}
```

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
