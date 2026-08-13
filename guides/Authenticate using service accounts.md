# Authenticate as an Google Apps Script project using service accounts

This guide explains how to authenticate with a service account when calling APIs
in Apps Script.
A service account is a special kind of account used by an application, rather than a person. You can use a service account to access data or perform actions by the robot account, or to access data on behalf of Google Workspace or Cloud Identity users. For more information, see [Understanding service accounts](https://cloud.google.com/iam/docs/understanding-service-accounts).

For an overview about authentication for Google Workspace APIs, see
[Create access credentials](https://developers.google.com/workspace/guides/create-credentials).

### When to use service accounts in Apps Script

By default, Apps Script uses the script user's credentials to
call APIs. If you're calling Google APIs using
[`UrlFetchApp`](https://developers.google.com/apps-script/reference/url-fetch/url-fetch-app), you can get an
access token for the script user by calling
[`ScriptApp.getOAuthToken`](https://developers.google.com/apps-script/reference/script/script-app#getoauthtoken).

However, using service accounts provides several advantages over
`ScriptApp.getOAuthToken` in some scenarios. Consider using service account
authentication for these reasons:

- **Better performance with Google Cloud APIs and services**: Many Google Cloud APIs are designed for service account authentication. Service accounts can also provide a more integrated, reliable, and secure way to interact with most APIs.
- **Decoupled permissions** : Service accounts have their own permissions, separate from any user. The authentication method `ScriptApp.getOAuthToken` can fail when you share the project with other users. By using service accounts, share scripts and [publish them as Google Workspace add-ons](https://developers.google.com/workspace/add-ons/how-tos/building-workspace-addons).
- **Automated scripts and long-running tasks**: Service accounts let you run automated scripts, batch processes, or background tasks without user input.
- **Enhanced security and principle of least privilege** : Grant service accounts specific permissions, providing access only to the resources they need. This follows the **principle of least privilege** , which lowers security risks. Using `ScriptApp.getOAuthToken` often grants a script all user permissions, which can be too broad.
- **Centralized access management** : Service accounts are managed using Google Cloud's [Identity and Access Management (IAM)](https://docs.cloud.google.com/iam/docs). IAM helps Google Workspace organizations manage access to authenticated services within Apps Script projects.

## Prerequisites

- A [Google Cloud project](https://developers.google.com/workspace/guides/create-project).
- In your Cloud project, [enable any APIs](https://developers.google.com/workspace/guides/enable-apis) that you want to authenticate with using service account credentials.
- To [assign roles to service accounts](https://developers.google.com/apps-script/guides/service-account#assign-role), you must have [super administrator](https://support.google.com/a/answer/2405986#super_admin) privileges.

## Create a service account

In your Cloud project, create a service account:

### Google Cloud console

1. In the Google Cloud console, go to Menu \> **IAM \& Admin** \> **Service Accounts** .

   [Go to Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts)
2. Click **Create service account**.
3. Fill in the service account details, then click **Create and continue** .

   > [!NOTE]
   > Note: By default, Google creates a unique service account ID. If you would like to change the ID, modify the ID in the service account ID field.

4. Optional: Assign roles to your service account to grant access to your Google Cloud project's resources. For more details, refer to [Granting, changing, and revoking access to resources](https://cloud.google.com/iam/docs/granting-changing-revoking-access).
5. Click **Continue**.
6. Optional: Enter users or groups that can manage and perform actions with this service account. For more details, refer to [Managing service account impersonation](https://cloud.google.com/iam/docs/impersonating-service-accounts).
7. Click **Done**. Make a note of the email address for the service account.

### gcloud CLI

1. Create the service account:

       gcloud iam service-accounts create `SERVICE_ACCOUNT_NAME` \
         --display-name="`SERVICE_ACCOUNT_NAME`"

2. Optional: Assign roles to your service account to grant access to your Google Cloud project's resources. For more details, refer to [Granting, changing, and revoking access to resources](https://cloud.google.com/iam/docs/granting-changing-revoking-access).

### Assign a role to the service account

You must assign a prebuilt or custom role to a service account by a super
administrator account.

1. In the Google Admin console, go to Menu
   \>
   **Account** \> **Admin roles**.

   [Go to Admin roles](https://admin.google.com/ac/roles)
2. Point to the role that you want to assign, and then click **Assign admin**.

3. Click **Assign service accounts**.

4. Enter the email address of the service account.

5. Click **Add \> Assign role**.

### Create credentials for a service account

You need to obtain credentials in the form of a public/private key pair. These credentials are used by your code to authorize service account actions within your app.

To obtain credentials for your service account:

1. In the Google Cloud console, go to Menu \> **IAM \& Admin** \> **Service Accounts** .

   [Go to Service Accounts](https://console.cloud.google.com/iam-admin/serviceaccounts)
2. Select your service account.
3. Click **Keys** \> **Add key** \> **Create new key**.
4. Select **JSON** , then click **Create** .

   Your new public/private key pair is generated and downloaded to your
   machine as a new file. Save the downloaded JSON file as `credentials.json` in your
   working directory. This file is the only copy of this key. For information about how to store
   your key securely, see
   [Managing service account keys](https://cloud.google.com/iam/docs/best-practices-for-managing-service-account-keys).
5. Click **Close**.

### Copy the Cloud project number

1. In the Google Cloud console, go to Menu \> **IAM \& Admin** \> **Settings** .

   [Go to IAM \& Admin Settings](https://console.cloud.google.com/iam-admin/settings)
2. In the **Project number** field, copy the value.

## Set up service account authentication in your Apps Script project

This section explains how to add your service account credentials from your
Cloud project to an Apps Script project.

### Set your Cloud project in Apps Script

1. Go to Apps Script to open or create a project:

   <br />

   [Open Apps Script](https://script.google.com)
2. In your Apps Script project,
   click **Project Settings** ![The icon for project settings](https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/settings/default/24px.svg).

3. Under **Google Cloud project** , click **Change project**.

4. In **Google Cloud project number**, paste the Cloud project number.

5. Click **Set project**.

### Save the credentials as a script property

Securely store your service account credentials by saving
them as a [script property](https://developers.google.com/apps-script/guides/properties) in your
Apps Script project settings:

1. Copy the contents of your service account JSON file (`credentials.json`) that you created in the [previous section](https://developers.google.com/apps-script/guides/service-account#create-credentials).
2. In your Apps Script project, go to **Project Settings** .
3. From the **Project Settings** page, go to **Script Properties** and click **Add script property** and enter the following:
   - In the **Property** field, enter `SERVICE_ACCOUNT_KEY`.
   - In the **Value** field, paste the content of your JSON key file.
4. Click **Save script properties**.

### Add the OAuth2 library

To handle the OAuth2 authentication flow, use the Apps Script
library
[`apps-script-oauth2`](https://github.com/googleworkspace/apps-script-oauth2).

To add the library to your Apps Script project:

1. In the Apps Script editor, at the left, next to **Libraries** , click **Add a library** .
2. In the **Script ID** field, enter `1B7FSrk5Zi6L1rSxxTDgDEUsPzlukDsi4KGuTMorsTQHhGBzBkMun4iDF`.
3. Click **Look up**.
4. Select the latest version, and then click **Add**.

## Call an API using service account credentials

To use the service account credentials from your Apps Script
project, you can use the following function `getServiceAccountService()`:

    /**
     * Get a new OAuth2 service for a given service account.
     */
    function getServiceAccountService() {
      const serviceAccountKeyString = PropertiesService.getScriptProperties()
          .getProperty('SERVICE_ACCOUNT_KEY');

      if (!serviceAccountKeyString) {
        throw new Error('SERVICE_ACCOUNT_KEY property is not set. ' +
            'Please follow the setup instructions.');
      }

      const serviceAccountKey = JSON.parse(serviceAccountKeyString);

      const CLIENT_EMAIL = serviceAccountKey.client_email;
      const PRIVATE_KEY = serviceAccountKey.private_key;

      // Replace with the specific scopes required for your API.
      const SCOPES = ['SCOPE'];

      return OAuth2.createService('ServiceAccount')
          .setTokenUrl('https://oauth2.googleapis.com/token')
          .setPrivateKey(PRIVATE_KEY)
          .setIssuer(CLIENT_EMAIL)
          .setPropertyStore(PropertiesService.getScriptProperties())
          .setScope(SCOPES);
    }

Replace `SCOPE` with the
[authorization scope](https://developers.google.com/apps-script/concepts/scopes) that you need to call
the API. The script uses the service account credentials that you saved
as a `SERVICE_ACCOUNT_KEY` script property in the
[previous step](https://developers.google.com/apps-script/guides/service-account#save-credentials).

You can then use these credentials to call an API, as shown in the following
example with the [`UrlFetch`](https://developers.google.com/apps-script/reference/url-fetch) service:

    function callApi() {
      const service = getServiceAccountService();

      // TODO(developer): Replace with the payload
      const payload = {};

      // TODO(developer): Replace with the API endpoint
      const response = UrlFetchApp.fetch('API_URL', {
        method: 'post',
        headers: {
          'Authorization': `Bearer ${service.getAccessToken()}`,
          'Content-Type': 'application/json',
        },
        payload: payload,
      });

      const result = JSON.parse(response.getContentText());

      return result;
    }

Replace `API_URL` with the HTTP endpoint that you are
calling.

## Related topics

- [Create access credentials](https://developers.google.com/workspace/guides/create-credentials)
- [Authenticate as a Google Chat app](https://developers.google.com/workspace/chat/authenticate-authorize-chat-app#apps-script)