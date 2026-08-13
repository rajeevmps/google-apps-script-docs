# Assign permissions for Google Cloud projects

To manage add-on projects across your organization,
view and manage their associated Google Cloud projects. This guide describes how to
assign predefined roles that allow the role to view and manage all
Google Cloud projects in an organization. To learn more about available
permissions in Google Cloud, refer to [IAM basic and predefined roles
reference](https://cloud.google.com/iam/docs/understanding-roles).

## Prerequisites

To assign permissions in Google Cloud, sign in to Google Workspace as a
[super administrator](https://support.google.com/a/answer/2405986#super_admin).

## Assign view permission for all Cloud projects in an organization

To give someone view permission for all Cloud projects in your organization
as a super administrator, follow these steps:

1. Open the Cloud console at [console.cloud.google.com](https://console.cloud.google.com/).
2. Click Menu \> **IAM \& Admin** \> **Manage Resources**.
3. Select your organization.
4. At the right, click **Add Principal**.
5. In **New principals**, add the users or groups to let view projects.
6. In **Select a role** , in the first list, select **Resource Manager** . In the second list, select **Folder Viewer**.
7. Click **Save**.

## Assign edit permission for all Cloud projects in an organization

To give someone edit permission for all Cloud projects in an organization
as a super administrator, follow these steps:

1. Open the Cloud console at [console.cloud.google.com](https://console.cloud.google.com/).
2. Click Menu \> **IAM \& Admin** \> **Manage Resources**.
3. Select your organization.
4. At the right, click **Add Principal**.
5. In **New principals**, add the users or groups to let edit projects.
6. In **Select a role** , in the first list, select **Resource Manager** . In the second list, select **Folder Viewer**.
7. Click **Add Another Role**.
8. In **Select a role** , in the first list, select **Resource Manager** . In the second list, select **Project Mover**.
9. Optionally, to allow someone to turn APIs on or off in Cloud projects:
   1. Click **Add Another Role**.
   2. In **Select a role** , in the first list select **Service Usage** . In the second list, select **Service Usage Admin**.
10. Click **Save**.

## Assign delete permission for all Cloud projects in an organization

To give someone delete permission for all Cloud projects in an
organization as a super administrator, follow these steps:

1. Open the Google Cloud console at [console.cloud.google.com](https://console.cloud.google.com/).
2. Click Menu \> **IAM \& Admin** \> **Manage Resources**.
3. Select your organization.
4. At the right, click **Add Principal**.
5. In **New principals**, add the users or groups to let delete projects.
6. In **Select a role** , in the first list, select **Resource Manager** . In the second list, select **Folder Viewer**.
7. Click **Add Another Role**.
8. In **Select a role** , in the first list, select **Resource Manager** . In the second list, select **Project Deleter**.
9. Click **Save**.

## Related resources

- [IAM overview](https://cloud.google.com/iam/docs/overview)
- [Roles and permissions](https://cloud.google.com/iam/docs/roles-overview)
- [IAM basic and predefined roles reference](https://cloud.google.com/iam/docs/understanding-roles)


# Monitor &amp; restrict data access

You need an Enterprise, Education Standard, or Education
Plus Google Workspace account to monitor and restrict the data access that
users grant to Apps Script.

Google Workspace users grant access to levels of data, known as scopes, when
they run scripts or use apps like add-ons or web apps. This page
describes how to monitor or revoke the scopes that users grant access to within
their Google Workspace account.

## Monitor OAuth grant events by scope

To view events where users grant access to a specific scope or scopes, follow
these steps:

1. In the Google Admin console, go to Menu

   \> **Security**
   \> **Security center**
   \> **Investigation tool**.

   [Go to Investigation tool](https://admin.google.com/ac/sc/investigation)
2. Click **Data Source** and select **OAuth log events**.

3. Click **Add condition** \> **Attribute**
   and select **Event**.

4. Click **Event** and select **Grant**.

5. Click **Add condition** \> **Attribute**
   and select **Scope**.

6. For **Scope** , enter the scope you want to monitor. For a list of scopes,
   refer to [OAuth 2.0 Scopes for Google APIs](https://developers.google.com/identity/protocols/oauth2/scopes).

7. Click **Search**. A list of grant events displays for the scopes you
   specified.

## Revoke OAuth grants

**Important** : After you revoke access to a scope, users can re-grant access.
Set up alerts for scopes that you don't want users to grant access to so that
you can revoke access as needed. Refer to
[Create an alert for OAuth grants](https://developers.google.com/apps-script/guides/admin/monitor-restrict-oauth-scopes#create_an_alert_for_oauth_grants).

To revoke access to a scope, follow the steps for
[Monitor OAuth grant events by scope](https://developers.google.com/apps-script/guides/admin/monitor-restrict-oauth-scopes#monitor_oauth_grant_events_by_scope),
then select the events you want to revoke and click
**Revoke access tokens for users**.

## Create an alert for OAuth grants

To receive an alert when someone grants access to a specific scope, follow the
steps for [Monitor OAuth grant events by scope](https://developers.google.com/apps-script/guides/admin/monitor-restrict-oauth-scopes#monitor_oauth_grant_events_by_scope),
then follow these steps:

1. At the top of the search, click **Create activity rule**.
2. For **Rule name**, enter a name for the alert.
3. Click **Next: View Conditions** . The conditions automatically populate from the search parameters. Edit them if needed, then click **Next: Add Actions**.
4. In **Threshold 1** , select a time frame and threshold for the rule and check the **Send to alert center** box.
5. Click **Add email recipients** and enter the email addresses that should receive alerts. Click **Done**.
6. Click **Next: Review**.
7. Review the details and click **Create Rule**.

For more information, refer to
[Create and manage activity rules](https://support.google.com/a/answer/9275024).

## Restrict access to high-risk OAuth scopes

You can restrict access to most Google Workspace services. For Gmail
and Google Drive, restrict access to high-risk OAuth scopes while allowing
users to give access to OAuth scopes that are not classified as high-risk. If
an app requests access to a restricted high-risk OAuth scope, and you have
not specifically trusted the app, users cannot authorize it.

To restrict access to high-risk OAuth scopes, refer to [Restrict or unrestrict
Google services](https://support.google.com/a/answer/7281227#restrictaccess&zippy=%2Cmanage-access-to-google-services-restricted-or-unrestricted%2Cmanage-access-to-apps-trusted-limited-or-blocked%2Cstep-restrict-or-unrestrict-google-services).


# Monitor and control Google Apps Script use in your Google Workspace organization

You can monitor the actions people take on Apps Script projects
and how many people use Apps Script per day in the
[Google Admin console](https://admin.google.com/).

## View Apps Script audit logs

To view the actions people take on Apps Script projects with
Drive log events reporting in the Admin console, follow these
steps:

1. Open your Admin console at [admin.google.com](https://admin.google.com/).
2. Click Menu \> **Reporting** \> **Audit and investigation** \> **Drive log events** . If **Reporting** doesn't appear, click **Show more**.
3. Click **Filter** \> **Add a filter** \> **Document type**.
4. In the **Document type** section, select **Google Script** and click **Apply**.
5. Click **Search**.

## View how many people use Apps Script

To view the number of people in your organization using
Apps Script each day and how many Apps Script
projects people use per day, follow these steps:

1. Open your Admin console at [admin.google.com](https://admin.google.com/).
2. Click Menu \> **Reporting** \> **Reports** \> **Apps Reports** \> **Apps Script** . If **Reporting** doesn't appear, click **Show more**.
3. To export the data, click Download ![](https://developers.google.com/static/apps-script/images/icons/download_24px.svg).

The charts show data for the last 6 months and include all script executions,
which includes any time a script runs.

## Control access to external domains

Control access to external domains with a Business Plus, Enterprise,
Education Standard, Teaching and Learning Upgrade, or Education Plus
Google Workspace account.

By default, scripts can send or fetch data using any URL with
[URL Fetch Service](https://developers.google.com/apps-script/reference/url-fetch). As an administrator,
you can control which external domains your users can access through
Apps Script. Refer to [Allow only certain external connections
for Apps Script and
Sheets](https://support.google.com/a/answer/13686736).

## Turn off Apps Script

As an administrator, you can turn Apps Script on or off for
people in your organization. For instructions on how to do this, see
[Turn Apps Script on or off for users](https://support.google.com/a/answer/15100049).

## Turn off a specific Apps Script project

You can turn off an individual Apps Script project by deleting
its associated Cloud project. After you shut down a
Cloud project, all executions of the script project stop.
For more information, see
[Shutting down (deleting) projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects).

To delete a Cloud project, obtain delete permissions on the project.
To give delete permissions for projects in your organization, refer to
[Assign delete permission for all Cloud projects in an organization](https://developers.google.com/apps-script/guides/admin/assign-cloud-permissions#assign-delete).

## Related resources

- [Drive log events](https://support.google.com/a/answer/4579696)
- [Create and manage reporting rules](https://support.google.com/a/answer/9908423)
- [Reports API: Drive Activity Report](https://developers.google.com/admin-sdk/reports/v1/guides/manage-audit-drive)


# View or edit Google Cloud projects

Every Google Apps Script project is associated with a project in
Google Cloud. There are 2 types of Cloud projects for
Apps Script:

- **Default Cloud projects** : Apps Script automatically creates and manages a Google Cloud project each time someone creates and runs an Apps Script project. To learn more, refer to [Default Cloud projects](https://developers.google.com/apps-script/guides/cloud-platform-projects#default_google_cloud_projects).
- **Standard Cloud projects** : Users can create and manage their own Cloud projects for advanced Apps Script use cases. To learn more, see [Standard Cloud projects](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_google_cloud_projects).

To view your organization's default and standard Cloud projects in the
Cloud console, obtain the `resourcemanager.projects.list` permission for your
organization. To view standard and default projects separately, obtain
`resourcemanager.folders.list` permission. To set view permissions for
projects in your organization, see [Assign view permission for all Cloud
projects in an organization](https://developers.google.com/apps-script/guides/admin/assign-cloud-permissions#assign_view_permission_for_all_cloud_projects_in_an_organization).

To edit your organization's standard and default Cloud projects in the
Cloud console, obtain the `resourcemanager.projects.update` permission for your
organization. To set edit permissions for projects in your organization, see
[Assign edit permission for all Cloud projects in an organization](https://developers.google.com/apps-script/guides/admin/assign-cloud-permissions#assign_edit_permission_for_all_cloud_projects_in_an_organization).

## View or edit default Cloud projects

Default projects are in the `Organization root > system-gsuite > apps-script`
folder in the Cloud resource hierarchy. Don't delete these folders. If you do,
Apps Script cannot create default projects and won't execute
scripts properly.

To view the `system-gsuite` and `apps-script` folders, obtain
`resourcemanager.folders.list` permission. If you only have
`resourcemanager.projects.list` permission, standard and default projects show
up together in one list. Default project IDs start with `sys-`.

To view or edit the default projects in your organization, follow these steps:

1. Open the Cloud console at [console.cloud.google.com](https://console.cloud.google.com/).
2. Click Menu \> **IAM \& Admin** \> **Manage Resources**.
3. Next to your organization, click Expand node .
4. Next to the `system-gsuite` folder, click Expand node .
5. Next to the `apps-script` folder, copy the ID.
6. Click **Filter** \> **Parent ID**.
7. Paste the Apps Script folder ID and press **Enter**.
8. Next to the project you want to view or edit, click More \> **Settings**. The project opens in the Cloud console, where you can modify it.

## View or edit standard Cloud projects

To view or edit the standard projects in your organization, follow these steps:

1. Open the Cloud console at [console.cloud.google.com](https://console.cloud.google.com/).
2. Click Menu \> **IAM \& Admin** \> **Manage Resources**.
3. Next to your organization, click Expand node . The list of projects includes all standard Cloud projects whether or not they have Apps Script projects associated with them.
   - If you don't have `resourcemanager.folders.list` permission, default Cloud projects might appear in the same list as standard Cloud projects. To tell the difference, default project IDs start with `sys-`.
4. Next to the project you want to view or edit, click More \> **Settings**. The project opens in the Cloud console, where you can modify it.

## Related resources

- [Creating and managing projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
- [Turn Google Cloud on or off for users](https://support.google.com/a/answer/9197205)

