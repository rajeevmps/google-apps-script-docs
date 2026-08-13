# File

A file in Google Drive.

A file in Google Drive. Files can be accessed or created from `DriveApp`.

## Methods

### addCommenter(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Add the given user to the list of commenters for the `File`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addCommenter(user)
**Parameters:** `user` (User)
**Return type:** `File`

Add the given user to the list of commenters for the `File`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addCommenters(emailAddresses)
**Parameters:** `emailAddresses` (String[])
**Return type:** `File`

Add the given array of users to the list of commenters for the `File`. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

### addEditor(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Adds the given user to the list of editors for the `File`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditor(user)
**Parameters:** `user` (User)
**Return type:** `File`

Adds the given user to the list of editors for the `File`. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

### addEditors(emailAddresses)
**Parameters:** `emailAddresses` (String[])
**Return type:** `File`

Adds the given array of users to the list of editors for the `File`. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

### addViewer(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Adds the given user to the list of viewers for the `File`. If the user was already on the list of editors, this method has no effect.

### addViewer(user)
**Parameters:** `user` (User)
**Return type:** `File`

Adds the given user to the list of viewers for the `File`. If the user was already on the list of editors, this method has no effect.

### addViewers(emailAddresses)
**Parameters:** `emailAddresses` (String[])
**Return type:** `File`

Adds the given array of users to the list of viewers for the `File`. If any of the users were already on the list of editors, this method has no effect for them.

### getAccess(email)
**Parameters:** `email` (String)
**Return type:** `Permission`

Gets the permission granted to a specific user. The method doesn't support returning permissions for a Google Group or permissions inherited through Google Groups.

### getAccess(user)
**Parameters:** `user` (User)
**Return type:** `Permission`

Gets the permission granted to a specific user. The method doesn't support returning permissions for a Google Group or permissions inherited through Google Groups.

### getAs(contentType)
**Parameters:** `contentType` (String)
**Return type:** `Blob`

Return the data inside this object as a blob converted to the specified content type. This method adds the appropriate extension to the filename—for example, "myfile.pdf". However, it assumes that the part of the filename that follows the last period (if any) is an existing extension that should be replaced. Consequently, "ShoppingList.12.25.2014" becomes "ShoppingList.12.25.pdf". To view the daily quotas for conversions, see Quotas for Google Services. Newly created Google Workspace domains might be temporarily subject to stricter quotas.

### getBlob()
**Return type:** `Blob`

Return the data inside this object as a blob.

### getDateCreated()
**Return type:** `Date`

Gets the date the `File` was created.

### getDescription()
**Return type:** `String`

Gets the description for the `File`.

### getDownloadUrl()
**Return type:** `String`

Gets the URL that can be used to download the file. Only users with permission to open the file in Google Drive can access the URL. You can use this URL in a browser to download the file, but you can't use to fetch the file with `UrlFetchApp`. If you want the contents of the file in the script, use `getBlob()`.

### getEditors()
**Return type:** `User[]`

Gets the list of editors for this `File`. If the user who executes the script does not have edit access to the `File`, this method returns an empty array.

### getId()
**Return type:** `String`

Gets the ID of the `File`.

### getLastUpdated()
**Return type:** `Date`

Gets the date the `File` was last updated.

### getMimeType()
**Return type:** `String`

Gets the MIME type of the file.

### getName()
**Return type:** `String`

Gets the name of the `File`.

### getOwner()
**Return type:** `User`

Gets the file owner.

### getParents()
**Return type:** `FolderIterator`

Gets a collection of folders that are immediate parents of the `File`.

### getResourceKey()
**Return type:** `String`

Gets the resource key of the `File` that is required to access items that have been shared using a link.

### getSecurityUpdateEligible()
**Return type:** `Boolean`

Gets whether this `File` is eligible to apply the security update that requires a resource key for access when it's shared using a link.

### getSecurityUpdateEnabled()
**Return type:** `Boolean`

Gets whether this `File` requires a resource key for access when it's shared using a link.

### getSharingAccess()
**Return type:** `Access`

Gets which class of users can access the `File`, besides any individual users who have been explicitly given access.

### getSharingPermission()
**Return type:** `Permission`

Gets the permission granted to those users who can access the `File`, besides any individual users who have been explicitly given access.

