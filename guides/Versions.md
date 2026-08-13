# Versions

[Video](https://www.youtube.com/watch?v=JvYdGlNNPy8)

A version is a static copy of a script. Track changes with versions. Once
saved, a version is immutable. Use versions when working on a script that
goes through many changes and iterations. Script projects can have up to 200
versions.

A version is distinct from a **[deployment](https://developers.google.com/apps-script/concepts/deployments)**:

- **Version**: A snapshot of your code at a specific point in time.
- **Deployment**: A release that uses a specific version of your script. To update the code for an existing deployment, you create a new version and then edit the deployment to use it.

Create versions when writing a library. For more information, see
[Libraries](https://developers.google.com/apps-script/guides/libraries#creating-a-library).

## Create a version

A version is automatically created when you create a new deployment. Create a
new version from an existing deployment by opening your Script
project and taking these steps:

1. At the top, click **Deploy** \> **Manage
   deployments**.
2. Select the active deployment to create a new version for and click Edit .
3. In the **Version** section, select **New version**.
4. Click **Deploy**.

## View a previous version

To view a previously created version within your script project, take these
steps:

1. In your script project, click **Project History**.
2. Under **Project history**, select the version you want to view. To view the description of a version, hold the pointer over the version number.

## Compare a previous version to the current version

To compare a previously created version to the current, or head, version, take
these steps:

1. In your script project, click **Project History**.
2. Under **Project history**, select the version you want to view.
3. Turn on **Highlight changes**.

Depending on the changes since the selected version, the files list contains
the following markers:

| Marker | Type of change | Description |
|---|---|---|
|   | File added | This file is new in the current version. |
|   | File deleted | This file is no longer present in the current version. |
|   | File modified | This file has changes in the current version that weren't present in the selected version. To view the changes, click the filename. |

## Restore a previous version

You can't automatically restore a previous version of your script project.
However, you can manually copy code from a previous version into your current
project:

1. In your script project, click **Project History**.
2. Under **Project history**, select the version you want to restore.
3. The code for that version appears. Copy the code from files in that version.
4. To update current version, paste copied code into corresponding files in editor.
5. Click Save ![The Save button icon in the Apps Script editor](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/save/default/24px.svg).

## Delete versions

You can permanently delete versions if they're not in use by an active
deployment. To archive a deployment or change the version that an active
deployment uses, refer to
[Create and manage deployments](https://developers.google.com/apps-script/concepts/deployments).

### Delete a version

To delete one version at a time, take these steps:

1. In your script project, click **Project History**.
2. Next to the version you want to delete, click **More actions** \> **Delete this version** \> **Delete**.

### Delete multiple versions at once

To delete multiple versions at the same time, take these steps:

1. In your script project, click **Project History**.
2. Click ![](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/delete/default/24px.svg) **Bulk delete versions**. A dialog shows a list of versions to delete. Versions in use by an active deployment aren't included in the list.
3. Select the versions to delete and click **Delete**.
4. In the dialog, click **Delete**.