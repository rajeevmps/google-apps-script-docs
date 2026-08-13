# Manage versions

## Page Summary

- This section describes Apps Script API methods for managing script project versions.
- You can use methods to create, list, and read project code versions.
- API methods return `Version` objects containing configuration details like version number and description.
- To read the code of a specific version, use a `projects.getContent` request.

This section provides an overview of the Google Apps Script API methods you can use to create a new project code [version](https://developers.google.com/apps-script/guides/versions), read version information, or list all existing versions.

**Note:** These methods return one or more [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) objects which contain version configuration information such as the version number and description. You can read the code attached to a specific version using a [`projects.getContent`](https://developers.google.com/apps-script/api/reference/rest/v1/projects/getContent) request.

## API method overview

### Create a version

[projects.versions.create](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/create)

**Results**: Create a new, immutable version of a script project's code. The project's current saved code is used for the version. This creates a code "snapshot" you can read later or use in a specific [deployment](https://developers.google.com/apps-script/concepts/deployments). Returns a [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) object, containing the version configuration details.

### List a project's versions

[projects.versions.list](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/list)

**Results**: Returns an array of [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) objects, each representing one of the versions of the script project.

### Read a version

[projects.versions.get](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions/get)

**Results**: Returns a [`Version`](https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions#Version) that represents a specific version of a script project.

Source: https://developers.google.com/apps-script/api/how-tos/manage-versions
