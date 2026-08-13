# Collaborate with other developers

Google Apps Script provides features that help teams build and maintain scripts,
Google Workspace add-ons, and web apps together. This guide covers active collaboration
on a project by multiple developers; if you want to share code for others to
include in their own projects, see the [Libraries](https://developers.google.com/apps-script/guides/libraries)
guide instead.

## Collaboration basics

In order to collaborate on a project, you and your collaborators must all have
editor access to the Apps Script project file (and its container,
if it is a [bound script](https://developers.google.com/apps-script/guides/bound)). This lets everyone on
your team see and make changes to the Apps Script code. Editors
can also create new code versions, publish add-ons, and deploy
scripts as web apps or as executables for the
[Apps Script API](https://developers.google.com/apps-script/api).

Plan beforehand how you handle the editing, reviewing, versioning, and (if
applicable) the deployment and publishing of your project,
add-on or web app.
[Standalone projects](https://developers.google.com/apps-script/guides/standalone) are usually the easiest
to collaborate on, because they appear directly in Google Drive and are the
recommended project type for add-on and web app
development.

A common problem in collaboration occurs when a script project owner leaves the
team without transferring ownership of the project to someone else on the team.
This can leave you unable to maintain or update the project. Placing your
script project in a [shared drive](https://developers.google.com/drive/api/v3/about-shareddrives) prevents
this problem, since files in a shared drive don't have specific owners.

**Always share ownership of script projects.** If someone leaves your
organization and their account is removed, access to scripts without other
owners is lost.
[Share your script in Drive](https://support.google.com/drive/answer/2494822) or
[move it into a shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives).

## Collaborate with the `clasp` command-line tool

`clasp` lets you sync projects between [script.google.com](https://script.google.com) and your local file system. This lets you streamline
and automate your code development if you and your collaborators are using
source control management software such as `git`.

For more details, refer to [Command Line Interface
using `clasp` guide](https://developers.google.com/apps-script/guides/clasp).

## Collaborate with shared drives

Shared drives are only available to
[Google Workspace Business](https://support.google.com/a/answer/6034782) and
[Google Workspace Enterprise](https://support.google.com/a/answer/7284269)
customers.

[Shared drives](https://developers.google.com/drive/api/v3/about-shareddrives) provide a shared space in
Drive where groups of Drive users can more
effectively collaborate. Files placed in a shared drive are owned by the group
as a whole, rather than individuals. This means that when a collaborator leaves
the group they don't take file ownership and control with them.

Shared drives also let you move files across domains --- a shared drive
in one domain can have collaborators from another domain who can move files from
that domain into the shared drive. This provides a means for a team to develop
add-ons, web apps, or other code for customers in different
domains.

When you use shared drives to collaborate on Apps Script projects:

1. Collaborators with editor access to a shared drive can create or move new files into the shared drive. As script editors, they can view and edit scripts projects, run script code, create new script versions, and publish add-ons.
2. To deploy scripts as web apps or executables for the [Apps Script API](https://developers.google.com/apps-script/api), the account that creates the deployment must belong to the same domain as the shared drive that the script resides in.
3. Shared drives let you share specific files within the shared drive to others outside the group, and update their edit and view permissions on those files like any other Drive file. However, if a user is part of the team the shared drive belongs to, you can't reduce their access for specific files. For example, if a user has edit access to a shared drive, you can't change that to view-only access for a specific file within the shared drive.
4. Collaborators with full access to a shared drive can also delete files and Apps Script projects, and move files out of the shared drive.
5. All [container-bound scripts](https://developers.google.com/apps-script/guides/bound) use the same viewer and editor access lists defined for the container file. For example, if you have edit access to a Google Sheet you also have edit access to any Apps Script project code attached to it. Placing such a container file into a shared drive grants the shared drive's collaborators the same access to the script code as they have for the container itself.
6. When a script project resides in a shared drive, access to its [Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects) may be restricted. See the [Google Cloud projects and shared drives](https://developers.google.com/apps-script/guides/cloud-platform-projects#gcp_projects_and_shared_drives) guide section for details.
7. [Web apps](https://developers.google.com/apps-script/guides/web#deploying_a_script_as_a_web_app) deployed in one domain cease to function if their ownership changes to a shared drive or account in a different domain. Correct this by moving the script back to its original domain.
8. Similarly, script projects that are [deployed as an Apps Script API executable](https://developers.google.com/apps-script/api/how-tos/execute) cease to function when called by the API if moved via shared drive from one domain to another. Correct this by moving the script back to its original domain.

## Collaborate with a shared folder

Use caution if you create or move an Apps Script project to a
shared folder. Make sure the folder is only shared with trusted people.

If you can't collaborate with a shared drive, use a shared folder instead.
When you create or move an Apps Script project to a
Drive folder that other people can access, they inherit the same
access to the Apps Script project that they have for the folder.
For example:

- If someone has edit access to the folder, they can edit or delete the Apps Script project and run the script.
- If someone only has view access to the folder, they can view the Apps Script project and run the script.

## Collaborate with project sharing

[Video](https://www.youtube.com/watch?v=3A2y_Gw8gSc)

Collaborate on a project by directly sharing the project with all
collaborators. Directly share script projects that reside in regular
Drive folders or in shared drives. Carefully plan who owns and
maintains the script over time.

[Standalone projects](https://developers.google.com/apps-script/guides/standalone) appear in
Drive as a file; share them like any other file. For more
information, see
[Sharing files and folders](https://support.google.com/drive/answer/2494822).

[Container-bound projects](https://developers.google.com/apps-script/guides/bound) aren't visible in
Drive. To share a container-bound project, share the parent
container file. For example, if you have a script bound to a Google Sheets
spreadsheet, make someone an editor of the script by making them an editor of
the spreadsheet. Container-bound projects inherit the viewer and editor access
settings of their container file.

**All container-bound scripts use the same owner, viewer and editor access list
defined for the container file**. The container owner takes ownership of a new
script project regardless of who created it.

## Collaboration and project resources

Resources are entities that are associated with your project but exist
independently of its code. This section explains how collaborating on a project
affects its resources, in particular: its Google Cloud project, triggers,
libraries, and user properties.

### Collaboration and Google Cloud projects

Every Apps Script project has an associated
[Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects).
Google Cloud projects have their own set of owners, editors, and other roles,
which can be different from the set of users that can access the script
project.

> [!CAUTION]
> If your script project is meant to be published as an
> [add-on](https://developers.google.com/workspace/add-ons/overview), it
> must use a [standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects).
>
> When you collaborate on an application that uses a standard project,
> [configure the Google Cloud owners and roles](https://developers.google.com/apps-script/guides/cloud-platform-projects#adding_additional_owners_to_a_standard_gcp_project)
> to ensure all your collaborators have the proper levels of access. This helps
> prevent situations where you lose access to the project's Cloud settings because
> its owners are no longer with your organization.

### Collaboration and triggers

When you collaborate on a project, any
[installable triggers](https://developers.google.com/apps-script/guides/triggers/installable) that you create
are not shared with those who have access to your project. If you need to have
a consistent trigger setup for all collaborators, use the
[Script service](https://developers.google.com/apps-script/reference/script/script-app) to create triggers
programmatically, at run time. For more information, see
[Managing Triggers Programmatically](https://developers.google.com/apps-script/managing_triggers_programmatically).

Since simple triggers are created from code, they **are** shared with project
collaborators.

### Collaboration and libraries

Libraries included in your project are available to project collaborators.
However, if they don't have at least read-level access to an included library
they can't use those libraries --- the script throws an error in this case.
For more information about libraries, see
[Managing Libraries](https://developers.google.com/apps-script/managing_libraries).

### Collaboration and user properties

[User properties](https://developers.google.com/apps-script/reference/properties/properties-service#getuserproperties)
are unique to the user that created them. This means that project
collaborators can't see or access your user properties and you can't see or
access theirs. Use
[script properties](https://developers.google.com/apps-script/reference/properties/properties-service#getscriptproperties)
if you want to share project specific properties with collaborators. For
more information, see the [Properties guide](https://developers.google.com/apps-script/guides/properties).