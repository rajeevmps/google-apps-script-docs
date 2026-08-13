# Installable Triggers

## Page Summary

- Installable triggers allow Apps Script functions to run automatically based on events, offering more flexibility and authorization capabilities than simple triggers.
- Installable triggers are subject to restrictions, including not running in read-only mode, not being triggered by script executions or API requests (with one exception), and always running under the creator's account.
- Time-driven triggers allow scripts to execute at specific times or intervals.
- Event-driven triggers respond to various events in Google Workspace applications, such as opening, editing, or submitting forms, and can call services requiring authorization.
- Installable triggers can be managed manually through the script editor or programmatically using the Script service.

Like [simple triggers](https://developers.google.com/apps-script/guides/triggers), installable triggers let
Google Apps Script run a function automatically when a certain event,
such as opening a document, occurs. Installable triggers, however, offer more
flexibility than simple triggers: they can call
[services](https://developers.google.com/apps-script/guides/services) that require
[authorization](https://developers.google.com/apps-script/guides/services/authorization), they offer several
additional types of events including time-driven (clock) triggers, and they can
be controlled programmatically. For both simple and installable triggers,
Apps Script passes the triggered function an
[event object](https://developers.google.com/apps-script/guides/triggers/events) that contains information
about the context in which the event occurred.

For more information about how to use triggers in add-ons, see
[Triggers for Google Workspace add-ons](https://developers.google.com/workspace/add-ons/concepts/workspace-triggers).

## Restrictions

Even though installable triggers offer more flexibility than simple triggers,
they are still subject to several restrictions:

- They don't run if a file is opened in read-only (view or comment) mode. For
standalone scripts, users need at least view access to the script file for
triggers to run properly.
- Script executions and API requests don't cause triggers to run. For example,
calling
[`FormResponse.submit()`](https://developers.google.com/apps-script/reference/forms/form-response#submit)
to submit a new form response doesn't cause the form's submit trigger to run.
An exception to this restriction is `Form.submitGrades()`. If your code
uses an `onFormSubmit` trigger, calling `Form.submitGrades()` triggers
the `onFormSubmit` condition and causes an infinite loop. To prevent the
infinite loop, add code that checks whether grades already exist before
calling `submitGrades()`.
- Installable triggers always run under the account of the person who created
them. For example, if you create an installable open trigger, it runs
when your colleague opens the document (if your colleague has edit access),
but it runs as your account. This means that if you create a trigger to
send an email when a document is opened, the email is always sent from
your account, not necessarily the account that opened the document. However,
you can create an installable trigger for each account, which results
in one email sent from each account.
- A given account can't see triggers installed from a second account, even
though the first account can still activate those triggers.
- Installable triggers are subject to Apps Script trigger
[quota limits](https://developers.google.com/apps-script/guides/services/quotas).

## Time-driven triggers

A time-driven trigger (also called a clock trigger) is similar to a
[cron job](http://en.wikipedia.org/wiki/Cron) in Unix. Time-driven triggers let
scripts execute at a particular time or on a recurring interval, as frequently
as every minute or as infrequently as once per month. (An
add-on can use a time-driven trigger once per hour at
most.) The time might be slightly randomized—for example, if you create a
recurring 9 AM trigger, Apps Script chooses a time between 9 AM
and 10 AM, then keeps that timing consistent from day to day so that 24 hours
elapse before the trigger fires again.

## Event-driven triggers

Installable event-driven triggers are conceptually similar to
[simple triggers](https://developers.google.com/apps-script/guides/triggers#getting_started) like
`onOpen()`, but they can respond to additional events, and they behave
differently.

For example, the installable open trigger for Google Sheets activates whenever
the spreadsheet is opened by any user who has edit access, just like the simple
`onOpen()` trigger. However, the installable version can call
[services](https://developers.google.com/apps-script/guides/services) that require
[authorization](https://developers.google.com/apps-script/guides/services/authorization). The installable
version runs with the authorization of the user who created the trigger, even
if another user with edit access opens the spreadsheet.

There are several installable triggers for Google Workspace applications:

- An installable **open** trigger runs when a user opens a spreadsheet,
document, or form that they have permission to edit.
- An installable **edit** trigger runs when a user modifies a value in a
spreadsheet.
- An installable **change** trigger runs when a user modifies the structure of a
spreadsheet itself—for example, by adding a new sheet or removing a
column.
- An installable **form submit** trigger runs when a user responds to a form.
There are two versions of the form-submit trigger,
[one for Google Forms itself](https://developers.google.com/apps-script/guides/triggers/events#google_forms_events)
and [one for Sheets if the form submits to a spreadsheet](https://developers.google.com/apps-script/guides/triggers/events#google_sheets_events).
- An installable **calendar event** trigger runs when a user's calendar events
are updated—created, edited, or deleted.

Installable triggers are available in standalone and bound scripts. For
example, a standalone script can programmatically create an installable trigger
for an arbitrary Google Sheets file by calling
[`TriggerBuilder.forSpreadsheet(key)`](https://developers.google.com/apps-script/reference/script/trigger-builder#forSpreadsheet(String))
and passing in the spreadsheet's ID.

## Manage triggers manually

To manually create an installable trigger in the script editor, follow these
steps:

1. Open your Apps Script project.
2. At the left, click **Triggers** alarm.
3. At the bottom right, click **Add Trigger**.
4. Select and configure the type of trigger you want to create.
5. Click **Save**.

## Manage triggers programmatically

Create and delete triggers programmatically with the
[Script service](https://developers.google.com/apps-script/reference/script). Start by calling
[`ScriptApp.newTrigger(functionName)`](https://developers.google.com/apps-script/reference/script/script-app#newTrigger(String)),
which returns a
[`TriggerBuilder`](https://developers.google.com/apps-script/reference/script/trigger-builder).

The following example shows how to create two time-driven triggers—one that
fires every 6 hours, and one that fires every Monday at 9 a.m. (in the time zone
that your script is set to).

```javascript
/**
 * Creates two time-driven triggers.
 * @see https://developers.google.com/apps-script/guides/triggers/installable#time-driven_triggers
 */
function createTimeDrivenTriggers() {
  // Trigger every 6 hours.
  ScriptApp.newTrigger("myFunction").timeBased().everyHours(6).create();
  // Trigger every Monday at 09:00.
  ScriptApp.newTrigger("myFunction")
    .timeBased()
    .onWeekDay(ScriptApp.WeekDay.MONDAY)
    .atHour(9)
    .create();
}
```

This next example shows how to create an installable open trigger for a
spreadsheet. Unlike for a simple `onOpen()` trigger, the script for
the installable trigger doesn't need to be bound to the spreadsheet. To create
this trigger from a standalone script, replace `SpreadsheetApp.getActive()` with
a call to
[`SpreadsheetApp.openById(id)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#openById(String)).

```javascript
/**
 * Creates a trigger for when a spreadsheet opens.
 * @see https://developers.google.com/apps-script/guides/triggers/installable
 */
function createSpreadsheetOpenTrigger() {
  const ss = SpreadsheetApp.getActive();
  ScriptApp.newTrigger("myFunction").forSpreadsheet(ss).onOpen().create();
}
```

To programmatically modify an existing installable trigger, you must delete it
and create a new one. If you have previously stored the ID of a trigger, delete
it by passing the ID as an argument to the following function.

```javascript
/**
 * Deletes a trigger.
 * @param {string} triggerId The Trigger ID.
 * @see https://developers.google.com/apps-script/guides/triggers/installable
 */
function deleteTrigger(triggerId) {
  // Loop over all triggers.
  const allTriggers = ScriptApp.getProjectTriggers();
  for (let index = 0; index < allTriggers.length; index++) {
    // If the current trigger is the correct one, delete it.
    if (allTriggers[index].getUniqueId() === triggerId) {
      ScriptApp.deleteTrigger(allTriggers[index]);
      break;
    }
  }
}
```

Before creating a trigger, verify that the associated function has all the
necessary [OAuth permissions](https://developers.google.com/apps-script/concepts/scopes#trigger-permissions).

## Errors in triggers

When an installable trigger fires but the function throws an exception or
otherwise fails to run successfully, no error message appears on your screen.
After all, when a time-driven trigger runs or another user activates
your form-submit trigger, you might not even be at your computer.

Instead, Apps Script sends an email like the following:

```
From: noreply-apps-scripts-notifications@google.com
Subject: Summary of failures for Apps Script
Your script has recently failed to finish successfully.
A summary of the failure(s) is shown below.
```

The email includes a link to deactivate or reconfigure the trigger. If the
script is
[bound](https://developers.google.com/apps-script/scripts_containers)
to a Google Sheets, Docs, or Forms
file, the email also includes a link to that file. These links let you
deactivate the trigger or edit the script to fix the bug.

To troubleshoot errors in your script, click the link in the notification email
to open your script project. Once the project is open, view the execution logs
by clicking **Executions** playlist_play in
the left navigation panel. The logs show which executions failed and include
error messages to help you diagnose and fix the problem.

Installable triggers created by add-ons don't send users these
email notices.

To review all of the triggers that are associated with your Google Account and
deactivate the triggers you no longer need, follow these steps:

1. Go to [`script.google.com`](https://script.google.com).
2. At the left, click **My Triggers**.
3. To delete a trigger, at the right of the trigger, click More
 more_vert > **Delete trigger**.

If a trigger is deactivated, its corresponding failure notifications are also
deactivated. Failure notifications are an inherent part of an active trigger.
Consequently, to stop receiving all failure notifications for a specific
trigger, deactivate or delete the trigger itself. While a trigger
is active, you can only adjust the frequency of these notifications.

```
 Simple triggers like `onOpen()` can't be deactivated from this
 page; instead, edit the appropriate script and remove or rename
 the `onOpen()` function.
```

## Triggers in add-ons

In addition to installable triggers, use manifest triggers in
add-ons. For more information, see
[Triggers for Google Workspace add-ons](https://developers.google.com/workspace/add-ons/concepts/workspace-triggers).
