# Build a Google Chat app with a Gemini Enterprise AI agent

This page explains how to build a Google Workspace add-on that works in Google Chat and interfaces with a [Gemini Enterprise](//docs.cloud.google.com/gemini/enterprise/docs/get-started) AI agent.

**Note:** In Google Chat, add-ons appear to users as Google Chat apps. You can also build your Chat app using _Google Chat API interaction events_. To learn more, see the [Extend Google Chat overview](/workspace/add-ons/chat).

AI agents autonomously perceive their environment, reason, and execute complex, multi-step actions to achieve a defined goal. In this tutorial, you use [the Idea Generation agent](//docs.cloud.google.com/gemini/enterprise/docs/idea-generation) provided by default by Google that helps with innovation and problem-solving for enterprise users.

![Idea Generation agent as Chat app.](/static/workspace/add-ons/images/quickstart-ge-agent.png)

The following diagram shows the architecture and messaging pattern:

![Architecture of a Chat app implemented with a Gemini Enterprise AI agent.](/static/workspace/add-ons/images/design-patterns/ge-agent.svg)

In the preceding diagram, a user interacting with a Chat app implemented with a Gemini Enterprise AI agent has the following flow of information:

1.  A user sends a message to a Chat app, either in a direct message or in a Chat space.
2.  The Chat app logic that's implemented either in Apps Script or as a web server with HTTP endpoints receives and processes the message.
3.  The Gemini Enterprise AI agent receives and processes the interaction.
4.  Optionally, the Chat app or AI agent can integrate with Google Workspace services, such as Calendar or Sheets, or other Google services, such as Google Maps or YouTube.
5.  The Chat app asynchronously sends responses using the Google Chat API to communicate the AI agent progress.
6.  The responses are delivered to the user.

## Objectives

*   Set up your environment.
*   Deploy the Chat app.
*   Configure the Chat app.
*   Test the Chat app.

## Prerequisites

*   A Business or Enterprise [Google Workspace](https://support.google.com/a/answer/6043576) account with access to [Google Chat](https://workspace.google.com/products/chat/).
*   A Google Cloud project with billing enabled. To check that an existing project has billing enabled, see [Verify the billing status of your projects](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled). To create a project and set up billing, see [Create a Google Cloud project](/workspace/guides/create-project).
*   A [Gemini Enterprise app](//docs.cloud.google.com/gemini/enterprise/docs/create-app) set up with Google Identity as identity provider.

## Set up your environment

### Turn on the Chat API

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

In the Google Cloud console, enable the Google Chat API.

### Configure the OAuth consent screen

All apps using OAuth 2.0 require a consent screen configuration. Configuring your app's OAuth consent screen defines what is displayed to users and app reviewers, and registers your app so you can publish it later.

1.  In the Google API Console, go to Menu menu > **Google Auth platform** > **Branding**.

2.  If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in [Branding](https://console.developers.google.com/auth/branding), [Audience](https://console.developers.google.com/auth/audience), and [Data Access](https://console.developers.google.com/auth/scopes). If you see a message that says **Google Auth platform not configured yet**, click **Get Started**:

    1.  Under **App Information**, in **App name**, enter a name for the app.
    2.  In **User support email**, choose a support email address where users can contact you if they have questions about their consent.
    3.  Click **Next**.
    4.  Under **Audience**, select **Internal**.
    5.  Click **Next**.
    6.  Under **Contact Information**, enter an **Email address** where you can be notified about any changes to your project.
    7.  Click **Next**.
    8.  Under **Finish**, review the [Google API Services User Data Policy](https://developers.google.com/terms/api-services-user-data-policy) and if you agree, select **I agree to the Google API Services: User Data Policy**.
    9.  Click **Continue**.
    10.  Click **Create**.

3.  For now, you can skip adding scopes. In the future, when you create an app for use outside of your Google Workspace organization, you must change the **User type** to **External**. Then add the authorization scopes that your app requires. To learn more, see the full [Configure OAuth consent](/workspace/guides/configure-oauth-consent) guide.

### Create a service account in Google Cloud console

Create a new service account with the role `Discovery Engine User` by following these steps:

#### Google Cloud Console

1.  In the Google Cloud Console, go to Menu menu > **IAM & Admin** > **Service Accounts**.

    The remaining steps appear in the Google Cloud Console.

2.  Select a Google Cloud project.
3.  Click **Create service account**.
4.  Enter a service account name to display in the Google Cloud Console.

    Note: By default, Google creates a unique service account ID based on the service account name. You can modify the ID in the service account ID field. You cannot change the ID later.

5.  If you don't want to set access controls now, click **Done** to finish creating the service account. To set access controls now, click **Create and continue** and proceed to the next step.

    **Note:** Granting access control here only affects Google Cloud resources. Google Workspace resources (such as Google Sheets and Google Drive) are shared and configured separately.

6.  Optional: Assign roles to your service account to grant access to your Google Cloud project's resources in addition to Google Workspace resources. For more details, refer to [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access).
7.  Click **Continue**.
8.  Optional: Enter users or groups that can manage and perform actions with this service account. For more details, refer to [Service account impersonation](https://docs.cloud.google.com/iam/docs/service-account-impersonation).
9.  Click **Done** to finish creating the service account.

    Make a note of the email address for the service account.

#### gcloud CLI

1.  Create the service account:

    ```
    gcloud iam service-accounts create SERVICE_ACCOUNT_NAME \
      --display-name="SERVICE_ACCOUNT_NAME"
    ```

2.  Optional: Assign roles to your service account to grant access to your Google Cloud project's resources in addition to Google Workspace resources. For more details, refer to [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access).

The service account appears on the service account page.

### Create a private key

**Warning:** This example uses an exported service account key for simplicity's sake. Exporting a private key is not recommended in production because it shouldn't be stored in an insecure location, such as source control.

To learn more about secure service account implementations and best practices, see [Choose when to use service accounts](https://cloud.google.com/iam/docs/best-practices-for-using-and-managing-service-accounts#choose-when-to-use).

To create and download a private key for the service account, follow these steps:

1.  In the Google Cloud Console, go to Menu menu > **IAM & Admin** > **Service Accounts**.

    The remaining steps appear in the Google Cloud Console.

2.  Select a Google Cloud project.
3.  Click the email address of the service account that you want to create a key for.
4.  Click the **Keys** tab.
5.  Click the **Add key** drop-down menu, then select **Create new key**.
6.  Select **JSON** as the **Key type** and click **Create**.

    Your new public/private key pair is generated and downloaded to your machine as a service account key file. Save the downloaded JSON file as `credentials.json` in your working directory. This file is the only copy of this key. After you download the key file, you cannot download it again. For information about how to store your key securely, see [Best practices for managing service account keys](https://docs.cloud.google.com/iam/docs/best-practices-for-managing-service-account-keys).

For more information about service accounts, see [service accounts in the Google Cloud IAM documentation](https://cloud.google.com/iam/docs/service-accounts).

## Create and configure the Chat app project

1.  In the Google API Console, go to Menu menu > **IAM & Admin** > **Settings**.

2.  Note the **Project number** and **Project ID** fields.

3.  Go to Gemini Enterprise.

4.  Note the **Location** and **ID** of the application.

5.  Click the following button to open the **GE AI Agent Quickstart** Apps Script project.

    [Open the project](https://script.google.com/d/1YeDvZtq5c5TU2DXFVCNGjA6RCVkUn5x0ip5QVksmSwgsy7gwpI7izPLt/edit?usp=sharing)

6.  Click **Overview** > **Make a copy**.

7.  In your Apps Script project, click **Project Settings** > **Edit script properties** > **Add script property** to add the following script properties:

    1.  `REASONING_ENGINE_RESOURCE_NAME` with the Gemini Enterprise app resource composed with the information noted in previous steps.

        ```
        projects/PROJECT_ID/locations/APP_LOCATION/collections/default_collection/engines/APP_ID
        ```

    2.  `SERVICE_ACCOUNT_KEY` with the JSON key from the service account downloaded in previous steps such as `{ ... }`.

8.  Click **Save script properties**

9.  In your Apps Script project, click **Project Settings**.

10.  Under **Google Cloud Platform (GCP) Project**, click **Change project**.

11.  In **GCP project number**, paste the Google Cloud project number noted in previous steps.

12.  Click **Set project**. The Cloud project and Apps Script project are now connected.

## Create a test deployment

You need a deployment ID for this Apps Script project, so that you can use it in the next step.

To get the head deployment ID, do the following:

1.  In the Chat app Apps Script project, click **Deploy** > **Test deployments**.
2.  Under **Head deployment ID**, click **Copy**.
3.  Click **Done**.

## Configure the Chat app

Using your Apps Script deployment, follow these steps to deploy the Google Chat app for testing:

1.  In the [API Console](https://console.developers.google.com/), search for `Google Chat API`, and click **Google Chat API**.
2.  Click **Manage**.
3.  Click **Configuration** and set up the Chat app:

    1.  In the **App name** field, enter `GE Quickstart`.
    2.  In the **Avatar URL** field, enter `https://developers.google.com/workspace/add-ons/images/quickstart-app-avatar.png`.
    3.  In the **Description** field, enter `GE Quickstart`.
    4.  Under **Functionality**, select **Join spaces and group conversations**.
    5.  Under Connection settings, select **Apps Script project**.
    6.  In the **Deployment ID** field, paste the Head deployment ID that you previously copied.
    7.  Under Visibility, select **Specific people and groups in your domain**, and enter your email.
4.  Click **Save**.

The Chat app is ready to respond to messages.

## Test the Chat app

To test your Chat app, open a direct message space with the Chat app and send a message:

1.  Open Google Chat using the Google Workspace account that you provided when you added yourself as a trusted tester.

2.  Click add **New chat**.
3.  In the **Add 1 or more people** field, type the name of your Chat app.
4.  Select your Chat app from the results. A direct message opens.

    **Note:** If you don't see your Chat app in the list of results, ensure that you've included your Google Workspace account in the **Visibility** settings of the [**Chat API Configuration**](/workspace/chat/configure-chat-api) page in the Google API Console.

5.  In the new direct message with the app, type `I need to find ideas!` and press `enter`.

    The Chat app replies with **Default Idea Generation** agent response.

## Troubleshoot

When a Google Chat app or [card](/workspace/chat/create-messages#create) returns an error, the Chat interface surfaces a message saying "Something went wrong." or "Unable to process your request." Sometimes the Chat UI doesn't display any error message, but the Chat app or card produces an unexpected result; for example, a card message might not appear.

Although an error message might not display in the Chat UI, descriptive error messages and log data are available to help you fix errors when error logging for Chat apps is turned on. For help viewing, debugging, and fixing errors, see [Troubleshoot and fix Google Chat errors](/workspace/chat/troubleshoot).

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, we recommend that you delete the Cloud project.

**Caution:** Deleting a project has the following effects:

*   **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
*   **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1.  In the Google API Console, go to the **Manage resources** page. Click **Menu** menu > **IAM & Admin** > **Manage Resources**.

2.  In the project list, select the project you want to delete and then click **Delete** delete.
3.  In the dialog, type the project ID and then click **Shut down** to delete the project.

## Related topics

*   [Build Gemini Enterprise agents that are tightly integrated with Workspace data stores, APIs, and Chat apps](//codelabs.developers.google.com/ge-gws-agents)
*   [Build Vertex AI agents that are tightly integrated with Workspace data stores, APIs, and Chat apps](//codelabs.developers.google.com/vertexai-gws-agents)
*   [Build a Google Chat app with an ADK AI agent](/workspace/add-ons/chat/quickstart-adk-agent)
*   [Build a Google Chat app with an ADK AI agent exposed by A2A](/workspace/add-ons/chat/quickstart-a2a-agent)
*   [Build a Google Chat app with an ADK AI agent exposed by A2UI](/workspace/add-ons/chat/quickstart-a2ui-agent)
*   [Fact-check statements with an ADK AI agent and Gemini model](/apps-script/samples/custom-functions/fact-check)
*   [Plan travels with an AI agent accessible across Google Workspace](/workspace/add-ons/samples/travel-concierge)
*   [Integrate fundamental AI concepts in Chat apps](//codelabs.developers.google.com/chat-apps-ai-concepts)
*   [Answer questions based on Chat conversations with a Gemini AI Chat app](/workspace/add-ons/samples/tutorial-ai-knowledge-assistant)
*   [Respond to incidents with Google Chat, Vertex AI, Apps Script, and user authentication](/workspace/add-ons/samples/tutorial-incident-response-user-auth)
*   [Manage projects with Google Chat, Vertex AI, and Firestore](/workspace/add-ons/samples/tutorial-project-management)
