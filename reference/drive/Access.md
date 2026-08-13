# Access

An enum representing classes of users who can access a file or folder.

An enum representing classes of users who can access a file or folder, besides any individual users who have been explicitly given access.

These properties are accessed via `DriveApp.Access` followed by the specific access property (e.g., `DriveApp.Access.ANYONE`).

## Properties

| Value | Description |
|-------|-------------|
| `ANYONE` | Anyone on the Internet can find and access. No sign-in required. Domain administrators can prohibit this setting for users of a Google Workspace domain. If the setting is disabled, passing this value to `File.setSharing(accessType, permissionType)` throws an exception. |
| `ANYONE_WITH_LINK` | Anyone who has the link can access. No sign-in required. Domain administrators can prohibit this setting for users of a Google Workspace domain. If the setting is disabled, passing this value to `File.setSharing(accessType, permissionType)` throws an exception. |
| `DOMAIN` | People in your domain can find and access. Sign-in required. This setting is available only for users of a Google Workspace domain. For other types of Google accounts, passing this value to `File.setSharing(accessType, permissionType)` throws an exception. |
| `DOMAIN_WITH_LINK` | People in your domain who have the link can access. Sign-in required. This setting is available only for users of a Google Workspace domain. For other types of Google accounts, passing this value to `File.setSharing(accessType, permissionType)` throws an exception. |
| `PRIVATE` | Only people explicitly granted permission can access. Sign-in required. |
