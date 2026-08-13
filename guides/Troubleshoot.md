# Troubleshoot authentication and authorization issues

This page describes some common issues that you might encounter involving
authentication and authorization.

## `This app isn't verified`

If the OAuth consent screen displays the warning "This app isn't verified," your
app is requesting scopes that provide access to sensitive user data. If your
application uses sensitive scopes, your app must go through the
[verification process](https://support.google.com/cloud/answer/7454865)
to remove that warning and other limitations. During the development phase, you
can continue past this warning by selecting **Advanced \> Go to {Project Name}
(unsafe)**.

## `File not found error for credentials.json`

When running the code sample, you might receive a "file not found" or "no such
file" error message regarding credentials.json.

This error occurs when you have not authorized the desktop application
credentials. To learn how to create credentials
for a desktop application, go to
[Create credentials](https://developers.google.com/workspace/guides/create-credentials#desktop-app).

After you create the credentials, make sure the downloaded JSON file is saved as
`credentials.json`. Then move the file to your working directory.

## `Token has been expired or revoked`

When running the code sample, you might receive a "Token has been expired" or
"Token has been revoked" error message.

This error occurs when an access token from the Google Authorization Server has
either expired or has been revoked. For information about potential causes
and fixes, see
[Refresh token expiration](https://developers.google.com/identity/protocols/oauth2#expiration).

## JavaScript errors

The following are some common JavaScript errors.

### `Error: origin_mismatch`

This error occurs during the authorization flow if the host and port used
to serve the web page doesn't match an allowed JavaScript origin on your
Google Cloud console project. Make sure you set an authorized
JavaScript origin and that the URL in your browser matches the origin URL.

### `idpiframe_initialization_failed: Failed to read the 'localStorage' property from 'Window'`

This error occurs when third-party cookies and data storage aren't enabled
in your browser. These options are required by the Google Sign-in library. For
more information, see
[3rd-party cookies and data storage](https://developers.google.com/identity/sign-in/web/troubleshooting#third-party_cookies_and_data_blocked).

> [!NOTE]
> **Note:** In your own app, you should prompt users to enable third-party cookies and data storage or add an exception for `accounts.google.com`.

### `idpiframe_initialization_failed: Not a valid origin for the client`

This error occurs when the domain registered doesn't match the domain being
used to host the web page. Ensure that the origin you registered matches the URL
in the browser.