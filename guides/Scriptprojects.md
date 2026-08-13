# Script Projects

A script project represents a collection of files and resources in
Google Apps Script, sometimes referred to as "a script". A script
project has one or more script files which can either be code files (having a
`.gs` extension) or HTML files (a `.html` extension). You can also include
JavaScript and CSS in HTML files.

The script editor always has one and only one project opened at any given time.
You can open multiple projects in multiple browser windows or tabs.

## Create and delete projects

This section explains how to create and delete standalone or
container-bound Apps Script projects.

### Create a standalone project

To create a standalone project from Apps Script:

1. Go to [`script.google.com`](https://script.google.com/).
2. Click **New Project**.
3. In the script editor, click **Untitled project**.
4. Give your project a name and click **Rename**.

### Create a standalone project from Google Drive

1. Open [Google Drive](https://drive.google.com/).
2. Click **New** \> **More** \> **Apps Script**.

### Create a container-bound project from Google Docs, Google Sheets, or Google Slides

1. Open a Docs document, a Sheets spreadsheet, or Slides presentation.
2. Click **Extensions** \> **Apps Script**.
3. In the script editor, click **Untitled project**.
4. Give your project a name and click **Rename**.

### Create a container-bound project from Google Forms

1. Open a form in Forms.
2. Click More \> **Script editor**.
3. In the script editor, click **Untitled project**.
4. Give your project a name and click **Rename**.

### Create a standalone project using the `clasp` command-line tool

`clasp` is a command-line tool that creates, pulls/pushes, and deploys Apps
Script projects from a terminal.

See the [Command-line interface using `clasp` guide](https://developers.google.com/apps-script/guides/clasp) for more details.

### Delete a container-bound project

Once you delete a container-bound Apps Script project, it can't be
recovered.

1. Open your container-bound project using one of the methods described previously.
2. At the top left, click **Overview** .
3. At the top right, click Remove \> **Delete forever**.

Only the owner of the container can see the deletion menu options.

### Delete a standalone project

1. Go to [`script.google.com`](https://script.google.com/).
2. At the right of the project you want to delete, click More \> **Remove** \> **Remove**.

## Manage files in a project

This section describes how to add, delete, and export files within an
Apps Script project.

### Create a file

1. Open your Apps Script project.
2. At the left, click **Editor** \> Add .
3. Select the type of file to create and give it a name.

### Delete a file

> [!CAUTION]
> **Caution:** Deleted files can't be recovered.

1. Open your Apps Script project.
2. At the left, click **Editor** .
3. Next to the file you want to delete, click More \> **Delete**.

### Export files out of an Apps Script project

To export code files, copy and paste the code from each file into your preferred
text editor or use `clasp` on the command-line. To use `clasp`, refer to
[download a script project](https://developers.google.com/apps-script/guides/clasp#download_a_script_project).

## Set the time zone for a project

When you set a time zone for an Apps Script project, scripts use
that time zone when they run.

1. Open your Apps Script project.
2. At the left, click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).
3. In the **Time zone** section, select the time zone you want to use.

To use a different time zone for a specific function, explicitly enter the time
zone in that function. For example, in the following sample, each function
creates a new event in Google Calendar. The first function defaults to the
project time zone. The second function specifies the Pacific time zone, so the
event is scheduled in Pacific time, regardless of the project's time zone.

    function createEvent(){
    // Creates an event in the script project's time zone and logs the ID
    var event = CalendarApp.getDefaultCalendar().createEvent('New test event',
       new Date('December 20, 2022 17:00:00'),
       new Date('December 20, 2022 18:00:00'));
    console.log('Event ID: ' + event.getId());
    }
    function createEventPacific(){
    // Creates an event with a specified time zone and logs the event ID.
    var event = CalendarApp.getDefaultCalendar().createEvent('New sample event',
       new Date('December 20, 2022 17:00:00 PDT'),
       new Date('December 20, 2022 18:00:00 PDT'));
    console.log('Event ID: ' + event.getId());
    }

## Fix issues with multiple Google Accounts

If you're logged into multiple Google Accounts at the same time, you might
have trouble accessing your add-ons and web apps.
Multi-login, or
being logged into multiple Google Accounts at once, isn't supported for Apps
Script, add-ons, or web apps.

- **If you open the Apps Script editor** while logged in to more than one account,
  Google prompts
  you to choose the account you want to proceed with.

- **If you open a web app or add-on** and experience multi-login issues, try one of
  the following solutions:

  - Log out of all your Google Accounts and only log in to the one that has the add-on or web app you want to access.
  - Open an incognito window in Google Chrome, or an equivalent private browsing window, and log in to the Google Account that has the add-on or web app you want to access.