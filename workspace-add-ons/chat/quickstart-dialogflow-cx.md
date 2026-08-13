# Build a Dialogflow CX add-on that extends Google Chat that understands and responds with natural language

This page explains how to build a Google Chat app that can both understand and respond with natural language using [Dialogflow](https://cloud.google.com/dialogflow). This guide uses [Dialogflow CX](https://cloud.google.com/dialogflow/cx/docs), which has a direct integration with Google Chat. You can also use [Dialogflow ES](https://cloud.google.com/dialogflow/es/docs) to build a Dialogflow ES Google Chat app by following the [Dialogflow ES Google Chat](/workspace/add-ons/chat/quickstart-dialogflow-es) guide.

For example, consider a Chat app that helps people rent cars. A user might write, "I'd like to rent a car". The Chat app might respond with a question like "Where would you like to pick up the vehicle?" which starts a human-like conversation with the user in which the Chat app both understands and responds with human speech while booking the car rental.

This is just one example. Dialogflow Chat apps are useful in all kinds of interactions. If it requires natural human speech, it calls for a Dialogflow Chat app. The [prebuilt agents](https://docs.cloud.google.com/dialogflow/cx/docs/concept/agents-prebuilt) help you get started fast, and showcase what Dialogflow can do, like:

*   Book flights
*   Schedule doctor appointments
*   Order food delivery
*   Answer questions about a retail product catalog, like whether items are available in other colors

## Objectives

*   Set up your environment.
*   Create and deploy a Dialogflow CX agent.
*   Create and deploy a Chat app powered by the Dialogflow CX agent.
*   Test the Chat app.

## Prerequisites

*   A Business or Enterprise [Google Workspace](https://support.google.com/a/answer/6043576) account with access to [Google Chat](https://workspace.google.com/products/chat/).
*   A Google Cloud project with billing enabled. To check that an existing project has billing enabled, see [Verify the billing status of your projects](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled). To create a project and set up billing, see [Create a Google Cloud project](/workspace/guides/create-project).

## Architecture

The following diagram shows the architecture of a Chat app built with Dialogflow:

In the preceding diagram, a user interacting with a Dialogflow Chat app has the following flow of information:

1.  A user sends a message in Chat to a Chat app, either in a direct message or in a Chat space.
2.  A Dialogflow virtual agent, which resides in Google Cloud, receives and processes the message to produce a response.
3.  Optionally, using a [Dialogflow webhook](https://cloud.google.com/dialogflow/cx/docs/concept/webhook), the Dialogflow agent can interact with external third-party services, such as a project management system or a ticketing tool.
4.  The Dialogflow agent sends a response back to the Chat app service in Chat.
5.  The response is delivered to the Chat space.

## Set up the environment

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

1.  In the Google Cloud console, enable the Google Chat API and the Dialogflow API.

2.  Confirm that you're enabling the APIs in the correct Cloud project, then click **Next**.

3.  Confirm that you're enabling the correct APIs, then click **Enable**.

## Create a Dialogflow CX agent

A [Dialogflow CX agent](https://cloud.google.com/dialogflow/cx/docs/concept/agent) is a virtual agent that handles concurrent conversations with your end-users. It's a natural language comprehension module that understands the nuances of human language. Dialogflow translates end-user text during a conversation to structured data that your apps and services can understand. You design and build a Dialogflow agent to handle the types of conversations required for your system.

A Dialogflow agent is like a human call center agent. You train them both to handle expected conversation scenarios, and your training doesn't need to be overly explicit.

Here's how to create the Dialogflow CX agent:

1.  In the Dialogflow CX console, open the Dialogflow CX Console. Click **Menu** menu > **Dialogflow CX**.

2.  Choose a Google Cloud project. To find your project, you might need to click **All** and then search for it.

3.  Now you have the option to choose a prebuilt agent or create your own. If you prefer to explore agent customization in detail later, choose one of the [prebuilt agents](https://docs.cloud.google.com/dialogflow/cx/docs/concept/agents-prebuilt), which are also helpful to learn about what agents can do.

    To choose a prebuilt agent, follow these steps:

    1.  Click **Use prebuilt agents**.
    2.  Select a prebuilt agent. For this guide, select **Travel: car rental**.

        Agents are rated as beginner, intermediate, or advanced based on how many features the agent uses and upon the sophistication of its conversation logic. Choosing an intermediate or advanced agent might require agent-specific customizations and settings, including enabling features and APIs in Google Cloud console.

    3.  Click **Import as agent**.

    To create your own agent, follow these steps:

    1.  Click **Create agent**.
    2.  Select **Auto-generate** to create a [data store agent](https://cloud.google.com/dialogflow/cx/docs/concept/data-store-agent) or select **Build your own** to create other kinds of agents.

    For a detailed walkthrough of the agent building process, see [Create a Dialogflow CX agent](https://cloud.google.com/dialogflow/cx/docs/quick/build-agent).

4.  Configure basic agent settings:

    1.  In **Display name**, enter a display name.
    2.  Select your preferred [location](https://cloud.google.com/dialogflow/cx/docs/concept/region). If you want to change advanced [location settings](https://cloud.google.com/dialogflow/cx/docs/concept/region#location-settings), click **Edit**.
    3.  Select your preferred time zone.
    4.  Select the default language for your agent. You can't change the default language for an agent after creation.
5.  Click **Create**. Dialogflow CX begins creating the agent, and then displays the agent's default start flow.

6.  Optionally, customize the agent. For a detailed walkthrough the agent customization process, see [Create a Dialogflow CX agent](https://cloud.google.com/dialogflow/cx/docs/quick/build-agent).

7.  As a best practice, test the agent:

    1.  Click **Test agent**.
    2.  Select **Test agent in environment**.
    3.  In Environment, select **Draft**.
    4.  In Flow, select **Default Start Flow**.
    5.  In Page, select **Start Page**.
    6.  In the **Talk to agent** compose bar, type `Hello` and press **Enter**. The agent responds by introducing itself.
    7.  Complete the test by having the sample test conversation.
8.  The Dialogflow CX agent is created. Return to the Dialogflow CX console. Click **Menu** menu > **Dialogflow CX**.

9.  Under **Agents**, click more_vert > **Copy name**. Save this name, as you use it when configuring the Chat app.

## Create a Chat app and connect it with the Dialogflow agent

After creating a Dialogflow CX agent, follow these steps to turn it into a Chat app:

1.  In the Google Cloud console, go to Google Chat API. Search for "Google Chat API" and click **Google Chat API**, then click **Manage**.

2.  Click **Configuration** and set up the Chat app:

    1.  In **App name**, enter `Dialogflow App`.
    2.  In **Avatar URL**, enter `https://developers.google.com/workspace/chat/images/quickstart-app-avatar.png`.
    3.  In **Description**, enter `Responds to real human conversation`.
    4.  Under **Functionality**, select **Join spaces and group conversations**.
    5.  Under **Connection settings**, select **Dialogflow**.
    6.  Under **Dialogflow settings**, select **Dialogflow CX**.
    7.  In **Agent or Environment resource name**, paste the Dialogflow CX agent name you copied at the end of Create a Dialogflow CX agent.
    8.  **Make this Chat app available to specific people and groups** in your domain and enter your email address.
    9.  Under **Logs**, select **Log errors to Logging**.
3.  Click **Save**.

The Chat app is ready to receive and respond to messages on Chat.

## Test the Chat app

Test the Dialogflow CX Chat app by messaging it in Google Chat.

1.  Open Google Chat using the Google Workspace account that you provided when you added yourself as a trusted tester.

2.  Click add **New chat**.
3.  In the **Add 1 or more people** field, type the name of your Chat app.
4.  Select your Chat app from the results. A direct message opens.

    **Note:** If you don't see your Chat app in the list of results, ensure that you've included your Google Workspace account in the **Visibility** settings of the [**Chat API Configuration**](/workspace/chat/configure-chat-api) page in the Google Cloud console.

5.  In the new direct message with the app, type `Hello` and press `enter`.

    The Dialogflow Chat app responds by introducing itself.

6.  Complete the test by having the sample test conversation.

### Sample test conversation

To test the Dialogflow CX Chat app in either the Dialogflow CX console or in Google Chat, have the following conversation. The explanation helps you understand how the Dialogflow CX agent interprets the user's natural language and produces its own natural language response at each step in the conversation. This sample conversation is based on the [prebuilt agent](https://docs.cloud.google.com/dialogflow/cx/docs/concept/agents-prebuilt) called **Travel: car rental**.

| Dialog | Explanation |
|--------|-------------|
| **End-user:** Hello  **Agent:** Hi! I'm the virtual car rental agent. I can help you start a new car rental reservation. How can I assist you today? | 1. The **Default Welcome Intent** route in the **Default Start Flow** is called. 2. The fulfillment for this state handler ("Hi! I'm...") is added to the response queue. 3. The agent sends the response queue to the end-user. |
| **End-user:** I'd like to rent a car.  **Agent:** Where would you like to pick up the vehicle? | 1. The **car_rental.reservation_create** intent route in the **Start Page** is matched. 2. The session transitions to the **Pickup Location** page. 3. The **Pickup Location** page form isn't complete, so the agent uses the **pickup_location** parameter to prompt the user ("Where would you like to pick up..."), which is added to the response queue. 4. The agent sends the response queue to the end-user. |
| **End-user:** Las Vegas  **Agent:** Ok, your pickup will be in Las Vegas.  **Agent:** Is your drop off location different from your pickup location? | 1. The end-user input fills the **pickup_location** parameter requested by the agent in the previous conversation turn. 2. The **car_rental.return_different_location** intent route in the **Default Start Flow** is matched. 3. The form completion route in the **Pickup Location** page is evaluated and called. It has a fulfillment ("Ok, your pickup..."), which is added to the response queue with its parameter references resolved to actual values supplied by the end-user. 4. The session transitions to the **Confirm Location** page. 5. The **Confirm Location** page has an entry fulfillment ("Is your drop off location different..."), which is added to the response queue. 6. The agent sends the response queue to the end-user. |
| **End-user:** Yes. I'll drop the car off in Los Angeles.  **Agent:** Ok, your drop off will be in Los Angeles.  **Agent:** What date and time would you like to pick up the vehicle? | 1. The **car_rental.return_different_location** intent route in the **Default Start Flow** is matched. 2. The session transitions to the **Drop Off Location** page. 3. The end-user input fills the **drop_off_location** parameter requested by the agent in the previous conversation turn. 4. The form completion route in the **Drop Off Location** page is evaluated and called. It has a fulfillment ("Ok, your drop off..."), which is added to the response queue. 5. The session transitions to the **Rental Duration** page. 6. The **Rental Duration** page has incomplete form values, so it prompts the user for the **pickup_date_time** parameter ("What date and time would you like to pick up..."), which is added to the response queue. 7. The agent sends the response queue to the end-user. |
| **End-user:** I'd like to pick up the car on March 5 at noon.  **Agent:** What date and time would you like to drop off the vehicle? | 1. The end-user input fills the **pickup_date_time** parameter requested by the agent in the previous conversation turn. 2. The **Rental Duration** page has another missing form value, so it prompts the user for the **drop_off_date_time** parameter ("What date and time would you like to drop off..."), which is added to the response queue. 3. The agent sends the response queue to the end-user. |
| **End-user:** March 15 at noon.  **Agent:** So to confirm:  You will be picking the vehicle up in Las Vegas 2024-03-05 12:00:00 and dropping it off in Los Angeles 2024-03-15 12:00:00  Does that sound right? | 1. The end-user input fills the **drop_off_date_time** parameter requested by the agent in the previous conversation turn. 2. The session transitions to the **Confirm Rental Duration** page. 3. The **Confirm Rental Duration** page has an entry fulfillment ("So to confirm..."), which is added to the response queue. 4. The agent sends the response queue to the end-user. |
| **End-user:** Yes, thank you.  **Agent:** Great! Now let's choose a vehicle.  **Agent:** Would you like an economy or luxury vehicle? | 1. The **small_talk.confirmation.yes** intent route in the **Confirm Rental Duration** page is matched. 2. The agent confirms the user's choice with a message ("Great! Now let's choose..."), which is added to the response queue. 3. The session transitions to the **Vehicle Disambiguation** page. 4. The **Vehicle Disambiguation** page form is not complete, so the agent uses the **vehicle_type** parameter to prompt the user ("Would you like an economy or luxury..."), which is added to the response queue. 5. The agent sends the response queue to the end-user. |
| **End-user:** Economy, please.  **Agent:** Would you like the Cymbal Car or the Cymbal Truck? | 1. The **$session.params.vehicle_type="economy_vehicle"** intent route is matched. 2. The session transitions to the **Economy Options** page. 3. The **Economy Options** page has an entry fulfillment ("Would you like the..."), which is added to the response queue. 4. The agent sends the response queue to the end-user. |
| **End-user:** Cymbal Truck.  **Agent:** The Cymbal Truck is $50.33 per day. It fits 4 people and comes with an AM/FM radio. Would you like to proceed to payment?  **End-user:** Yes, please. | 1. The **$session.params.vehicle_type="Cymbal Truck"** intent route is matched and the **vehicle_model** parameter is filled. 2. The session transitions to the **Confirm Cymbal Truck** page. 3. The **Confirm Cymbal Truck** page has an entry fulfillment ("The Cymbal Truck is $50.33 per day..."), which is added to the response queue. 4. The agent sends the response queue to the end-user. 5. The user's response matches the **small_talk.confirmation.yes** route. |
| **Agent:** What card type will you be using?  **End-user:** Altostrat  **Agent:** Please enter the card number.  **End-user:** 1234 1234 1234 1234  **Agent:** What is the name on the card?  **End-user:** Charlie  **Agent:** What is the billing street address?  **End-user:** 1800 Amphibious Blvd. Mountain View, CA  **Agent:** What is the billing ZIP code?  **End-user:** 94045  **Agent:** You will be picking the Cymbal Car up in Las Vegas, 2024-03-05 12:00:00 and dropping it off, 2024-03-15 12:00:00. The total for this trip will be $175.38.  **Agent:** Thank you for renting with us and have a wonderful day! | 1. The session transitions to the **Payment** page. 2. The **Payment** form is not complete so the agent prompts the user for the **card_type**, **card_number**, **billing_name**, **billing_street_address**, and **billing_zip_code** parameters ("What card type will..."), which are sequentially added to the response queue and sent as the user responds. The user's responses set each parameter value. 3. The session transitions to the **Rental Confirmation** page. 4. The **Rental Confirmation** page has an entry fulfillment ("Ok, your pickup will be..."), which is added to the response queue. 5. The agent sends the response queue to the end-user. 6. The session transitions to the **End Session** page. |

## Send card messages from Dialogflow

Dialogflow can respond with [text](/workspace/add-ons/chat/send-messages#reply-message) or [card](/workspace/add-ons/chat/collect-information) messages. To respond with a card message, specify it as a [custom payload](https://cloud.google.com/dialogflow/cx/docs/concept/fulfillment#payload) in [fulfillment](https://cloud.google.com/dialogflow/cx/docs/concept/fulfillment).

The following JSON shows how to send a card message as a custom payload in fulfillment:

```json
{
  "hostAppDataAction": {
    "chatDataAction": {
      "createMessageAction": {
        "message": {
          "cardsV2": [
            {
              "cardId": "createCardMessage",
              "card": {
                "header": {
                  "title": "A card message!",
                  "subtitle": "Sent from Dialogflow",
                  "imageUrl": "https://developers.google.com/chat/images/chat-product-icon.png",
                  "imageType": "CIRCLE"
                },
                "sections": [
                  {
                    "widgets": [
                      {
                        "buttonList": {
                          "buttons": [
                            {
                              "text": "Read the docs!",
                              "onClick": {
                                "openLink": {
                                  "url": "https://developers.google.com/workspace/chat"
                                }
                              }
                            }
                          ]
                        }
                      }
                    ]
                  }
                ]
              }
            }
          ]
        }
      }
    }
  }
}
```

## Limits and considerations

*   When using Google Workspace add-ons with Dialogflow, [Chat event objects](/workspace/add-ons/concepts/event-objects#chat-event-object) have the following limitations and considerations:
    *   **App Home Events:** Support for `APP_HOME` events is not yet available.
    *   **Dialogflow Query Input:** The text sent as query input to the Dialogflow agent depends on the event type:
        *   **`MESSAGE`:** The value of the `argumentText` field from the Chat message.
        *   **`APP_COMMAND`:** The string `"APP_COMMAND_PAYLOAD"`.
        *   **`ADDED_TO_SPACE`:** The string `"ADDED_TO_SPACE_PAYLOAD"`.
        *   **`REMOVED_FROM_SPACE`:** The string `"REMOVED_FROM_SPACE_PAYLOAD"`.
        *   **`CARD_CLICKED`:** The string `"BUTTON_CLICKED_PAYLOAD"`.
        *   **`WIDGET_UPDATED`:** The string `"WIDGET_UPDATED_PAYLOAD"` (used for autocomplete).
    *   **Full Event Payload:** The full JSON payload of the Chat interaction event is sent to Dialogflow within the `WebhookRequest.payload` field. You can access this in your Dialogflow webhook. For more information, see the [Dialogflow CX webhook request documentation](https://cloud.google.com/dialogflow/cx/docs/concept/webhook#webhook-request).
*   Considerations for responding to [commands](/workspace/add-ons/chat/commands) and [receiving data from cards or dialogs](/workspace/add-ons/chat/collect-information):
    *   If the Dialogflow agent needs to process the [Chat interaction event JSON payload](/workspace/add-ons/concepts/event-objects#chat-event-object), it can do so by using a [Dialogflow webhook](https://cloud.google.com/dialogflow/cx/docs/concept/webhook) to inspect the custom payload in the query parameter.
    *   To display a [dialog](/workspace/add-ons/chat/dialogs) from the Dialogflow Agent, respond with a single custom JSON payload that contains a [`RenderActions` object with the navigation `pushCard`](/workspace/add-ons/chat/dialogs#request).
    *   To process data entered from cards, you can use a [Dialogflow webhook](https://cloud.google.com/dialogflow/cx/docs/concept/webhook) and respond with a single custom JSON payload containing the appropriate [action](/workspace/add-ons/chat/collect-information).
*   [Link previews](/workspace/chat/how-tos/preview-links) aren't supported.
*   If the Dialogflow agent responds with just one message, then the message is sent to Google Chat synchronously. If the Dialogflow agent responds with multiple messages, then all messages are sent to Chat asynchronously by calling the [`create`](/workspace/chat/api/reference/rest/v1/spaces.messages/create) method on the `spaces.messages` resource in Chat API once for each message.
*   When using the Dialogflow CX integration with Chat, the Dialogflow agent and the Chat app must be set up in the same Google Cloud project. If you need to set up the Dialogflow and Chat in different Cloud projects, then you can set up an intermediate server to facilitate the connection. To learn how, see this [Chat integration for Dialogflow CX example](https://github.com/GoogleCloudPlatform/dialogflow-integrations/tree/master/cx/google-chat) on GitHub.

## Troubleshoot

To debug your Chat app, start by reviewing the error logs. Since this app uses Dialogflow, you have several logging and troubleshooting resources available:

*   **Google Workspace add-on Logs:** Query logs for detailed information about the add-on's behavior, including its interactions with Chat. See [Query logs for Google Workspace Add-ons](/workspace/add-ons/guides/query-logs).

*   **Google Google Chat app Errors:** For general Chat app error messages and fixes, refer to [Troubleshoot and fix Chat app errors](/workspace/chat/troubleshoot-fix-chat-errors).

*   **Dialogflow CX Cloud Logging:** Ensure Cloud Logging is enabled in your Dialogflow agent settings to capture detailed execution logs, including errors from the agent and webhook interactions. Learn how to enable and configure this in the [Dialogflow CX Agent Settings documentation](https://cloud.google.com/dialogflow/cx/docs/concept/agent-settings#logging-settings). These logs can be viewed in the Google Cloud Console's Logs Explorer.

*   **Dialogflow CX Conversation History:** Review past interactions to understand conversation flow and identify where issues occur. See [Conversation History](https://cloud.google.com/dialogflow/cx/docs/concept/conversation-history).

*   **Dialogflow General Troubleshooting:** For broader Dialogflow issues, consult the [Dialogflow CX Troubleshooting guide](https://cloud.google.com/dialogflow/docs/support/troubleshooting).

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, we recommend that you delete the Cloud project.

**Caution:** Deleting a project has the following effects:

*   **Everything in the project is deleted.** If you used an existing project for this tutorial, when you delete it, you also delete any other work you've done in the project.
*   **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as a URL on appspot.com, delete the selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple tutorials and quickstarts, reusing projects can help you avoid exceeding project quota limits.

1.  In the Google Cloud console, go to the **Manage resources** page. Click **Menu** menu > **IAM & Admin** > **Manage Resources**.

2.  In the project list, select the project you want to delete and then click **Delete** delete.
3.  In the dialog, type the project ID and then click **Shut down** to delete the project.

## Related topics

*   [Dialogflow CX](https://cloud.google.com/dialogflow/cx/docs) takes a [state machine](https://en.wikipedia.org/wiki/Finite-state_machine) approach to Dialogflow agent design, which gives you clear and explicit control over a conversation, a better end-user experience, and a better development workflow. When building a Dialogflow Chat app, we recommend using Dialogflow CX.
    *   To learn more about building and configuring agents, see [Dialogflow CX Agents](https://cloud.google.com/dialogflow/cx/docs/concept/agent).
    *   For a detailed walkthrough instructing you how to build and configure agents, see [Create a Dialogflow CX agent](https://cloud.google.com/dialogflow/cx/docs/quick/build-agent).
*   [Dialogflow ES](https://cloud.google.com/dialogflow/es/docs) is another way to use Dialogflow with a Chat app.
