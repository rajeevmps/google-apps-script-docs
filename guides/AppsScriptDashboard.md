# The Google Apps Script Dashboard

The [Apps Script dashboard](https://script.google.com/) lets you
manage and monitor your Apps Script projects. Use the dashboard
to:

- View and search for your existing Apps Script projects, including [bound](https://developers.google.com/apps-script/guides/bound) scripts attached to Google Workspace documents.
- Create new projects.
- View details about your projects, such as the [OAuth scopes](https://developers.google.com/apps-script/concepts/scopes) it uses.
- Monitor the health and usage of your script projects.
- View execution logs for your projects and others that run using your account's credentials.
- Toggle on or off the [Apps Script API](https://developers.google.com/apps-script/api/concepts) to allow or prevent apps from using the API to interact with your script projects.

## View and search projects

The Apps Script dashboard lists all the script projects you can
view or edit. The left nav of the dashboard divides these projects into the
following categories:

- **Starred Projects** . Projects that you are [monitoring](https://developers.google.com/apps-script/guides/dashboard#monitor_projects).
- **My Projects**. Projects for which you are an owner.
- **All Projects**. Projects which you own or have view or edit permissions for.
- **Shared with me**. Projects that you do not own but that have been shared with you.
- **Trash**. Projects that you have removed from Google Drive.

The project lists show the project name, owner, and last modified date. Icons
next to the project name indicate whether the project is a
[standalone](https://developers.google.com/apps-script/guides/standalone) project or a
[bound](https://developers.google.com/apps-script/guides/bound) project.

## View project details

Each project includes a view to see developer details about the project. To
view the details about a project, click the row from the project list.

The project details view shows **Error rate** , **Executions** and **Users**
data and graphs about the project, as well as
[OAuth scopes](https://developers.google.com/apps-script/concepts/scopes) requested of any user of the
project. Data metrics are defined as follows:

- **Error rate**. The percent of executions that failed to run due to uncaught exceptions. It is calculated as failed executions divided by the total executions over the defined time period.
- **Executions** . The number of times a project has been "run" or executed. See [Execution types](https://developers.google.com/apps-script/guides/dashboard#execution_type) for more information about how a project can be run.
- **Users**. The number of unique user accounts who ran the project one or more times over the specified time period. Anonymous users are not tracked and therefore are not reflected in the user count or graphs.

Each deployment of your project appears as a tab on the **Project Details**
page preceding the data and graphs; select the tab to see the associated data for
that deployment. Selecting **ALL** shows aggregate data for all of the project's
deployments and from executions resulting from developers running the project
from within the Apps Script code editor.

Projects published as add-ons don't appear as deployed in the
Apps Script dashboard.

## Monitor projects

Bookmark projects by starring them. Starring projects also lets
you monitor aggregate usage and error rate statistics and graphs.

To star a project, on the right of a project row, click More
\> **Add star** . You can also
star a project by clicking More
while [viewing project details](https://developers.google.com/apps-script/guides/dashboard#view_project_details).

In the left nav, select **Starred Projects** to see the projects you've
bookmarked. Click the **Error rate** , **Executions** , or **Users** scorecard at
the top of the page to see the associated graphs for all your starred projects
over the last 7 days.

Remove a star from a project by clicking More
in its project row and selecting
**Remove star**.

## Manage executions

Use the Apps Script dashboard to view and manage individual
executions of Apps Script project functions. Find a full log of
recent executions by selecting **My Executions** in the left nav.

The **My Executions** panel shows a log of all previous and running
executions for projects for which you are an owner, editor or viewer. This list
can also include function executions in projects that you don't have access to
if they run on your behalf (for example, add-ons that you've
installed and run). The execution list only shows the initial function that is
called to start the execution. It doesn't show every function called during
that execution.

Control which type of execution is reported in the log using the filters at the
top of the view. Each row of the log represents a single execution. The
**Start Time** , **Duration** , and **Status** columns show the corresponding
information about that execution.

The **Function** column shows the name of the function that initiated the
execution. There is no name in this column if you don't have access to the
execution's corresponding script project but it ran on your behalf.

The **Type** column shows what initiated the execution. Values include:

- **Add On**. The execution originated from an add-on.
- **Execution API**. The execution originated from an invocation of the Apps Script API.
- **Time Driven**. The execution was caused by a time event.
- **Trigger**. The execution originated from a trigger source.
- **Webapp**. The execution originated from a deployed web app.
- **Editor**. The execution originated from the Apps Script editor.

### Terminate executions

Long running executions that are in-progress are indicated by a **Status** of
"Running". To stop these executions, on the right of the project row, click
More \> **Terminate**.

## Settings

Adjust your dashboard settings by selecting **Settings** in the left nav.

In the **Settings** panel is a toggle for the
[Apps Script API](https://developers.google.com/apps-script/api/concepts). This lets you grant
the API [access to your script projects](https://developers.google.com/apps-script/api/how-tos/enable#granting_access_to_script_projects).

To access this toggle click the **Google Apps Script API** label in the
**Settings** panel. This opens a new panel with warning text and a toggle
switch. Access to your script projects is toggled off by default as a security
precaution. Once you grant access, any third-party application you authorize
can use the API to modify your scripts and deployments. Revoke this access in
the **Settings** panel at any time.

Find more information in the [Apps Script API access guide](https://developers.google.com/apps-script/api/how-tos/enable#granting_access_to_script_projects).