### getSize()
**Return type:** `Integer`

Gets the number of bytes used to store the `File` in Drive.

### getTargetId()
**Return type:** `String|null`

If this is a Shortcut, returns the ID of the item it points to.

### getTargetMimeType()
**Return type:** `String|null`

If this is a Shortcut, returns the mime type of the item it points to.

### getTargetResourceKey()
**Return type:** `String|null`

If the file is a shortcut, returns the resource key of the item it points to.

### getThumbnail()
**Return type:** `Blob|null`

Gets a thumbnail image for the file, or `null` if no thumbnail exists.

### getUrl()
**Return type:** `String`

Gets the URL that can be used to open the `File` in a Google App like Drive or Docs.

### getViewers()
**Return type:** `User[]`

Gets the list of viewers and commenters for this `File`.

### isShareableByEditors()
**Return type:** `Boolean`

Determines whether users with edit permissions to the `File` are allowed to share with other users or change the permissions.

### isStarred()
**Return type:** `Boolean`

Determines whether the `File` has been starred in the user's Drive.

### isTrashed()
**Return type:** `Boolean`

Determines whether the `File` is in the trash of the user's Drive.

### makeCopy()
**Return type:** `File`

Creates a copy of the file.

### makeCopy(destination)
**Parameters:** `destination` (Folder)
**Return type:** `File`

Creates a copy of the file in the destination directory.

### makeCopy(name)
**Parameters:** `name` (String)
**Return type:** `File`

Creates a copy of the file and names it with the name provided.

### makeCopy(name, destination)
**Parameters:** `name` (String), `destination` (Folder)
**Return type:** `File`

Creates a copy of the file in the destination directory and names it with the name provided.

### moveTo(destination)
**Parameters:** `destination` (Folder)
**Return type:** `File`

Moves this item to the provided destination folder.

### removeCommenter(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Removes the given user from the list of commenters for the `File`.

### removeCommenter(user)
**Parameters:** `user` (User)
**Return type:** `File`

Removes the given user from the list of commenters for the `File`.

### removeEditor(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Removes the given user from the list of editors for the `File`.

### removeEditor(user)
**Parameters:** `user` (User)
**Return type:** `File`

Removes the given user from the list of editors for the `File`.

### removeViewer(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Removes the given user from the list of viewers and commenters for the `File`.

### removeViewer(user)
**Parameters:** `user` (User)
**Return type:** `File`

Removes the given user from the list of viewers and commenters for the `File`.

### revokePermissions(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Revokes the access to the `File` granted to the given user.

### revokePermissions(user)
**Parameters:** `user` (User)
**Return type:** `File`

Revokes the access to the `File` granted to the given user.

### setContent(content)
**Parameters:** `content` (String)
**Return type:** `File`

Overwrites the content of the file with a given replacement.

### setDescription(description)
**Parameters:** `description` (String)
**Return type:** `File`

Sets the description for the `File`.

### setName(name)
**Parameters:** `name` (String)
**Return type:** `File`

Sets the name of the `File`.

### setOwner(emailAddress)
**Parameters:** `emailAddress` (String)
**Return type:** `File`

Changes the owner of the `File`.

### setOwner(user)
**Parameters:** `user` (User)
**Return type:** `File`

Changes the owner of the `File`.

### setSecurityUpdateEnabled(enabled)
**Parameters:** `enabled` (Boolean)
**Return type:** `File`

Sets whether the `File` requires a resource key for access when it's shared using a link.

### setShareableByEditors(shareable)
**Parameters:** `shareable` (Boolean)
**Return type:** `File`

Sets whether users with edit permissions to the `File` are allowed to share with other users or change the permissions.

### setSharing(accessType, permissionType)
**Parameters:** `accessType` (Access), `permissionType` (Permission)
**Return type:** `File`

Sets which class of users can access the `File` and what permissions those users are granted, besides any individual users who have been explicitly given access.

### setStarred(starred)
**Parameters:** `starred` (Boolean)
**Return type:** `File`

Sets whether the `File` is starred in the user's Drive.

### setTrashed(trashed)
**Parameters:** `trashed` (Boolean)
**Return type:** `File`

Sets whether the `File` is in the trash of the user's Drive.
