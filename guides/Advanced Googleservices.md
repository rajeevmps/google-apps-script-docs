# Advanced Google services

Advanced services in Google Apps Script let you connect to certain public
Google APIs with less setup than using their HTTP interfaces. Advanced services
are thin wrappers around those Google APIs. They work much like
Apps Script's [built-in services](https://developers.google.com/apps-script/guides/services)---for example, they
offer autocomplete, and Apps Script handles the [authorization
flow](https://developers.google.com/apps-script/guides/services/authorization) automatically. Enable an [advanced service](https://developers.google.com/apps-script/guides/services/advanced#enable) before
using it in a script.

## Enable advanced services

To use an advanced Google service, follow these instructions:

### Step 1: Enable the advanced service

Enable an advanced service using the Apps Script editor or by
editing the manifest.

#### Method A: Using the Editor

1. Open the Apps Script project.
2. At the left, click **Editor** .
3. At the left, next to **Services** , click **Add a service** .
4. Select an advanced Google service and click **Add**.

#### Method B: Using the manifest

Enable advanced services by editing the [manifest
file](https://developers.google.com/apps-script/concepts/manifests). For example, to enable the
Google Drive advanced service, add the `enabledAdvancedServices` field to the
`dependencies` object:

    {
      "timeZone": "America/Denver",
      "dependencies": {
        "enabledAdvancedServices": [
          {
            "userSymbol": "Drive",
            "version": "v3",
            "serviceId": "drive"
          }
        ]
      },
      "exceptionLogging": "STACKDRIVER",
      "runtimeVersion": "V8"
    }

After you enable an advanced service, it's available in autocomplete.

### Step 2: Enable the Google Cloud API (Standard Google Cloud project projects only)

If using a default Google Cloud project (created automatically by
Apps Script), skip this step. The API is enabled
automatically when you add the service in Step 1.

If using a [standard
Google Cloud project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects),
manually enable the API corresponding to the advanced service. To
enable the API manually:

1. Open the Cloud project associated with your script in the [\*\*
   Google Cloud console\*\*](https://console.developers.google.com/apis/dashboard)

2. At the top of the console, click into the search bar and type part of the
   name of the API (for example, "Calendar"), then click the
   name once you see it.

3. Click **Enable API**.

4. Close the Google Cloud console and return to the script editor.

## How method signatures are determined

Advanced services generally use the same objects, method names, and parameters
as the corresponding public APIs, although method signatures are translated for
use in Apps Script. The script editor [autocomplete
function](https://developers.google.com/apps-script/guides/services#using_autocomplete) usually provides
enough information to get started. The following rules explain how
Apps Script generates a method signature from a public Google
API.

Requests to Google APIs can accept a variety of different types of data,
including path parameters, query parameters, a request body, or a media upload
attachment. Some advanced services can also accept specific HTTP request headers
(for example, the [Calendar advanced
service](https://developers.google.com/apps-script/advanced/calendar)).

The corresponding method signature in Apps Script has the following
arguments:

1. The request body (usually a resource), as a JavaScript object.
2. Path or required parameters, as individual arguments. If the method requires multiple path parameters, they appear in the order they are listed in the API endpoint URL.
3. The media upload attachment, as a [`Blob`](https://developers.google.com/apps-script/reference/base/blob) argument.
4. Optional parameters (typically query parameters), as a JavaScript object mapping parameter names to values.
5. HTTP request headers, as a JavaScript object mapping header names to header values.

If the method doesn't have any items in a given category, that part of the
signature is omitted.

Be aware of these exceptions:

- For methods that accept a media upload, the parameter `uploadType` is set automatically.
- Methods named `delete` in the Google API are named `remove` in Apps Script, since `delete` is a reserved word in JavaScript.
- If an advanced service is configured to accept HTTP request headers, and you set a request headers JavaScript object, then you must also set the optional parameters JavaScript object (to an empty object if you aren't using optional parameters).

### Example: Calendar.Events.insert

To create a [Calendar
event](https://developers.google.com/calendar/api/v3/reference/events/insert):

The Google Calendar API documentation shows the corresponding HTTP request
structure:

- **HTTP Verb** : `POST`
- **Request URL** : `https://www.googleapis.com/calendar/v3/calendars/{calendarId}/events`
- **Request Body** : An [Event
  resource](https://developers.google.com/calendar/api/v3/reference/events#resource).

- **Query Parameters** : `sendUpdates`, `supportsAttachments`, etc.

In Apps Script, the method signature is determined by reordering
these inputs:

1. **Body**: The event resource (JavaScript object).
2. **Path** : The `calendarId` (string).
3. **Optional parameters**: The query parameters (JavaScript object).

The resulting method call looks like this:

    const event = {
      summary: 'Lunch',
      location: 'Deli',
      start: {
        dateTime: '2026-01-01T12:00:00-05:00'
      },
      end: {
        dateTime: '2026-01-01T13:00:00-05:00'
      }
    };
    const calendarId = 'primary';
    const optionalArgs = {
      sendUpdates: 'all'
    };

    Calendar.Events.insert(event, calendarId, optionalArgs);

## Advanced services or HTTP?

Each advanced Google service is associated with a public Google API. In
Apps Script, access these APIs using advanced services or
by making the API requests directly using
[`UrlFetch`](https://developers.google.com/apps-script/reference/url-fetch).

**If you use the advanced service method** , Apps Script handles
the [authorization flow](https://developers.google.com/apps-script/guides/services/authorization) and offers autocomplete support.
Enable the [advanced service](https://developers.google.com/apps-script/guides/services/advanced#enable) before using it.

**If you use the `UrlFetch` method to access the API directly** , you
essentially treat the Google API as an [external API](https://developers.google.com/apps-script/guides/services/external). With this
method, use all aspects of the API. However, you must handle the API
authorization.

The following table compares the two methods:

| Feature | Advanced Service | UrlFetch (HTTP) |
|---|---|---|
| **Authorization** | Handled automatically | Manual handling required |
| **Autocomplete** | Available | Not available |
| **Functionality Scope** | May be a subset of the API | Full access to all API features |
| **Complexity** | Easier | More complex (requires constructing headers and parsing responses) |

### Code comparison

The code samples show the difference in complexity between creating a
Calendar event using the advanced service versus using
`UrlFetchApp`.

**Advanced Service:**

    const event = {
      summary: 'Lunch',
      location: 'Deli',
      start: { dateTime: '2026-01-01T12:00:00-05:00' },
      end: { dateTime: '2026-01-01T13:00:00-05:00' }
    };

    const optionalArgs = {
      sendUpdates: 'all'
    };

    Calendar.Events.insert(event, 'primary', optionalArgs);

**UrlFetch (HTTP):**

    const event = {
      summary: 'Lunch',
      location: 'Deli',
      start: { dateTime: '2026-01-01T12:00:00-05:00' },
      end: { dateTime: '2026-01-01T13:00:00-05:00' }
    };
    const url = 'https://www.googleapis.com/calendar/v3/calendars/primary/events?sendUpdates=all';
    const options = {
      method: 'post',
      contentType: 'application/json',
      headers: {
        Authorization: `Bearer ${ScriptApp.getOAuthToken()}`
      },
      payload: JSON.stringify(event)
    };

    UrlFetchApp.fetch(url, options);

For the `UrlFetchApp` method, manually specify the required
[OAuth scopes](https://developers.google.com/apps-script/concepts/scopes) in the script's [manifest
file](https://developers.google.com/apps-script/concepts/manifests).

Use an advanced service whenever possible and only use the
`UrlFetch` method when the advanced service isn't available or doesn't provide
the functionality you need.

## Support for advanced services

Because advanced services are thin wrappers around Google APIs, any issue
encountered while using them is usually an issue with the underlying API, not
with Apps Script.

If you encounter a problem while using an advanced service, report it using the
support instructions for the underlying API.