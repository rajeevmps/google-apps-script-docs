# Advanced Drive Service

Source: https://developers.google.com/apps-script/advanced/drive

## Overview

The Advanced Drive Service enables Google Apps Script to interact with the Google Drive API for comprehensive file and folder manipulation. As noted in the documentation, "this advanced service provides a few extra features, including access to custom file properties as well as revisions for files and folders."

## Key Capabilities

This service extends beyond the built-in Drive service by offering:
- Custom file properties management
- File revision tracking
- Direct Drive API v3 access
- Advanced permission handling

## Enabling the Service

The advanced Drive service must be activated before use through the Apps Script development environment's advanced services settings.

## Core Operations

### File Upload
Scripts can save files to user Drive storage by specifying metadata and providing blob content through the `Drive.Files.create()` method.

### Folder Management
Creating directories requires setting MIME type to `application/vnd.google-apps.folder` and using the Files.create operation.

### File Search
The service supports query-based file discovery using the `Drive.Files.list()` method with filter parameters.

### Revision History
Access file change history through the `Drive.Revisions.list()` method, which returns modification timestamps and file sizes across versions.

### Custom Properties
The `appProperties` field stores script-only metadata, while the `properties` field creates cross-application visible custom properties.

### Permission Management
Add users as editors or viewers via `Drive.Permissions.create()` with optional email notification suppression.

## Reference Documentation

Complete method signatures and parameters align with the [official Drive API v3 reference](https://developers.google.com/drive/api/reference/rest/v3) (external — not scraped). JavaScript reserved words like `delete` are renamed (e.g., `remove`) in the Apps Script implementation.
</content>
