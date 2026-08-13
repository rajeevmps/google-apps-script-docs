# Web Apps

## Page Summary

- Apps Script allows you to publish scripts with a user interface as web apps accessible from a browser.
- A script needs to contain a `doGet(e)` or `doPost(e)` function that returns an `HtmlOutput` or `TextOutput` object to be published as a web app.
- Request parameters are passed to the `doGet(e)` or `doPost(e)` function via the `e` event parameter, containing information about the query string and parameters.
- You can deploy a script as a web app through the "Deploy" menu in the script project, configuring deployment settings and sharing the resulting URL.
- Web apps can be configured to execute as the script owner or the user accessing the web app, which affects permissions.

Publish the script as a web app if you build a user interface for it. For
example, a script that lets users schedule appointments with members of a
support team is best presented as a web app so that users access it directly
from their browsers.

Both [standalone scripts](https://developers.google.com/apps-script/guides/standalone) and [scripts bound to
Google Workspace applications](https://developers.google.com/apps-script/guides/bound) can be turned into
web apps, so long as they meet the following requirements.

## Requirements for web apps

A script can be published as a web app if it meets these requirements:

- It contains a `doGet` or `doPost` function.
- The function returns an [HTML service](https://developers.google.com/apps-script/guides/html)
[`HtmlOutput`](https://developers.google.com/apps-script/reference/html/html-output) object or a
[Content service](https://developers.google.com/apps-script/guides/content)
[`TextOutput`](https://developers.google.com/apps-script/reference/content/text-output) object.

## Request parameters

When a user visits an app or a program sends the app an HTTP `GET` request,
Google Apps Script runs the function `doGet`. When a program sends the app
an HTTP `POST` request, Apps Script runs `doPost` instead. In
both cases, the `e` argument represents an event parameter that can contain
information about any request parameters. The structure of the event object is
shown in the following table:

| Fields |  |
|---|---|
| `e.queryString` | The value of the query string portion of the URL, or `null` if no query string is specified — Example: `name=alice&n=1&n=2` |
| `e.parameter` | An object of key/value pairs that correspond to the request parameters. Only the first value is returned for parameters that have multiple values. — Example: `{"name": "alice", "n": "1"}` |
| `e.parameters` | An object similar to `e.parameter`, but with an array of values for each key — Example: `{"name": ["alice"], "n": ["1", "2"]}` |
| `e.pathInfo` | The URL path after `/exec` or `/dev`. For example, if the URL path ends in `/exec/hello`, the path info is `hello`. |
| `e.contextPath` | Not used, always the empty string. |
| `e.contentLength` | The length of the request body for POST requests, or `-1` for GET requests — Example: `332` |
| `e.postData.length` | The same as `e.contentLength` — Example: `332` |
| `e.postData.type` | The MIME type of the POST body — Example: `text/csv` |
| `e.postData.contents` | The content text of the POST body — Example: `Alice,21` |
| `e.postData.name` | Always the value "postData" — Example: `postData` |

Pass parameters such as `username` and `age` to a URL like the following:

```
https://script.google.com/.../exec?username=jsmith&age=21
```

Display the parameters like so:

```javascript
function doGet(e) {
  var params = JSON.stringify(e);
  return ContentService.createTextOutput(params).setMimeType(ContentService.MimeType.JSON);
}
```

In the preceding example, `doGet` returns the following output:

```json
{
  "queryString": "username=jsmith&age=21",
  "parameter": {
    "username": "jsmith",
    "age": "21"
  },
  "contextPath": "",
  "parameters": {
    "username": [
      "jsmith"
    ],
    "age": [
      "21"
    ]
  },
  "contentLength": -1
}
```

The following parameter names are reserved by the system and shouldn't
be used in URL parameters or POST bodies:

- `c`
- `sid`

Using these parameters can result in an HTTP 405 response with the error message
"Sorry, the file you have requested does not exist." If possible, update your
script to use different parameter names.

## Deploy a script as a web app

To deploy a script as a web app, follow these steps:

1. At the top right of the script project, click **Deploy** >
 **New deployment**.
2. Next to "Select type," click Enable deployment types
 settings > **Web app**.
3. Enter the information about your web app in the fields under "Deployment
 configuration."
4. Click **Deploy**.

Share the web app URL with those you would like to use your app, provided you
have granted them access.

Web apps deployed in one domain cease to function if their ownership
changes to a
[shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives)
or account in a different domain. This can be corrected by having the
new owner or collaborator redeploy the web app in the new domain. Alternatively,
if the web app is moved back to its original domain the web app starts
functioning again for that domain without redeploying.

## Test a web app deployment

To test your script as a web app, follow the steps below:

1. At the top right of the script project, click **Deploy > Test
 deployments**.
2. Next to "Select type," click Enable deployment types
 settings **> Web app**.
3. Under the web app URL, click **Copy**.
4. Paste the URL in your browser and test your web app.
This URL ends in `/dev` and can only be accessed by users who have edit access
to the script. This instance of the app always runs the most recently saved
code and is only intended for testing during development.

To test [granular OAuth](https://developers.google.com/apps-script/concepts/scopes#handle-granular) feature on the
web app, make sure that your project doesn't already have some authorizations.
To invalidate any existing authorizations use
[ScriptApp.invalidateAuth](https://developers.google.com/apps-script/reference/script/script-app#invalidateauth).
For any web apps that are already deployed and running
under the identity of the active user, modify the `executeAs`
JSON field in the [manifest](https://developers.google.com/apps-script/concepts/manifests#editing_a_manifest)
to `USER_DEPLOYING`.

When deploying web apps to run as the developer, exercise great care when
handling OAuth tokens obtained through
[ScriptApp.getOAuthToken](https://developers.google.com/apps-script/reference/script/script-app#getoauthtoken).
These tokens can grant other applications access to your data — never
transmit them to the client.

## Permissions

The permissions for a web app differ depending how you choose to execute
the app:

- **Execute the app as me**—In this case, the script always executes
as you, the owner of the script, no matter who accesses the web app.
- **Execute the app as user accessing the web app**—In this case, the
script runs under the identity of the active user using the web app. This
permission approach causes the web app to show the email of the script owner
when the user authorizes access.

When running a web app under the identity of the accessing user, that user is
presented with the granular OAuth consent screen. Because users can selectively
grant or deny specific scopes in this screen, we recommend that your script
executes checks (using `ScriptApp.getAuthorizationInfo`) to ensure all necessary
scopes are granted before attempting service calls. For details on handling
missing scopes programmatically, see
[Handle granular OAuth permissions](https://developers.google.com/apps-script/concepts/scopes#handle-granular).

To prevent abuse, Apps Script imposes limits on the rate at which
new users can authorize a web app that executes as the user. These limits
depend, among other factors, on whether the publishing account is part of a
[Google Workspace](https://gsuite.google.com/) domain.

Collaborate on web apps using
[shared drive](https://developers.google.com/apps-script/guides/collaborating#collaborating_with_shared_drives).
When a web app in a shared drive is deployed, choosing to "execute as you"
causes the web app to execute under the authority of the user that deployed it
(since there is no script owner).

## Embed your web app in Google Sites {:#embed-web-app}

Embedded web apps are still subject to access permissions to prevent malicious
use. If your embedded web app doesn't seem to be working, check to see if the
permissions set by the web app owner and the domain administrator allow its use.

In order to embed a web app in Sites, it must first be
deployed. You also need the **Deployed URL**
from the **Deploy** dialog.

To embed a web app into a [Sites](https://sites.google.com/new)
page, follow these steps:

1. Open the Sites page where you'd like to add the web app.
2. Select **Insert > Embed URL**.
3. Paste in the web app URL and then click **ADD**.

The web app appears in a frame in the page's preview. When you publish the page,
your site viewers may need to authorize the web app before it executes
normally. Unauthorized web apps present authorization prompts to the user.

## Web Apps and Browser History

To simulate a multi-page application, or one with a dynamic UI controlled using
URL parameters, define a state object to represent the app's UI or page, and
push the state into the browser history as the user navigates your app. Listen
to history events so that your web app displays the correct UI when the user
navigates back and forth with the browser buttons. By querying the URL
parameters at load time, have your app dynamically build its UI based on those
parameters, allowing the user to start the app in a particular state.

Apps Script provides two asynchronous client-side JavaScript APIs
to assist with creating web apps that are linked to the browser history:

- [`google.script.history`](https://developers.google.com/apps-script/guides/html/reference/history)
provides methods to allow dynamic response to browser history changes. This
includes: pushing states (simple Objects you define) onto the browser
history, replacing the top state in the history stack, and setting a listener
callback function to respond to history changes.
- [`google.script.url`](https://developers.google.com/apps-script/guides/html/reference/url) provides
the means to retrieve the current page's URL parameters and URL fragment, if
they are present.

These history APIs are only available to web apps. They are not supported for
sidebars, dialogs or add-ons. This functionality is also not
recommended for use in web apps embedded in a Sites.
