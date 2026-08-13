# Troubleshoot authentication and authorization issues

## Page Summary

- The page addresses common authentication and authorization issues like "This app isn't verified," file not found errors for `credentials.json`, expired or revoked tokens, and various JavaScript errors.
- The "This app isn't verified" warning appears if your app requests sensitive scopes and requires verification to remove limitations.
- A "File not found error for credentials.json" indicates the desktop application credentials have not been authorized and the file needs to be created and placed in the working directory.
- "Token has been expired or revoked" errors mean the access token is no longer valid and refer to documentation on refresh token expiration for solutions.
- Common JavaScript errors covered include `origin_mismatch` (origin URL doesn't match), `idpiframe_initialization_failed: Failed to read the 'localStorage' property from 'Window'` (third-party cookies blocked), and `idpiframe_initialization_failed: Not a valid origin for the client` (registered domain doesn't match hosting domain).

## `This app isn't verified`

If the OAuth consent screen displays the warning "This app isn't verified," your app is requesting scopes that provide access to sensitive user data. If your application uses sensitive scopes, your app must go through the verification process to remove that warning and other limitations. During the development phase, you can continue past this warning by selecting **Advanced > Go to {Project Name} (unsafe)**.

## `File not found error for credentials.json`

When running the code sample, you might receive a "file not found" or "no such file" error message regarding credentials.json.

This error occurs when you have not authorized the desktop application credentials. To learn how to create credentials for a desktop application, go to Create credentials.

After you create the credentials, make sure the downloaded JSON file is saved as `credentials.json`. Then move the file to your working directory.

## `Token has been expired or revoked`

When running the code sample, you might receive a "Token has been expired" or "Token has been revoked" error message.

This error occurs when an access token from the Google Authorization Server has either expired or has been revoked. For information about potential causes and fixes, see Refresh token expiration.

## JavaScript errors

The following are some common JavaScript errors.

### `Error: origin_mismatch`

This error occurs during the authorization flow if the host and port used to serve the web page doesn't match an allowed JavaScript origin on your Google Cloud console project. Make sure you set an authorized JavaScript origin and that the URL in your browser matches the origin URL.

### `idpiframe_initialization_failed: Failed to read the 'localStorage' property from 'Window'`

This error occurs when third-party cookies and data storage aren't enabled in your browser. These options are required by the Google Sign-in library. For more information, see 3rd-party cookies and data storage.

**Note:** In your own app, you should prompt users to enable third-party cookies and data storage or add an exception for `accounts.google.com`.

### `idpiframe_initialization_failed: Not a valid origin for the client`

This error occurs when the domain registered doesn't match the domain being used to host the web page. Ensure that the origin you registered matches the URL in the browser.

Source: https://developers.google.com/apps-script/api/troubleshoot-authentication-authorization
