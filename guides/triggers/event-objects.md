# Event Objects

## Page Summary

- Apps Script can run a function automatically using simple or installable triggers when a specific event occurs.
- When a trigger fires, an event object (`e`) containing contextual information is passed to the function as an argument.
- This page details the fields within the event object for various trigger types across different Google services like Sheets, Docs, Slides, Forms, Calendar, and Workspace add-ons.
- Events produced by installable triggers include a `triggerUid` to identify the specific trigger.
- Calendar triggers indicate that a sync operation is needed, not which specific event changed.

[Simple triggers](https://developers.google.com/apps-script/guides/triggers) and
[installable triggers](https://developers.google.com/apps-script/guides/triggers/installable) let
Google Apps Script run a function automatically if a certain event
occurs. When a trigger fires, Apps Script passes the function an
event object as an argument, typically `e`. The event object contains
information about the context that caused the trigger to fire. For example, the
following sample code shows a simple `onEdit(e)` trigger for a Google Sheets
script that uses the event object to determine which cell was edited.

```javascript
function onEdit(e){
  // Set a comment on the edited cell to indicate when it was changed.
  var range = e.range;
  range.setNote('Last modified: ' + new Date());
}
```

This page describes the fields in the event object for different types of
triggers.

Events produced by installable triggers contain a `triggerUid` identifying the
trigger that produced the event. This helps scripts that have multiple
installable triggers.

## Google Sheets events

The various Google Sheets-specific triggers let scripts respond to a user's
actions in a spreadsheet.

| Open ( [simple](https://developers.google.com/apps-script/guides/triggers#onopen) and [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `LIMITED` |
| `source` | A [`Spreadsheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet) object, representing the Sheets file to which the script is bound. — Example: `Spreadsheet` |
| `triggerUid` | ID of trigger that produced this event (installable triggers only). — Example: `4034124084959907503` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |

| Change ( [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |
| `changeType` | The type of change (`EDIT`, `INSERT_ROW`, `INSERT_COLUMN`, `REMOVE_ROW`, `REMOVE_COLUMN`, `INSERT_GRID`, `REMOVE_GRID`, `FORMAT`, or `OTHER`). — Example: `INSERT_ROW` |
| `source` | A [`Spreadsheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet) object, representing the Sheets file to which the script is bound. — Example: `Spreadsheet` |
| `triggerUid` | ID of trigger that produced this event. — Example: `4034124084959907503` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |

| Edit ( [simple](https://developers.google.com/apps-script/guides/triggers#onedit) and [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `LIMITED` |
| `oldValue` | Cell value prior to the edit, if any. Only available if the edited range is a single cell. Is undefined if the cell had no previous content. — Example: `1234` |
| `range` | A [`Range`](https://developers.google.com/apps-script/reference/spreadsheet/range) object, representing the cell or range of cells that were edited. — Example: `Range` |
| `source` | A [`Spreadsheet`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet) object, representing the Sheets file to which the script is bound. — Example: `Spreadsheet` |
| `triggerUid` | ID of trigger that produced this event (installable triggers only). — Example: `4034124084959907503` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |
| `value` | New cell value after the edit. Only available if the edited range is a single cell. — Example: `10` |

| Form submit ( [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| **Caution:** Make sure you use this form submit trigger with `SpreadsheetTriggerBuilder`. |  |
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |
| `namedValues` | An object containing the question names and values from the form submission. — Example: `{<br>  'First Name': ['Jane'],<br>  'Timestamp': ['6/7/2015 20:54:13'],<br>  'Last Name': ['Doe']<br>}` |
| `range` | A [`Range`](https://developers.google.com/apps-script/reference/spreadsheet/range) object, representing the cell or range of cells that were edited. — Example: `Range` |
| `triggerUid` | ID of trigger that produced this event. — Example: `4034124084959907503` |
| `values` | Array with values in the same order as they appear in the spreadsheet. — Example: `['2015/05/04 15:00', 'amin@example.com', 'Bob', '27', 'Bill',<br>'28', 'Susan', '25']` |

## Google Docs events

Triggers allow Docs to respond when a user opens a document.

| Open ( [simple](https://developers.google.com/apps-script/guides/triggers#onopen) and [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `LIMITED` |
| `source` | A [`Document`](https://developers.google.com/apps-script/reference/document/document) object, representing the Docs file to which the script is bound. — Example: `Document` |
| `triggerUid` | ID of trigger that produced this event (installable triggers only). — Example: `4034124084959907503` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |

## Google Slides events

Triggers allow Slides to respond when a user opens a presentation.

| Open ( [simple](https://developers.google.com/apps-script/guides/triggers#onopen) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `LIMITED` |
| `source` | A [`Presentation`](https://developers.google.com/apps-script/reference/slides/presentation) object, representing the Slides file to which the script is bound. — Example: `Presentation` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |

## Google Forms events

The Forms-specific triggers let scripts respond when a user
edits a form or submits a response.

| Open * ( [simple](https://developers.google.com/apps-script/guides/triggers#onopen) and [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `LIMITED` |
| `source` | A [`Form`](https://developers.google.com/apps-script/reference/forms/form) object, representing the Forms file to which the script is bound. — Example: `Form` |
| `triggerUid` | ID of trigger that produced this event (installable triggers only). — Example: `4034124084959907503` |
| `user` | A [`User`](https://developers.google.com/apps-script/reference/base/user) object, representing the active user, if available ([depending on a complex set of security restrictions](https://developers.google.com/apps-script/reference/base/session#getActiveUser())). — Example: `amin@example.com` |

* This event does not occur when a user opens a form to respond, but rather
when an editor opens the form to modify it.

| Form submit ( [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| **Caution:** Make sure you use this form submit trigger with `FormTriggerBuilder`. |  |
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |
| `response` | A [`FormResponse`](https://developers.google.com/apps-script/reference/forms/form-response) object, representing the user's response to the form as a whole. — Example: `FormResponse` |
| `source` | A [`Form`](https://developers.google.com/apps-script/reference/forms/form) object, representing the Forms file to which the script is bound. — Example: `Form` |
| `triggerUid` | ID of trigger that produced this event. — Example: `4034124084959907503` |

## Google Calendar events

Google Calendar triggers fire when a user's calendar events are updated
(created, edited, or deleted).

These triggers do not tell you which event changed or how it changed.
Instead, they indicate that your code needs to do an incremental sync operation
to pick up recent changes to the calendar. For a full description
of this procedure, see the
[Synchronizing resources guide](https://developers.google.com/calendar/v3/sync) for the
[Calendar API](https://developers.google.com/calendar/overview).

To synchronize with Calendar in Apps Script,
perform the following steps:

1. Enable the [Calendar advanced service](https://developers.google.com/apps-script/advanced/calendar)
for the script project. The built-in
[Calendar service](https://developers.google.com/apps-script/reference/calendar) isn't
sufficient for this workflow.
2. Determine what calendars to synchronize. For each calendar, perform an
[initial sync](https://developers.google.com/calendar/api/guides/sync#initial_full_sync) operation using
the Calendar advanced service's
[Events.list()](https://developers.google.com/calendar/v3/reference/events/list) method.
3. The initial sync returns a `nextSyncToken` for that calendar. Store this
token for later use.
4. When the Apps Script `EventUpdated` trigger fires indicating a
calendar event change, perform an
[incremental sync](https://developers.google.com/calendar/api/guides/sync#incremental_sync) for the
affected calendar using the stored `nextSyncToken`. This is essentially
another [Events.list()](https://developers.google.com/calendar/api/v3/reference/events/list) request, but
providing the `nextSyncToken` limits the response to only events that have
changed since the last sync.
5. Examine the response of the sync to learn what events were updated and
have your code respond appropriately. For example, log the change,
update a spreadsheet, send email notices, or take other actions.
6. Update the `nextSyncToken` stored for that calendar with the one returned
by the incremental sync request. This forces the next sync operation to
only return the most current changes.

Occasionally sync tokens are invalidated by the server, resulting in a
`410` error. When this happens, your code should conduct a
[full sync](https://developers.google.com/calendar/api/guides/sync#full_sync_required_by_server)
and replace all the stored synced data and tokens for that calendar.

| EventUpdated ( [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |
| `calendarId` | The string ID of the calendar where the event update occurred. — Example: `susan@example.com` |
| `triggerUid` | ID of trigger that produced this event. — Example: `4034124084959907503` |

## Google Workspace add-on events

The [`onInstall()` trigger](https://developers.google.com/apps-script/guides/triggers#oninstall) runs
automatically when a user installs an
[add-on](https://developers.google.com/workspace/add-ons/overview).

| Install ( [simple](https://developers.google.com/apps-script/guides/triggers#oninstall) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |

## Google Chat app events

To learn about event objects in Google Chat, see
[Receive and respond to interactions with your Google Chat app](https://developers.google.com/chat/api/guides/message-formats).

## Time-driven events

[Time-driven triggers](https://developers.google.com/apps-script/guides/triggers/installable#time-driven_triggers)
(also called clock triggers) let scripts execute at a particular time or on a
recurring interval.

| Time-driven ( [installable](https://developers.google.com/apps-script/guides/triggers/installable#google_apps_triggers) ) |  |
|---|---|
| `authMode` | A value from the [`ScriptApp.AuthMode`](https://developers.google.com/apps-script/reference/script/auth-mode) enum. — Example: `FULL` |
| `day-of-month` | Between `1` and `31`. Because this property name contains dashes it must be accessed via `e['day-of-month']` rather than dot notation. — Example: `31` |
| `day-of-week` | Between `1` (Monday) and `7` (Sunday). Because this property name contains dashes it must be accessed via `e['day-of-week']` rather than dot notation. — Example: `7` |
| `hour` | Between `0` and `23`. — Example: `23` |
| `minute` | Between `0` and `59`. — Example: `59` |
| `month` | Between `1` and `12`. — Example: `12` |
| `second` | Between `0` and `59`. — Example: `59` |
| `timezone` | The time zone. — Example: `UTC` |
| `triggerUid` | ID of trigger that produced this event. — Example: `4034124084959907503` |
| `week-of-year` | Between `1` and `52`. Because this property name contains dashes it must be accessed via `e['week-of-year']` rather than dot notation. — Example: `52` |
| `year` | The year. — Example: `2015` |
