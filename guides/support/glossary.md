# Glossary

## Page Summary

- The active user is the Google account that causes a script to run, distinct from the effective user whose permissions are used during execution.
- Add-ons are Apps Script projects that extend Google product functionality and can be published for public or domain-specific use.
- Containers are Google products like Sheets or Docs that can hold scripts, while standalone scripts are accessible from Google Drive and not attached to a specific product.
- Libraries are script projects that can be included in other scripts to share common code without copying the script into your account.
- Triggers are resources that cause a script function to run based on specified events, such as user actions or time-based intervals.

## Active user

The user (Google account) that causes a script to execute. Depending on the execution method, this may be different from the effective user. Also think of this as the user at the keyboard.

**More information:** [Scripts and Google Accounts](https://developers.google.com/apps-script/scripts_google_accounts#understandingPermissions)

## Add-on

An Apps Script project that extends the functionality of a Google product such as Google Docs or Sheets. Add-ons can be published publicly to allow others to use them, or published for use only within a particular domain.

**More information:** [Add-ons Overview](https://developers.google.com/workspace/add-ons/overview)

## Container

A Google product that can contain scripts. For example, Google Sheets and Docs are both containers because new scripts can be created and be accessed from each of these products. Creating a script in a container makes it easier to access and manipulate the data in the container. Container-bound scripts are not recommended for projects you want to publish; use standalone scripts instead.

**More information:** [Container-bound Scripts](https://developers.google.com/apps-script/guides/bound)

## Effective user

The user (Google account) under whose identity a script executes. Depending on the execution method, this may be different from the active user. The permissions of the effective user are used in the execution context.

**More information:** [Scripts and Google Accounts](https://developers.google.com/apps-script/scripts_google_accounts#understandingPermissions)

## Library

A script project that can be included into other scripts, allowing for common code to be shared. Unlike installing a script from the gallery, adding a library doesn't copy the script into your account. When adding a library, specify a version to use and an identifier to reference it by.

**More information:** [Libraries](https://developers.google.com/apps-script/guides/versions), [Versions](https://developers.google.com/apps-script/guides/versions)

## Script project

A collection of files and resources in Google Apps Script, sometimes referred to as "the script". The script editor always has one project open at any time. Open multiple projects in multiple browser windows or tabs.

**More information:** [Projects](https://developers.google.com/apps-script/guides/projects)

## Shared drive

An organizational space within Google Drive shared among multiple people. Files within a shared drive are not owned by individuals, but by the group of collaborators. Formerly known as "Team Drives".

**More information:** [Shared drives overview](https://developers.google.com/drive/v3/web/about-shareddrives)

## Standalone script

A script accessible from Drive. Unlike a container-bound script, it isn't attached to a specific Google product, like Docs or Sheets.

**More information:** [Scripts and Containers](https://developers.google.com/apps-script/scripts_containers#standalone)

## Team Drive

See [Shared drive](#shared_drive).

## Trigger

A resource in the project that causes a function to run when a specified event takes place. Create triggers for user-initiated events such as opening a spreadsheet or changing a cell value, or for time-based events that fire every day, hour, etc.

**More information:** [Understanding Triggers](https://developers.google.com/apps-script/understanding_triggers)

## Version

An immutable copy of a script at a point in time. Versions are automatically assigned a number when created; add an optional description.

**More information:** [Versions](https://developers.google.com/apps-script/guides/versions), [Libraries](https://developers.google.com/apps-script/guides/versions)

## Web app

A script deployed such that users can access it using only a URL. This was previously known as publishing the script as a "service".

**More information:** [Web Apps](https://developers.google.com/apps-script/execution_web_apps)

Source: https://developers.google.com/apps-script/guides/support/glossary
