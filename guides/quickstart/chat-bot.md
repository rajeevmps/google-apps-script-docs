# Build a Google Chat app with Google Apps Script

## Page Summary

- Create a Google Chat app that echoes user messages using Apps Script and Google Cloud.
- This involves setting up your environment, configuring the script, publishing the app, and testing its functionality.
- Prerequisites include a Google Workspace account and a Google Cloud project.
- The app is designed to receive direct messages and participate in spaces, integrating with various Google services as needed.
- You can find troubleshooting information and cleanup instructions in the provided documentation.

**Note:** This guide explains how to build an interactive Chat app using _Chat API interaction events_. You can also build your Chat app as a Google Workspace add-on. To learn about which framework to use, see [Build an interactive Google Chat app](https://developers.google.com/workspace/chat/interact-users-overview).

Create a Google Chat app that you can directly message and that responds by echoing your messages.

The following diagram shows the architecture and messaging pattern:

![Architecture of a Chat app implemented with Apps Script.](https://developers.google.com/static/workspace/chat/images/design-patterns/gsuite-via-appsscript.svg)

In the preceding diagram, a user interacting with an Apps Script Chat app has the following flow of information:

1. A user sends a message to a Chat app, either in a direct message or in a Chat space.
2. The Chat app logic that's implemented in Apps Script, which resides in Google Cloud, receives and processes the message.
3. Optionally, the Chat app logic can integrate with Google Workspace services, such as a Calendar or Sheets, or other Google Services, such as Google Maps or YouTube.
4. The Chat app logic sends a response back to the Chat app service in Chat.
5. The response is delivered to the user.

## Objectives

- Set up your environment.
- Set up the script.
- Configure the Chat app.
- Test the Chat app.

## Prerequisites

- A Business or Enterprise [Google Workspace](https://support.google.com/a/answer/6043576) account with access to [Google Chat](https://workspace.google.com/products/chat/).
- A Google Cloud project. To create one, see [Create a Google Cloud project](https://developers.google.com/workspace/guides/create-project).

## Set up your environment

### Open your Cloud project in the Google Cloud console

If it's not open already, open the Cloud project that you intend to use for this sample:

1. In the Google Cloud console, go to the **Select a project** page.

   [Select a Cloud project](https://console.cloud.google.com/projectselector2)

2. Select the Google Cloud project you want to use. Or, click **Create project** and follow the on-screen instructions. If you create a Google Cloud project, you might need to [turn on billing for the project](https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project).

### Turn on the Chat API

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

- In the Google Cloud console, enable the Google Chat API.

  [Enable the API](https://console.cloud.google.com/flows/enableapi?apiid=chat.googleapis.com)

### Configure the OAuth consent screen

All apps using OAuth 2.0 require a consent screen configuration. Configuring your app's OAuth consent screen defines what is displayed to users and app reviewers, and registers your app so you can publish it later.

1. In the Google API Console, go to Menu menu > **Google Auth platform** > **Branding**.

   [Go to Branding](https://console.developers.google.com/auth/branding)

2. If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in [Branding](https://console.developers.google.com/auth/branding), [Audience](https://console.developers.google.com/auth/audience), and [Data Access](https://console.developers.google.com/auth/scopes). If you see a message that says **Google Auth platform not configured yet**, click **Get Started**:

3. Under **App Information**, in **App name**, enter a name for the app.

4. In **User support email**, choose a support email address where users can contact you if they have questions about their consent.

5. Click **Next**.

6. Under **Audience**, select **Internal**.

7. Click **Next**.

8. Under **Contact Information**, enter an **Email address** where you can be notified about any changes to your project.

9. Click **Next**.

10. Under **Finish**, review the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy) and if you agree, select **I agree to the Google API Services: User Data Policy**.

11. Click **Continue**.

12. Click **Create**.

13. For now, you can skip adding scopes. In the future, when you create an app for use outside of your Google Workspace organization, you must change the **User type** to **External**. Then add the authorization scopes that your app requires. To learn more, see the full [Configure OAuth consent](https://developers.google.com/workspace/guides/configure-oauth-consent) guide.

## Set up the script

To set up the script, you use a template and then set your Cloud project in Apps Script.

### Create the script from the template

1. Go to the [Apps Script **Getting Started** page](https://script.google.com/home/start).
2. Click the **Chat App** template at the top of the page.
3. Click **Untitled project**, type `Quickstart app`, and click **Rename**.

In the future, if you want to use certain Google APIs or publish your app, you must associate your Cloud project with your Apps Script project. For this guide, you don't need to do so. To learn more, see the [Google Cloud projects guide](https://developers.google.com/apps-script/guides/cloud-platform-projects).

### Create a test deployment

You need a deployment ID for this Apps Script project, so that you can use it in the next step.

To get the head deployment ID, do the following:

1. In the Chat app Apps Script project, click **Deploy** > **Test deployments**.
2. Copy the **Head deployment ID** for use in a later step and click **Done**.

## Configure the Chat app

Configure the Chat app from the API Console.

1. In the [API Console](https://console.developers.google.com/), search for `Google Chat API`, and click **Google Chat API**.
2. Click **Manage**.
3. Click **Configuration** and set up the Chat app:

   1. Clear **Build this Chat app as a Google Workspace add-on**. A dialog opens asking you to confirm. In the dialog, click **Disable**.
   2. In the **App name** field, enter `Quickstart app`.
   3. In the **Avatar URL** field, enter `https://developers.google.com/chat/images/quickstart-app-avatar.png`.
   4. In the **Description** field, enter `Quickstart app`.
   5. Under **Functionality**, select **Join spaces and group conversations**.
   6. Under Connection settings, select **Apps Script**.
   7. In the **Deployment ID** field, paste the Head deployment ID that you previously copied.
   8. Under Visibility, select **Specific people and groups in your domain**, and enter your email.

4. Click **Save**.

The Chat app is ready to respond to messages.

## Test the Chat app

To test your Chat app, open a direct message space with the Chat app and send a message:

1. Open Google Chat using the Google Workspace account that you provided when you added yourself as a trusted tester.

   [Go to Google Chat](https://chat.google.com)

2. Click add **New chat**.
3. In the **Add 1 or more people** field, type the name of your Chat app.
4. Select your Chat app from the results. A direct message opens.

   **Note:** If you don't see your Chat app in the list of results, ensure that you've included your Google Workspace account in the **Visibility** settings of the [**Chat API Configuration**](https://developers.google.com/workspace/chat/configure-chat-api) page in the Google API Console.

5. In the new direct message with the app, type `Hello` and press `enter`.

   The Chat app thanks you for adding it and echoes your message.

To add trusted testers and learn more about testing interactive features, see [Test interactive features for Google Chat apps](https://developers.google.com/workspace/chat/test-interactive-chat-apps).

## Troubleshoot

When a Google Chat app or [card](https://developers.google.com/workspace/chat/create-messages#create) returns an error, the Chat interface surfaces a message saying "Something went wrong." or "Unable to process your request." Sometimes the Chat UI doesn't display any error message, but the Chat app or card produces an unexpected result; for example, a card message might not appear.

Although an error message might not display in the Chat UI, descriptive error messages and log data are available to help you fix errors when error logging for Chat apps is turned on. For help viewing, debugging, and fixing errors, see [Troubleshoot and fix Google Chat errors](https://developers.google.com/workspace/chat/troubleshoot).

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, we recommend that you delete the Cloud project.

**Caution:** Deleting a project has the following effects:

- **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
- **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1. In the Google API Console, go to the **Manage resources** page. Click **Menu** menu > **IAM & Admin** > **Manage Resources**.

   [Go to Resource Manager](https://console.developers.google.com/cloud-resource-manager)

2. In the project list, select the project you want to delete and then click **Delete** delete.
3. In the dialog, type the project ID and then click **Shut down** to delete the project.

## Next steps

- [Create interactive cards](https://developers.google.com/workspace/chat/api/guides/v1/messages/create#create) – Card messages support a defined layout, interactive UI elements like buttons, and rich media like images. Use card messages to present detailed information, gather information from users, and guide users to take a next step.
- [Respond to commands](https://developers.google.com/workspace/chat/commands) – Commands help users discover and use key features of your Chat app.
- [Launch dialogs](https://developers.google.com/workspace/chat/dialogs) – Dialogs are windowed, card-based interfaces that your app can open to interact with a user. Multiple cards can be strung together sequentially, which helps users complete multi-step processes, like filling in form data.
- **Codelab:** Ready to build a more advanced Chat app? See the feedback Chat app from the codelab [Build apps for Google Chat with Gemini](https://codelabs.developers.google.com/codelabs/chat-apps-gemini#2).

Source: https://developers.google.com/apps-script/quickstart/chat-bot
