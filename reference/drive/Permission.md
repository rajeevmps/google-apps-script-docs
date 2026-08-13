# Permission

An enum representing the permissions granted to users who can access a file or folder.

An enum representing the permissions granted to users who can access a file or folder, besides any individual users who have been explicitly given access.

These properties are accessible via `DriveApp.Permission`.

## Properties

| Value | Description |
|-------|-------------|
| `VIEW` | Users who can access the file or folder are able only to view it or copy it. Passing this value to `File.setSharing(accessType, permissionType)` throws an exception if the type of file does not support it. |
| `EDIT` | Users who can access the file or folder are able to edit it. Unless `File.setShareableByEditors(shareable)` is set to `false`, users can also change the sharing settings. Passing this value to `File.setSharing(accessType, permissionType)` throws an exception if the type of file does not support it. |
| `COMMENT` | Users who can access the file or folder are able only to view it, copy it, or comment on it. Passing this value to `File.setSharing(accessType, permissionType)` throws an exception if the type of file does not support it. |
| `OWNER` | The user owns the file or folder. This value can be returned, but passing it to `File.setSharing(accessType, permissionType)` throws an exception. |
| `ORGANIZER` | Users who can organize files and folders within a shared drive. This value can be returned, but passing it to `File.setSharing(accessType, permissionType)` throws an exception. |
| `FILE_ORGANIZER` | Users who can edit, trash, and move content within a shared drive. This value can be returned, but passing it to `File.setSharing(accessType, permissionType)` throws an exception. |
| `NONE` | The user does not have any permissions for the file or folder. This value can be returned, but passing it to `File.setSharing(accessType, permissionType)` throws an exception unless it is set in combination with `Access.ANYONE`. |
