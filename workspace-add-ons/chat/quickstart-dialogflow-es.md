# Build a Google Chat add-on with Dialogflow ES

This page explains how to build a Google Chat app as a Google Workspace Add-on that uses [Dialogflow ES](https://cloud.google.com/dialogflow/es/docs) to understand and respond to natural language. You can also use [Dialogflow CX](https://cloud.google.com/dialogflow/cx/docs), which has a direct integration with Google Chat, to build a Dialogflow CX Google Chat app by following the [Dialogflow CX Google Chat](/workspace/add-ons/chat/quickstart-dialogflow-cx) guide.

## Objectives

*   Set up your environment.
*   Create and deploy a Dialogflow ES agent.
*   Create and deploy a Chat app powered by the Dialogflow ES agent.
*   Test the Chat app.

## Prerequisites

*   A Business or Enterprise [Google Workspace](https://support.google.com/a/answer/6043576) account with access to [Google Chat](https://workspace.google.com/products/chat/).
*   A Google Cloud project with billing enabled. To check that an existing project has billing enabled, see [Verify the billing status of your projects](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled). To create a project and set up billing, see [Create a Google Cloud project](/workspace/guides/create-project).

## Architecture

The following diagram shows the architecture of a Chat app built with Dialogflow:

![Architecture of a Chat app implemented with Dialogflow.](/static/workspace/chat/images/design-patterns/gsuite-via-dialogflow.svg)

In the preceding diagram, a user interacting with a Dialogflow Chat app has the following flow of information:

1.  A user sends a message in Chat to a Chat app, either in a direct message or in a Chat space.
2.  A Dialogflow virtual agent receives and processes the message to produce a response.
3.  Optionally, using a [Dialogflow webhook](https://cloud.google.com/dialogflow/es/docs/fulfillment-webhook), the Dialogflow agent can interact with external third-party services, such as a project management system or a ticketing tool.
4.  The Dialogflow agent sends a response back to the Chat app service in Chat.
5.  The response is delivered to the Chat space.

## Set up the environment

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

1.  In the Google API Console, enable the Google Chat API and the Dialogflow API.

2.  Confirm that you're enabling the APIs in the correct Cloud project, then click **Next**.

3.  Confirm that you're enabling the correct APIs, then click **Enable**.

## Create a Dialogflow ES agent

If you don't have an existing Dialogflow ES agent:

1.  Go to the [Dialogflow ES Console](https://dialogflow.cloud.google.com).
2.  Click **Create Agent**.
3.  Give it a name, select a default language, and time zone.
4.  Associate it with your Cloud project.
5.  Click **Create**.
6.  Build your intents and entities as needed for your Chat app conversational flow. You can start with a greeting intent.
7.  Take note of your **Project ID**.

For a detailed guide, see [Build an Agent](https://cloud.google.com/dialogflow/es/docs/quick/build-agent).

## Create a Chat app and connect it with the Dialogflow agent

After creating a Dialogflow ES agent, follow these steps to turn it into a Chat app:

1.  In the Google API Console, go to Google Chat API. Search for "Google Chat API" and click **Google Chat API**, then click **Manage**.

2.  Click **Configuration** and set up the Chat app:

    1.  In **App name**, enter `Dialogflow App`.
    2.  In **Avatar URL**, enter `https://developers.google.com/workspace/chat/images/quickstart-app-avatar.png`.
    3.  In **Description**, enter `Responds to real human conversation`.
    4.  Under **Functionality**, select **Join spaces and group conversations**.
    5.  Under **Connection settings**, select **Dialogflow**.
    6.  Under **Dialogflow settings**, select **Dialogflow ES**.
    7.  **Make this Chat app available to specific people and groups** in your domain and enter your email address.
    8.  Under **Logs**, select **Log errors to Logging**.
3.  Click **Save**.

The Chat app is ready to receive and respond to messages on Chat.

## Test the Chat app

Test the Dialogflow ES Chat app by messaging it in Google Chat.

1.  Open Google Chat using the Google Workspace account that you provided when you added yourself as a trusted tester.

2.  Click add **New chat**.
3.  In the **Add 1 or more people** field, type the name of your Chat app.
4.  Select your Chat app from the results. A direct message opens.

    **Note:** If you don't see your Chat app in the list of results, ensure that you've included your Google Workspace account in the **Visibility** settings of the [**Chat API Configuration**](/workspace/chat/configure-chat-api) page in the Google API Console.

5.  In the new direct message with the app, type `Hello` and press `enter`.

    The Dialogflow Chat app responds by a greeting message.

### Text Responses

[Text responses](https://cloud.google.com/dialogflow/docs/intents-rich-messages#text) are sent to Google Chat as [Text messages](/workspace/add-ons/chat/send-messages#reply-message). With this formatting you can make text bold or italics by wrapping the text in certain (markdown light) symbols.

The text message response, visually looks the same as the Default Text Response in the Dialogflow Console. However, the raw API response will look a bit different. It also sets the platform config to _GOOGLE_HANGOUTS_, which could be interesting when building agents for multiple integrations.

```json
"fulfillmentMessages": [
    {
       "text": {
       "text": [
            "This is a test."
       ]
    },
      "platform": "GOOGLE_HANGOUTS"
    },
```

### Cards

[Card responses](https://cloud.google.com/dialogflow/docs/intents-rich-messages#card) are sent to Google Chat as [Card messages](/workspace/add-ons/chat/collect-information).

### Images

[Image responses](https://cloud.google.com/dialogflow/docs/intents-rich-messages#image) are sent to Google Chat as [Google Chat Image Widgets](https://developers.google.com/chat/ui/widgets/image).

### Custom Payload

To send other types of Google Chat messages, you can use a [custom payload](https://docs.cloud.google.com/dialogflow/es/docs/intents-rich-messages#custom).

Google Chat Custom Payload lets you create more advanced cards. One card can have one or many sections. Each section could have a header. You can have a look into the [Google Workspace Add-on extend Chat cards reference guide](/workspace/add-ons/chat/collect-information), to see some of the combinations you can create with this. However, using custom payloads means that you will have to provide the JSON format.

**Note:** When you copy and paste the examples from the reference guide to the custom payload box in Dialogflow, make sure the editor doesn't contain any linting errors. You can't test the results in the Dialogflow Simulator but can test it directly in Google Chat.

Here is an example of a custom payload for creating a message with a card:

```json
{ "hangouts": { "hostAppDataAction": { "chatDataAction": {
  "createMessageAction": { "message": { "cardsV2": [{
    "cardId": "pizza",
    "card": {
      "header": {
        "title": "Pizza Delivery Customer Support",
        "subtitle": "pizzadelivery@example.com",
        "imageUrl": "https://goo.gl/aeDtrS"
      },
      "sections": [{ "widgets": [{ "textParagraph": {
        "text": " Your pizza is here!"
      }}]}]
    }
  }]}}
}}}}
```

## Limits and considerations

*   When using Google Workspace add-ons with Dialogflow, [Chat event objects](/workspace/add-ons/concepts/event-objects#chat-event-object) have the following limitations and considerations:
    *   **App Home Events:** Support for `APP_HOME` events is not yet available.
    *   **Dialogflow Query Input:** The text sent as query input to the Dialogflow agent depends on the event type:
        *   **`MESSAGE`:** The value of the `argumentText` field from the Chat message.
        *   **`APP_COMMAND`:** The string `"APP_COMMAND_PAYLOAD"`.
        *   **`ADDED_TO_SPACE`:** A default [welcome event](https://docs.cloud.google.com/dialogflow/es/docs/intents-default#welcome) is sent.
        *   **`REMOVED_FROM_SPACE`:** The string `"REMOVED_FROM_SPACE_PAYLOAD"`.
        *   **`CARD_CLICKED`:** The string `"BUTTON_CLICKED_PAYLOAD"`.
        *   **`WIDGET_UPDATED`:** The string `"WIDGET_UPDATED_PAYLOAD"` (used for autocomplete).
    *   **Full Event Payload:** The full JSON payload of the Chat interaction event is sent to Dialogflow within the `WebhookRequest.payload` field.
*   Considerations for responding to [commands](/workspace/add-ons/chat/commands) and [receiving data from cards or dialogs](/workspace/add-ons/chat/collect-information):
    *   If the Dialogflow agent needs to process the [Chat interaction event JSON payload](/workspace/add-ons/concepts/event-objects#chat-event-object), it can do so by using a [Dialogflow webhook](https://cloud.google.com/dialogflow/es/docs/fulfillment-webhook) to inspect the custom payload in the query parameter.
    *   To display a [dialog](/workspace/add-ons/chat/dialogs) from the Dialogflow Agent, respond with a single custom JSON payload that contains a [`RenderActions` object with the navigation `pushCard`](/workspace/add-ons/chat/dialogs#request).
    *   To process data entered from cards, you can use a [Dialogflow webhook](https://cloud.google.com/dialogflow/es/docs/fulfillment-webhook) and respond with a single custom JSON payload containing the appropriate [action](/workspace/add-ons/chat/collect-information).
*   Link previews aren't supported.
*   If the Dialogflow agent responds with just one message, then the message is sent to Google Chat synchronously.
*   When using the Dialogflow ES integration with Chat, the Dialogflow agent and the Chat app must be set up in the same Google Cloud project.

## Troubleshoot

To debug your Chat app, start by reviewing the error logs. Since this app uses Dialogflow, you have several logging and troubleshooting resources available:

*   **Google Workspace add-on Logs:** Query logs for detailed information about the add-on's behavior, including its interactions with Chat. See [Query logs for Google Workspace Add-ons](/workspace/add-ons/guides/query-logs).

*   **Google Google Chat app Errors:** For general Chat app error messages and fixes, refer to [Troubleshoot and fix Chat app errors](/workspace/chat/troubleshoot-fix-chat-errors).

*   **Dialogflow ES Conversation History:** [History | Dialogflow ES](https://cloud.google.com/dialogflow/es/docs/history)

*   **Dialogflow General Troubleshooting:** [Troubleshooting | Dialogflow](https://cloud.google.com/dialogflow/docs/support/troubleshooting)

## Clean up

To avoid incurring charges to your account for the resources used in this tutorial, we recommend that you delete the Cloud project.

**Caution:** Deleting a project has the following effects:

*   **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
*   **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1.  In the Google API Console, go to the **Manage resources** page. Click **Menu** menu > **IAM & Admin** > **Manage Resources**.

2.  In the project list, select the project you want to delete and then click **Delete** delete.
3.  In the dialog, type the project ID and then click **Shut down** to delete the project.

## Related topics

*   [Dialogflow CX](https://cloud.google.com/dialogflow/cx/docs) is another way to use Dialogflow with a Chat app.
