# Google Cloud projects

Every Google Apps Script project uses
[Google Cloud](https://cloud.google.com/) to manage authorization,
[advanced services](https://developers.google.com/apps-script/guides/services/advanced), and other details.
To configure and manage these settings, every Apps Script project
has an associated
[Google Cloud project](https://cloud.google.com/resource-manager/docs/creating-managing-projects).
Your script project can use a
[*default* project](https://developers.google.com/apps-script/guides/cloud-platform-projects#default_cloud_platform_projects) that
Apps Script automatically creates, or a
[*standard* project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects) that you create
yourself. In general, default projects are good for everyday
scripts, but you should use a standard project for any application that
is complex, commercial quality, or that you intend to publish.

You can [switch from a default project to a standard project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project)
at any time, but you can't switch back to use a default project. It's best
to select the Cloud project your script uses early in development.
Switching later can cause complications, like requiring your users to
re-authorize.

## Default Cloud projects

When you create an Apps Script project, it creates a default
Cloud project that operates in the background.

- For most scripts, you never need to see or adjust this default project. Apps Script handles the necessary interactions with Google Cloud. For example, if you activate an advanced service in the Apps Script editor, Apps Script activates the advanced service in the default Cloud project when you save the script project.
- For some scripts, you need to interact with the Google Cloud console. In these cases, your script must use a standard Cloud project. For example, to view Google Cloud logs in the Google Cloud console, your script must use a standard project.

By default, Cloud projects have an Identity and Access Management
(IAM) policy with one entry, a Google service account that acts as the owner of
the default project. The Google service account is
`appsdev-apps-dev-script-auth@system.gserviceaccount.com`.

### View or update default Cloud projects

Most users can't directly locate, view, or edit default projects in the
Google Cloud console. If you're an Admin, refer to [View default Google Cloud projects](https://developers.google.com/apps-script/guides/admin/view-cloud-projects#view_default_cloud_projects).

**If you created your script project before April 8, 2019**, you might use a
default project that you can access in the Google Cloud console. To access the
default project, go to the script project's settings and click the project
number.

### Delete default Cloud projects

If you're an administrator, you can delete default Cloud projects like
you would
standard Cloud projects. See
[View or edit default Cloud projects](https://developers.google.com/apps-script/guides/admin/view-cloud-projects#view_or_edit_default).

Non-administrators can't manually delete default projects. However, if you
delete the script project or switch to a standard project,
Apps Script deletes the default project attached to the script
along with its settings and information.

## Standard Cloud projects

Default Cloud projects are the best option for most script projects,
unless you need to manually configure the project.
In these situations, you must
[switch your script project to use a standard project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

The following sections describe when Apps Script requires a
standard project, its properties, and common tasks. Perform these
tasks only with standard projects.

### When Apps Script requires standard Cloud projects

You must use a standard project in the following situations:

- To publish your script project as an [Google Workspace add-on](https://developers.google.com/add-ons/overview) in the [Google Workspace Marketplace](https://developers.google.com/workspace/marketplace/overview).
- To [verify your script project's OAuth client](https://developers.google.com/apps-script/guides/client-verification).
- When you have an application that needs to execute functions in your script project using the [Google Apps Script API's `scripts.run`
  method](https://developers.google.com/apps-script/api/how-tos/execute).
- To view your script project's Google Cloud logs in the [Google Cloud console](https://console.cloud.google.com/). The Google Cloud console provides more tools for filtering and viewing logs, and can be more helpful than the simplified view provided by the [Apps Script dashboard](https://script.google.com/home/executions).
- To view your script project's error reports using [Error
  Reporting](https://developers.google.com/apps-script/guides/logging#error_reporting).
- To create a [file-open dialog](https://developers.google.com/apps-script/guides/dialogs#file-open_dialogs).
- When you need manual control over the project's Google Cloud settings.

### Standard Cloud project properties

Standard projects have the following properties:

- Access all of the Google Cloud settings for the project directly from the [Google Cloud console](https://console.cloud.google.com/). This lets you activate APIs, adjust authorization credentials, and configure other details.
- When you delete a script project or switch it to use another standard project, the original standard project remains and can be reused.
- When you activate an [advanced service](https://developers.google.com/apps-script/guides/services/advanced) in a script project, you must manually activate the corresponding API in the standard project.
- Multiple script projects and other apps can share the same standard project. If you intend to publish a script project to the [Marketplace](https://developers.google.com/workspace/marketplace/overview) as an [add-on](https://developers.google.com/workspace/add-ons/overview), it must have its own standard project. Published apps can't share Cloud projects with other apps.
- If you want to execute functions in a script project from another app using the [Apps Script API's `scripts.run`
  method](https://developers.google.com/apps-script/api/how-tos/execute), the script project and the calling application must share the same standard project.
- When Apps Script asks a user to authorize a script that uses a standard project, the Cloud project name is used to identify the script (not the script project name). For this reason, be sure to set an appropriate Cloud project name.

### Access a standard Cloud project

To access the standard project associated with your script project:

1. Open the Apps Script project.
2. At the left, click **Project Settings** .
3. Under **Google Cloud Project**, click the project number.

Find a standard project directly on the [Google Cloud console **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager).

### Activate an API in a standard Cloud project

To give an Apps Script application access to another Google API,
activate the API in the corresponding Cloud project:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. Click Menu \> **APIs \& Services**.
3. Click **Enable APIs and Services**.
4. In the search box, enter the API you want to activate and press **Enter**.
5. Click the API from the search results and then click **Enable**.

You might be prompted to accept the Terms of Service for [Google
APIs](https://developers.google.com/terms) or [Google Cloud](https://cloud.google.com/terms/). Review
the Terms of Service carefully before accepting them.

Depending on the application, you might need to configure the API by selecting
it in the **APIs \& Services** dashboard.

### Determine the ID \& number of a standard Cloud project

All Cloud projects have a name, ID, and number. You might need these
identifiers to configure services or complete other tasks.

To determine your standard project's ID and number:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. At the top-right, click More \> **Project settings**.
3. View the **Project name** , **Project ID** , and **Project number** in the resulting **Settings** panel. The **Project number** consists of digits, while the **Project ID** is alphanumeric. Edit the **Project
   name**, which displays to users during authorization prompts.

### View Google Cloud logs \& error reports in the Google Cloud console

If you're using [Google Cloud logging](https://developers.google.com/apps-script/guides/logging#cloud_logging)
or [error reporting](https://developers.google.com/apps-script/guides/logging#error_reporting)
for your script project, you can view those logs and reports in the
[Google Cloud console](https://console.cloud.google.com/) by doing the following:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. Click Menu .
3. In the **Operations** section, click **Logging \> Logs explorer**.
4. To view error reports, in the **Operations** section, click **Error Reporting**. If you're prompted to set up error reporting, this means that your script project hasn't logged any exceptions yet.

### Complete the OAuth consent screen

When using services that require OAuth, Google prompts users to authorize
those services. The OAuth consent screen settings define the information
Google presents to users, such as the application name and Terms of Service
URL.

Default Cloud projects create a consent screen automatically from the
Apps Script project details; you can't adjust those settings.
Standard Cloud projects let you customize this information. To
configure your script's consent screen:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. Click Menu \> **APIs \& Services** \> **Credentials**.
3. Click **Configure consent screen**.
4. Fill in each section of the consent screen workflow.
5. To record your changes at each stage, click **Save and continue**.

### Create OAuth credentials

Apps Script usually sets up OAuth for the services your script
uses. For some applications, create additional OAuth credentials (client IDs
and client secrets). Do this only with standard projects.

To create a client ID and client secret for your script project:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. Click Menu \> **APIs \& Services** \> **Credentials**.
3. Click **Create credentials** \> **OAuth client ID**.
4. Under **Application type** , select your application type and fill in the form. When finished, click **Create**.
5. In the dialog, click **Download JSON**. Use this file to configure OAuth.

### Add additional owners to a standard Cloud project

Add additional owners or other roles to a standard project to ensure
that someone on your team always has access to the script project's
Google Cloud settings.

To add additional owners or other roles to a standard project (requires edit
permissions):

1. Determine your collaborators. We recommend using a Google Group. Specify domains to include all users in that domain.
2. [Open the script's Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
3. Click Menu \> **IAM \& admin** \> **IAM**.
4. At the top, click **Add**.
5. Follow the on-screen instructions to add new members and their roles. Add individual emails, Google Groups, or domains.
6. Click **Save**.

### Group multiple scripts with a single Cloud project

Multiple Apps Script projects can share the same standard
Cloud project. To do this, create a standard project and then
[switch](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project) each script project
to use it. You can't do this with default projects.

If you want to publish your script project on the
[Marketplace](https://developers.google.com/workspace/marketplace/overview) as an
[add-on](https://developers.google.com/workspace/add-ons/overview), it must have
its own standard project---published apps can't share
Cloud projects.

## Use a different standard Cloud project

Switch a script project to use a different standard
Cloud project. If your script requires manual configuration of the
Cloud project, switch from a default project to a standard project.
To learn more, refer to [standard
Cloud projects](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects).

### Effects of switching to a different standard Cloud project

If you switch your script from a default project or to a different standard
project, it has the following effects:

- If you activated advanced services for your script, you must turn on the corresponding APIs in the new Cloud project. You lose any data tied to the advanced services in the previous Cloud project. To learn how to turn on APIs in your Cloud project, refer to [Enable Google Workspace APIs](https://developers.google.com/workspace/guides/enable-apis).
- If your script uses the built-in Google Drive service, you must turn on the Drive API in standard Cloud projects. In your standard Cloud project, turn on the Drive API:

  [Turn on the Drive API](https://console.cloud.google.com/apis/enableflow?apiid=drive.googleapis.com)
- All users who have previously authorized the script must re-authorize. In most cases, all users who have previously authorized apps associated with the new project must also re-authorize.
- If your script is associated with an app listing on the Google Workspace Marketplace, your app listing, users, and reviews don't carry over to the new project. You must create an app listing within the new project and your users must reinstall your app. For information about creating a new app listing, refer to [Publish an app](https://developers.google.com/workspace/marketplace/how-to-publish).
- You can't switch a script back to a default project. Apps Script deletes default projects after you set the script to use a standard project.

### Switch to a different standard Cloud project

To switch a script's existing Cloud project over to another
Cloud project, follow these steps:

1. If you don't have a suitable Cloud project, create one by following the [Create a
   project](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project) instructions. Set a memorable project name to locate it on the [Google Cloud console **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager). Apps Script uses this name when asking users to authorize the script.
2. If you want to use an existing project, open the [Google Cloud console **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager) and locate an existing project to use. You must have the Project Browser and OAuth Config Editor roles, or roles with the equivalent permissions, for the project. You can't use a project that was automatically created by Apps Script.
3. [Determine the **Project number** of your Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#determining_the_id_and_number_of_a_standard_gcp_project).
4. Open the script whose Cloud project you want to replace.
5. At the left, click **Project Settings** .
6. Under **Google Cloud Project** , click **Change project**.
7. Enter the new project number and click **Set project**.

## Cloud projects \& shared drives

Shared drives are only available to
[Google Workspace Business](https://support.google.com/a/answer/6034782) and
[Google Workspace Enterprise](https://support.google.com/a/answer/7284269)
customers.

[Shared drives](https://developers.google.com/drive/v3/web/about-teamdrives) (formerly Team Drives) provide
shared spaces where groups of Drive users can collaborate on
Apps Script projects and Drive documents. Shared
drives are valuable when developing scripts, add-ons, and web
apps with a team, but they place some restrictions on what you can do with
older default Cloud projects.

The following list describes how Cloud projects interact with shared
drives:

- If your script project uses a standard project, there are no additional restrictions when the script project resides in a shared drive.
- If your script project uses a default project that was created on or after April 8, 2019, there are no additional restrictions when the script project resides in a shared drive.
- If your script project uses a default project that was created before April 8, 2019, the following restrictions apply while the script project resides on a shared drive:
  1. You can't access the default project using the Apps Script UI or the [Google Cloud console](https://console.cloud.google.com/). This restriction prevents you from taking [actions that require direct access to the project](https://developers.google.com/apps-script/guides/cloud-platform-projects#when_standard_gcp_projects_are_required).
  2. You can't activate [advanced services](https://developers.google.com/apps-script/guides/services/advanced). To activate advanced services, switch to a standard project.
  3. When you move an existing Apps Script project into a shared drive, Google restricts access to the default Cloud project. You can still access the default project if you had access prior to the move. For example, if you created a script in your My Drive folder and then moved it into a shared drive, you could still access the script's Cloud project. Your collaborators in the shared drive might not be able to.
  4. A script retains the Cloud project name it had prior to being moved to a shared drive. Even if you change the project name on the shared drive, users that authorize the script still see the old name on authorization dialogs.

To avoid these restrictions for older scripts,
[switch to a standard project](https://developers.google.com/apps-script/guides/cloud-platform-projects#use_a_different_standard_project).

## Get a list of Apps Script Cloud projects

If you have the `resourcemanager.projects.list` permission for your
organization's Apps Script project folder, you can view all of
the standard and default Apps Script Cloud projects
within the folder.

1. Open the [Google Cloud console **Manage Resources** page](https://console.cloud.google.com/cloud-resource-manager).
2. Next to the **Apps Script** folder, copy the ID.
3. Click **Filter** \> **Parent ID** and paste the Apps Script folder ID.

## Delete Apps Script Cloud projects

You must be an administrator to delete default projects.

To delete an Apps Script project from the Google Cloud console:

1. [Open the Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#access_standard_gcp_project).
2. At the top-right, click More \> **Project settings**.
3. Click **Shut down / delete**.
4. Follow the on-screen instructions to shut down the project.

To delete an Apps Script project using `gcloud`, use the following
commands.

    gcloud projects list --filter='parent.id=APPS_SCRIPT_FOLDER_ID'
    gcloud projects delete PROJECT_ID

For more information about deleting Cloud projects, see [Shutting down
(deleting) projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects).