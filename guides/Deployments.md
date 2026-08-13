# Create and manage deployments

A Google Apps Script project deployment is a release of your script that is
available for use as a web app, Google Workspace add-on, or API executable.
By creating and managing deployments, you can iterate on your code and control
which script [version](https://developers.google.com/apps-script/guides/versions) users access.

There are two types of deployments:

- *Head deployments*, which always sync to the current project code.
- *Versioned deployments*, which connect to a specific project version.

## Head deployments

A head deployment is the current project code. When you create a
Apps Script project, the system automatically creates a head
deployment for that project.

The head deployment always syncs with the most recently saved code. For
example, if you create a versioned deployment and then modify your code, the
head deployment reflects those changes while the versioned deployment remains
intact.

Use head deployments to test code. Don't use head deployments for public use.

There is only one head deployment for each Apps Script project. To
use a head deployment, you must have at least read access to the script
project.

## Versioned deployments

A versioned deployment makes a specific version of the project code available.
This lets users continue to use a functioning version while you make changes
and improvements to the code.

When you publish an application for public use, always use a versioned
deployment. You can have multiple active versioned deployments at once.

**Important**: You cannot transfer ownership of versioned deployments. If you
transfer ownership of a script project, the owner of the existing versioned
deployments doesn't change. If an administrator deletes the deployment owner's
account, their deployments might experience script errors.

## Deployments versus versions

A *version* and a *deployment* are distinct concepts in
Apps Script:

- **[Version](https://developers.google.com/apps-script/guides/versions)**: A static snapshot of your script project's code. Once created, a version is immutable. Think of a version as a "save point" in your development history.
- **Deployment**: A release that makes a specific version of your script available for users. A deployment has a unique URL or ID.

When you want to update the code used by an existing deployment (like a web
app), you create a new **version** and then
[edit the deployment](https://developers.google.com/apps-script/concepts/deployments#edit-versioned) to point to that new version. This
updates the application for all users while maintaining the same URL or
deployment ID.

## Create a versioned deployment

To deploy a version of an add-on,
Editor add-on, Chat app, or an API
executable, you must first [switch your Apps Script's
Google Cloud project association from the default project to a standard
project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

To create a versioned deployment:

1. Open the Apps Script project.
2. At the top right, click **Deploy** \> **New deployment**.
3. Next to **Select type** click Enable deployment types .
4. Select the deployment type that you want to deploy. For Google Workspace add-ons, Editor add-ons, and Google Chat apps, select **Add-on**.
5. Enter the information about your deployment and click **Deploy**.

Each new deployment can be shared as a library. If you share the script as a
library, the deployment description is visible to library users.

## View versioned deployments

To view the deployments of a Apps Script project, at the top,
click **Deploy** \> **Manage deployments**.

To view the code of a specific version, refer to
[View a previous version](https://developers.google.com/apps-script/guides/versions#view-script).

## Edit a versioned deployment

You can edit a versioned deployment to change its description or version. To
edit a deployment:

1. Open the Apps Script project.
2. Click **Deploy** \> **Manage deployments**.
3. Select the active deployment and click **Edit** .
4. Make your changes and click **Deploy**.

To edit an archived deployment, redeploy it and then follow the preceding
steps.

To deploy a change to the project code, create a new **version** and edit the
deployment to use it. This is the standard way to update your application
without changing its URL or deployment ID. The deployment automatically uses the
new version for all users.

## Find a deployment ID

Every deployment has an associated string ID. To find this ID:

1. Open the Apps Script project.
2. At the top right, click **Deploy** \> **Manage deployments**.
3. Select an active deployment to find its ID.

Deployment IDs only appear on active deployments.

## Test a deployment

The method for testing a deployment depends on the type of app you build.
**Google Workspace add-on**

To test a add-on deployment, see
[Testing add-ons](https://developers.google.com/workspace/add-ons/how-tos/testing-workspace-addons).
**Editor add-on**

To test an Editor add-on deployment, see
[Test an Editor add-on](https://developers.google.com/workspace/add-ons/how-tos/testing-editor-addons).
**Web app**

To test a web app deployment, see
[Test a web app deployment](https://developers.google.com/apps-script/guides/web#test_a_web_app_deployment).
**Google Chat app**

To test a Chat app deployment,
[create a versioned deployment](https://developers.google.com/apps-script/concepts/deployments#versioned-deployments) of the script to access its deployment ID.

After you have the deployment ID, specify the ID in the
[Chat API configuration](https://developers.google.com/workspace/chat/receive-respond-interactions#configure)
and follow the steps to
[test interactive
features](https://developers.google.com/workspace/chat/test-interactive-features).
**API Executable**

To test an API executable deployment,
[create a versioned deployment](https://developers.google.com/apps-script/concepts/deployments#create-versioned). After you
create a deployment, follow these steps:

1. At the top right of the Apps Script project, click **Deploy \> Test
   deployments**.
2. Next to "Select type," click ![The enable deployment types icon](https://fonts.gstatic.com/s/i/googlematerialicons/settings/v7/24px.svg) **\> API Executable**.
3. Copy and use the URL to test your API Executable deployment.

## Archive a versioned deployment

You can't delete versioned deployments from your record of deployments.
Instead, you can archive them.

To archive a versioned deployment:

1. Open the Apps Script project.
2. Click **Deploy** \> **Manage deployments**.
3. Select the deployment and click **Archive deployment** .

## Delete a version from project history

While you can't delete versioned deployments, you can delete the script
versions they use from your project history. To delete a version, it must not
be in use by an active deployment.

To delete a version, refer to
[Delete versions](https://developers.google.com/apps-script/guides/versions#delete-version).

## Redeploy an archived deployment

1. Open the Apps Script project.
2. At the top right, click **Deploy** \> **Manage deployments**.
3. Under **Archived** , select the deployment and click **Edit** \> **Deploy**.