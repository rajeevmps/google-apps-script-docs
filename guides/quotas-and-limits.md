# Quotas for Google Services

## Page Summary

- Apps Script services have daily quotas and limitations that can cause scripts to throw an exception and stop execution if exceeded.
- Some features have additional quotas from associated Google products, and exceeding any of these associated quotas makes the feature unavailable.
- Quotas are set at different levels for consumer/G Suite free edition and Google Workspace accounts, are per user, and reset 24 hours after the first request.
- Quotas and limits are subject to change at any time without notice and are provided to help test scripts.
- Reaching a quota or limitation will result in an exception message indicating the specific limit exceeded or service invoked too many times.

Google Apps Script services have daily quotas and limitations on some
features. If you exceed a quota or limitation, your script throws an exception
and execution stops.

Some features have additional quotas from their associated Google product. Using
a product's Apps Script service counts toward all associated
quota reserves. A feature becomes unavailable if you reach any of the associated
quotas.

## Current quotas

Quotas are set at different levels for users of consumer accounts (such as
gmail.com) and Google Workspace accounts.
Quotas are per user and reset 24 hours after the first request.

Use the following quotas to help test your scripts. All quotas are subject to
elimination, reduction, or change at any time, without notice.

| Feature | Consumer accounts (for example, gmail.com) | Google Workspace accounts |
|---|---|---|
| Calendar events created | 5,000 / day | 10,000 / day |
| Contacts created | 1,000 / day | 2,000 / day |
| Documents created | 250 / day | 1,500 / day |
| Files converted | 2,000 / day | 4,000 / day |
| Email recipients per day (for example, with MailApp) | 100 * / day | 1,500 * / day |
| Email recipients per day within domain (for example, with MailApp) | 100 * / day | 2,000 / day |
| Email read/write (excluding send) | 20,000 / day | 50,000 / day |
| Groups read | 2,000 / day | 10,000 / day |
| JDBC connection | 10,000 / day | 50,000 / day |
| JDBC failed connection | 100 / day | 500 / day |
| Presentations created | 250 / day | 1,500 / day |
| Properties read/write | 50,000 / day | 500,000 / day |
| Slides created | 250 / day | 1,500 / day |
| Spreadsheets created | 250 / day | 3,200 / day |
| Triggers total runtime | 90 min / day | 6 hr / day |
| URL Fetch calls | 20,000 / day | 100,000 / day |
| Static Map render | 1,000 / day | 10,000 / day |
| Google Map Direction query | 1,000 / day | 10,000 / day |
| Google Map Geocode calls | 1,000 / day | 10,000 / day |
| Translate calls | 5,000 / day | 20,000 / day |
| Google Map elevation samples query | 1,000 / day | 10,000 / day |
| Apps Script projects | 50 / day | 50 / day |

Additional limits apply for trial accounts. After you convert from a free trial
account to a paid subscription, your account limits automatically increase when
both of the following are true:

- Your domain has cumulatively paid at least USD $100 (or equivalent).
- At least 60 days have passed since reaching that payment threshold.

## Current limitations

Use the following limits to help test your scripts. All limits are subject to
elimination, reduction, or change at any time, without notice.

| Feature | Consumer accounts (e.g., gmail.com) | Google Workspace accounts |
|---|---|---|
| Script runtime | 6 min / execution | 6 min / execution |
| Custom function runtime | 30 sec / execution | 30 sec / execution |
| Google Workspace add-on runtime | 30 sec / execution | 30 sec * / execution |
| Simultaneous executions per user | 30 / user | 30 / user |
| Simultaneous executions per script | 1,000 | 1,000 |
| Email attachments | 250 / msg | 250 / msg |
| Email body size | 200 KB / msg | 400 KB / msg |
| Email recipients per message | 50 / msg | 50 / msg |
| Email total attachments size | 25 MB / msg | 25 MB / msg |
| Properties value size | 9 KB / val | 9 KB / val |
| Properties total storage | 500 KB / property store | 500 KB / property store |
| Triggers | 20 / user / script | 20 / user / script |
| URL Fetch response size | 50 MB / call | 50 MB / call |
| URL Fetch headers | 100 / call | 100 / call |
| URL Fetch header size | 8 KB / call | 8 KB / call |
| URL Fetch POST size | 50 MB / call | 50 MB / call |
| URL Fetch URL length | 2 KB / call | 2 KB / call |
| Versions | 200 / script | 200 / script |

## Monitor quota usage

To monitor your script's quota consumption and execution health, use the
following methods:

- **Email quota**: Use
[`MailApp.getRemainingDailyQuota()`](https://developers.google.com/apps-script/reference/mail/mail-app#getRemainingDailyQuota())
to check the number of remaining email recipients you can send to for the
rest of the day.
- **Execution monitoring**: Use the
[Apps Script dashboard](https://developers.google.com/apps-script/guides/dashboard) to view your
script's execution history and health. The **My Executions** page shows the
status (for example, `Completed`, `Failed`, or `Running`) of each script
execution. You can monitor the number of simultaneous executions by
filtering for executions with a **Status** of `Running`.
- **Google Cloud console**: If your Apps Script project uses a
[standard Google Cloud project](https://developers.google.com/apps-script/guides/cloud-projects),
you can monitor service-specific quotas and API usage in the
[Google Cloud console](https://console.cloud.google.com/apis/dashboard).

## Exception messages

If a script reaches a quota or limitation, it throws an exception with a
message similar to the following:

- **`Limit exceeded: Email Attachments Per Message.`** This indicates that the
script exceeded one of the quotas or limitations listed in the
Current quotas or
Current limitations sections.
- **`Service invoked too many times: Calendar.`** This indicates that the
script called the given service too many times in one day.
- **`Service invoked too many times in a short time: Calendar.
Try Utilities.sleep(1000) between calls.`** This indicates that the script
called the given service too many times in a short period.
- **`Service using too much computer time for one day.`** This indicates that
the script exceeded the total allowable execution time for one day. It most commonly
occurs for scripts that run on a
[trigger](https://developers.google.com/apps-script/understanding_triggers), which have a lower daily
limit than scripts executed manually.
- **`Script invoked too many times per second for this Google user account.`**
This indicates that the script began executing too many times in a short
period. It most commonly occurs for custom functions that are called
repeatedly in a single spreadsheet. To avoid this error, code your custom
functions so that they only need to be called once per range of data, as
explained in the [guide to custom
functions](https://developers.google.com/apps-script/execution_custom_functions).
- **`There are too many scripts running simultaneously for this Google user
account.`** This indicates that you have too many scripts executing at once,
although not necessarily the same script. Like the preceding exception, this
most commonly occurs for custom functions that are called repeatedly in a
single spreadsheet.

## Related topics

- [Restrictions for manifest triggers](https://developers.google.com/apps-script/add-ons/concepts/workspace-triggers#restrictions).
- [Restrictions for Editor add-ons triggers](https://developers.google.com/apps-script/add-ons/concepts/editor-triggers#restrictions_2).
