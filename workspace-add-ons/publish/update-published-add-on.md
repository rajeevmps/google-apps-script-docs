# Update and manage a published add-on

- To deploy a new version of your add-on, you need to make changes to the code, test it, and create a new version for deployment.
- When creating a new version, ensure you select "New version" instead of "New deployment" to avoid disabling existing triggers.
- If you add new scopes to your add-on's manifest, you must update the scopes listed in the Google Workspace Marketplace SDK and the OAuth consent screen.
- For Editor add-ons, update the version number on the App Configuration page of the Google Workspace Marketplace SDK.
- Users do not need to reinstall the add-on for a new version, but they need to authorize any newly added scopes.

To change or unpublish the Google Workspace Marketplace listing, see [Update, unpublish, or check publication status](/workspace/marketplace/manage-app-listing). To deploy a new version of add-on code, follow these steps:

1. Change the code.
2. Test the add-on using a head deployment.
3. To publish, create a new version for the deployment. From the Apps Script project, follow these steps:

   1. At the top, click **Deploy** > **Manage deployments**.
   2. Select the active deployment to create a new version for and click Edit edit.
   3. In the **Version** section, select **New version**.
   4. Click **Deploy**.

   **Warning:** Don't select **New deployment** from the **Deploy** menu in **Step 3.a**. A new deployment generates a new deployment ID. If you update the add-on to use the new ID, the application disables all existing triggers on the previously active deployment.

4. If you add scopes in the manifest, follow these steps:

   1. Update the [scopes listed in the Google Workspace Marketplace SDK](/workspace/marketplace/enable-configure-sdk#oauth_scopes) and the OAuth consent screen to match the manifest.
   2. Submit a request for OAuth verification from the [OAuth consent screen](https://console.cloud.google.com/apis/credentials/consent/edit). If you don't reverify before publishing, the application displays a "This app isn't verified" warning to users.

5. If you're updating an Editor add-on, update the version number on the [App Configuration page of the Google Workspace Marketplace SDK](https://console.cloud.google.com/apis/api/appsmarket-component.googleapis.com/googleapps_sdk).

6. Select **Save**. The new version is published.

Users don't need to reinstall the add-on, but if you added scopes, they must authorize them.

To learn more, see [Versions](/apps-script/guides/versions).
