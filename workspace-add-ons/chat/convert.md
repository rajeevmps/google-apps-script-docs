# Convert an interactive Google Chat app to a Google Workspace add-on

If you've built and published a Google Chat app that uses
Google Chat API interaction events, like one based on the
[Google Chat app quickstart](https://developers.google.com/workspace/chat/quickstart/gcf-app),
this page shows how to convert it to a Google Workspace add-on that extends
Google Chat.

By converting, your Google Chat app can use the Google Workspace add-ons
framework, opening up new possibilities for integration and features within
Google Chat and across Google Workspace. For example,
you can distribute a single Google Workspace add-on
through Google Workspace Marketplace that extends Chat apps
alongside other Google Workspace host applications, like Gmail,
Calendar, and Docs.

## Limitations

Before starting the conversion, review the
[Limitations of Google Workspace add-ons that extend Google Chat](https://developers.google.com/workspace/add-ons/chat#limitations-known-issues)
to ensure your Google Chat app can be converted without losing
essential functionality.

## Step 1: Copy your existing Google Chat app code

The conversion process requires code changes. To avoid affecting your live
Google Chat app, create and work on a copy of your code.

**Apps Script**

1. Open your existing Google Chat app Google Apps Script project.
2. At the left, click **Overview** info.
3. At the right, click **Make a copy** content_copy.
4. At the left, click **Project Settings** settings.
5. Under **Google Cloud project**, click **Change project**.
6. Enter the same project number associated with your existing Google Chat app
project.
7. Click **Set project**.

**HTTP**

Create a fork or copy of your existing codebase and deploy it as a new service,
separate from your live Google Chat app.

If your app is deployed on Google Cloud and relies on features tied to
the Google Cloud project (for example, the default App Engine identity),
the new code should be deployed on a service associated with the existing
Google Chat app project.

## Step 2: Modify the copied code

Google Workspace add-ons that extend Google Chat use different request and
response structures compared to Google Chat apps built with
Chat API interaction events. You need to
update your code to use the Google Workspace add-on
[`EventObject`](https://developers.google.com/workspace/add-ons/reference/rest/v1/EventObject)
instead of the Google Chat API's
[`Event`](https://developers.google.com/workspace/chat/api/reference/rest/v1/Event)
for requests and responses.
Use the Code conversion guide to modify your code.

## Step 3: Enable the Google Workspace add-on configuration for test users

Use the Google Cloud console to configure the Google Workspace add-on settings for
your Google Chat app:

1. Go to the Google Chat API configuration page in the Google Cloud console.
[Go to Google Chat API configuration page](https://console.cloud.google.com/apis/api/chat.googleapis.com/hangouts-chat)
2. Under **Interactive Features**, turn on **Enable Interactive features**.
3. Under **Convert to Google Workspace add-on**, click
**Convert to add-on**.
4. Enable **Turn on add-on configuration settings**.
5. In the **Visibility** section, add the email addresses of your test users.
6. If necessary, update **Connection Settings** with the deployment endpoint URL or Apps Script deployment ID of your
copied and modified Google Chat app code from Step 2.
7. Click **Save and test**.

## Step 4: Test the converted app

Test the Google Workspace add-on functionality thoroughly using the test user
accounts configured in Step 3. Verify all features and interactions.

## Step 5: Complete the conversion for all users

After you've verified that the converted Google Workspace add-on works correctly,
you can make it available to all users.

1. Go to the Google Chat API configuration page in the Google Cloud console.
[Go to Google Chat API configuration page](https://console.cloud.google.com/apis/api/chat.googleapis.com/hangouts-chat)
2. Under **Interactive Features**, click **Convert to add-on**. A side panel opens.
3. In the side panel, click **Convert to add-on**.
4. Type your Project ID and click **Convert**.

Your Google Chat app is now a Google Workspace add-on that extends
Google Chat.

## Optional: Clean up or free unused Google Cloud resources

Optionally, after converting your Google Chat app to an
Google Workspace add-on, to avoid
incurring charges to your Google Cloud account for the resources used by the
Google Chat app that are no longer in use, consider turning them
off.

## Code conversion guide

This section details the mapping between the Google Chat API interaction
[`Event`](https://developers.google.com/workspace/chat/api/reference/rest/v1/Event)
format and the Google Workspace add-on
[`EventObject`](https://developers.google.com/workspace/add-ons/concepts/event-objects)
format.

### Request mapping

The following table shows how fields in the Google Chat API
[`Event`](https://developers.google.com/workspace/chat/api/reference/rest/v1/Event)
map to the corresponding fields in the Google Workspace add-on
[`EventObject`](https://developers.google.com/workspace/add-ons/concepts/event-objects).

| Google Chat API interaction [`Event`](https://developers.google.com/workspace/chat/api/reference/rest/v1/Event) field | Google Workspace add-on [`EventObject`](https://developers.google.com/workspace/add-ons/concepts/event-objects) field | Notes |
|---|---|---|
| `action.actionMethodName` | N/A | For card interactions, the method name can be passed as a parameter in `commonEventObject.parameters` . See [Open an initial dialog](https://developers.google.com/workspace/add-ons/chat/dialogs#open_an_initial_dialog) . |
| `action.parameters` | `commonEventObject.parameters` |  |
| `appCommandMetadata` | `chat.appCommandPayload.appCommandMetadata` |  |
| `common` | `commonEventObject` |  |
| `configCompleteRedirectUrl` | `chat.appCommandPayload.configCompleteRedirectUri` `chat.addedToSpacePayload.configCompleteRedirectUri` `chat.messagePayload.configCompleteRedirectUri` | Available in different payloads depending on the event type. |
| `dialogEventType` | `chat.appCommandPayload.dialogEventType` `chat.buttonClickedPayload.dialogEventType` | Available in different payloads depending on the event type. |
| `eventTime` | `chat.eventTime` |  |
| `isDialogEvent` | `chat.appCommandPayload.isDialogEvent` `chat.buttonClickedPayload.isDialogEvent` | Available in different payloads depending on the event type. |
| `message` | `chat.messagePayload.message` `chat.buttonClickedPayload.message` `chat.appCommandPayload.message` | Available in different payloads depending on the event type. |
| `space` | `chat.messagePayload.space` `chat.addedToSpacePayload.space` `chat.removedFromSpacePayload.space` `chat.buttonClickedPayload.space` `chat.widgetUpdatedPayload.space` `chat.appCommandPayload.space` |  |
| `thread` | `chat.messagePayload.message.thread` `chat.buttonClickedPayload.message.thread` `chat.appCommandPayload.message.thread` | Available in different payloads depending on the event type. |
| `threadKey` | `chat.messagePayload.message.thread.threadKey` `chat.buttonClickedPayload.message.thread.threadKey` `chat.appCommandPayload.message.threadKey` | Available in different payloads depending on the event type. |
| `token` | N/A | Verification is handled differently, see Request Verification for HTTP Apps . |
| `type` | N/A | The event type can be deduced from the [trigger](https://developers.google.com/workspace/add-ons/chat/build#triggers) . |
| `user` | `chat.user` |  |

### Request mapping by use case

The following table shows the differences in request payloads for common use
cases between Google Chat apps built with Chat API interaction
events and Google Workspace add-ons that extend Google Chat.

| Use Case | Chat API interaction [`Event`](https://developers.google.com/workspace/chat/api/reference/rest/v1/Event) Payload | Google Workspace add-on [`EventObject`](https://developers.google.com/workspace/add-ons/concepts/event-objects) Payload |
|---|---|---|
| App added to space | `{<br>  "type": "ADDED_TO_SPACE",<br>  "space": { ... }<br>}` | `{<br>  "chat": {<br>    "addedToSpacePayload": {<br>      "space": { ... }<br>    }<br>  }<br>}` |
| Remove app from space | `{<br>  "type": "REMOVED_FROM_SPACE",<br>  "space": { ... }<br>}` | `{<br>  "chat": {<br>    "removedFromSpacePayload": {<br>      "space": { ... }<br>    }<br>  }<br>}` |
| User @-mentions an app | `{<br>  "type": "MESSAGE",<br>  "message": { ... },<br>  "space": { ... },<br>  "configCompleteRedirectUrl": "..."<br>}` | `{<br>  "chat": {<br>    "messagePayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "configCompleteRedirectUri": "..."<br>    }<br>  }<br>}` |
| User @-mentions an app to add it to the space | You need to handle one request from Google Chat: — Example: `{<br>  "type": "ADDED_TO_SPACE",<br>  "space": { ... },<br>  "message": { ... }<br>}` | You must handle two requests from Google Chat. First request: Second request: — Example: `{<br>  "chat": {<br>    "messagePayload": {<br>      "message": { ... },<br>      "space": { ... }<br>    }<br>  }<br>}` |
| Slash command | `{<br>  "type": "MESSAGE",<br>  "message": { "slashCommand": { ... } },<br>  "space": { ... }<br>}` | `{<br>  "chat": {<br>    "appCommandPayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "appCommandMetadata": { ... }<br>    }<br>  }<br>}` |
| Slash command to add an app to the space | You need to handle one request from Google Chat: — Example: `{<br>  "type": "ADDED_TO_SPACE",<br>  "space": { ... },<br>  "message": { "slashCommand": { ... } }<br>}` | You must handle two requests from Google Chat. First request: Second request: — Example: `{<br>  "chat": {<br>    "appCommandPayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "appCommandMetadata": { ... }<br>    }<br>  }<br>}` |
| User clicks a button on a card or dialog | For dialog events, `common.formInputs` contains widget values. Google Apps Script example: — Example: `{<br>  "type": "CARD_CLICKED",<br>  "common": {<br>   "formInputs": {<br>    "contactName": {<br>      "": { "stringInputs": { "value": ["Kai 0"] }}<br>    }<br>  }<br>  },<br>  "space": { ... },<br>  "message": { ... },<br>  "isDialogEvent": true,<br>  "dialogEventType": "..."<br>}` | For dialog events, `commonEventObject.formInputs` contains widget values. Google Apps Script example: — Example: `{<br>  "commonEventObject": {<br>     "formInputs": {<br>      "contactName": {<br>        "stringInputs": {<br>          "value": ["Kai 0"]<br>        }<br>      }<br>    }<br>  },<br>  "chat": {<br>    "buttonClickedPayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "isDialogEvent": "true",<br>      "dialogEventType": "..."<br>    }<br>  }<br>}` |
| User submits information in an app home card | `{<br>  "type": "SUBMIT_FORM",<br>  "common": { ... },<br>  "space": { ... },<br>  "message": { ... },<br>  "isDialogEvent": "...",<br>  "dialogEventType": "..."<br>}` | `{<br>  "commonEventObject": { ... },<br>  "chat": {<br>    "buttonClickedPayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "isDialogEvent": "...",<br>      "dialogEventType": "SUBMIT_DIALOG"<br>    }<br>  }<br>}` |
| User invokes an app command using a quick command | `{<br>  "type": "APP_COMMAND",<br>  "space": { ... },<br>  "isDialogEvent": "...",<br>  "dialogEventType": "..."<br>}` | `{<br>  "chat": {<br>    "appCommandPayload": {<br>      "message": { ... },<br>      "space": { ... },<br>      "appCommandMetadata": { ... }<br>    }<br>  }<br>}` |
| Link preview | `{<br>  "type": "MESSAGE",<br>  "message": {<br>    "matchedUrl": "..."<br>  },<br>  "space": { ... }<br>}` | `{<br>  "chat": {<br>    "messagePayload": {<br>      "message": {<br>        "matchedUrl": "..."<br>      },<br>      "space": { ... }<br>    }<br>  }<br>}` |
| User updates a widget in a card message or dialog | `{<br>  "type": "WIDGET_UPDATED",<br>  "space": { ... },<br>  "common": { ... }<br>}` | `{<br>  "commonEventObject": { ... },<br>  "chat": {<br>    "widgetUpdatedPayload": {<br>      "space": { ... }<br>    }<br>  }<br>}` |

### Response mapping by use case

Google Workspace add-ons that extend Google Chat return actions instead of a
`Message` object. The following table maps Google Chat API `Message` response types
to their Google Workspace add-on action equivalents.

| Use Case | Google Chat API [`Message`](https://developers.google.com/workspace/chat/api/reference/rest/v1/spaces.messages#Message) Response | Google Workspace add-on [Chat action](https://developers.google.com/workspace/add-ons/chat/build#actions) response |
|---|---|---|
| Create a message in the invoked space | `actionResponse` is optional. To learn more, see [Respond to a slash command](https://developers.google.com/workspace/chat/commands#slash). — Example: `{<br>  "actionResponse": {<br>    "type": "NEW_MESSAGE"<br>  },<br>  "text": "..."<br>}` | To learn more, see [Send a message](https://developers.google.com/workspace/add-ons/chat/send-messages). — Example: `{<br>  "hostAppDataAction": {<br>    "chatDataAction": {<br>      "createMessageAction": {<br>        "message": {<br>          "text": "..."<br>         }<br>       }<br>    }<br>  }<br>}` |
| Update a message | To learn more, see [Update a message (Chat)](https://developers.google.com/workspace/chat/update-messages). — Example: `{<br> "actionResponse": {<br>  "type": "UPDATE_MESSAGE"<br>  },<br> "text": "..."<br>}` | To learn more, see [Update a message (add-ons)](https://developers.google.com/workspace/add-ons/chat/send-messages#update-message). — Example: `{<br>  "hostAppDataAction": {<br>    "chatDataAction": {<br>      "updateMessageAction": {<br>        "message": {<br>          "text": "..."<br>         }<br>       }<br>    }<br>  }<br>}` |
| Link preview | To learn more, see [Preview a link (Chat)](https://developers.google.com/workspace/chat/preview-links). — Example: `{<br>  "actionResponse": {<br>    "type": "UPDATE_USER_MESSAGE_CARDS"<br>  },<br>  "cardsV2": [{ ... }]<br>}` | To learn more, see [Preview a link(add-ons)](https://developers.google.com/workspace/add-ons/chat/preview-links). — Example: `{<br>  "hostAppDataAction": {<br>    "chatDataAction": {<br>      "updateInlinePreviewAction": {<br>        "cardsV2": [{ ... }]<br>      }<br>    }<br>  }<br>}` |
| Open an initial dialog | To learn more, see [Open a dialog (Chat)](https://developers.google.com/workspace/chat/dialogs#open-dialog). — Example: `{<br>  "actionResponse": {<br>    "type": "DIALOG",<br>    "dialogAction": {<br>      "dialog": {<br>        "body": { /* Card object */ }<br>      }<br>    }<br>  }<br>}` | The card you push can contain widgets with `onClick` actions. For HTTP Google Workspace add-ons, configure these actions to call a function endpoint: To learn more, see [Open a dialog (add-ons)](https://developers.google.com/workspace/add-ons/chat/dialogs#open-dialog). — Example: `{<br>  "onClick": {<br>    "action": {<br>      "function": "https://...",<br>      "parameters": [{<br>        "key": "clickedButton",<br>        "value": "submit"<br>      }]<br>    }<br>  }<br>}` |
| Close a dialog | To learn more, see [Close a dialog (Chat)](https://developers.google.com/workspace/chat/dialogs#close). — Example: `{<br>  "actionResponse": {<br>    "type": "DIALOG",<br>    "dialogAction": {<br>      "actionStatus": {<br>        "userFacingMessage": "..."<br>      }<br>    }<br>  }<br>}` | To learn more, see [Close a dialog (add-ons)](https://developers.google.com/workspace/add-ons/chat/dialogs#close). — Example: `{<br>  "action": {<br>    "navigations": [{<br>      "endNavigation": "CLOSE_DIALOG"<br>    }],<br>    "notification": { "text": "..."}<br>  }<br>}` |
| Connect to an external system (Request config) | To learn more, see [Connect to an external system](https://developers.google.com/workspace/chat/connect-web-services-tools). — Example: `{<br>  "actionResponse": {<br>    "type": "REQUEST_CONFIG",<br>    "url": "..."<br>  }<br>}` | To learn more, see [Connect your Google Workspace add-on to a third-party service](https://developers.google.com/workspace/add-ons/guides/connect-third-party-service#basic-auth-chat). — Example: `{<br>  "basic_authorization_prompt": {<br>    "authorization_url": "...",<br>    "resource": "..."<br>  }<br>}` |
| Autocomplete items on interactive widgets | To learn more, see [Add a multiselect menu](https://developers.google.com/workspace/chat/design-interactive-card-dialog#multiselect-menu). — Example: `{<br>  "actionResponse": {<br>    "type": "UPDATE_WIDGET",<br>    "updatedWidget": {<br>      "suggestions": {<br>        "items": ["..."]<br>      },<br>      "widget": "widget_id"<br>    }<br>  }<br>}` | To learn more, see [Collect and process information from Google Chat users](https://developers.google.com/workspace/add-ons/chat/collect-information). — Example: `{<br>  "action": {<br>    "modifyOperations": [{<br>      "updateWidget": {<br>        "widgetId": "widget_id",<br>        "selectionInputWidgetSuggestions": {<br>          "suggestions": ["..."]<br>        }<br>      }<br>    }]<br>  }<br>}` |

### Handle card interactions on messages created prior to conversion

When you convert an HTTP Google Chat app to a
Google Workspace add-on, card interactions on messages created before the
conversion require special handling. add-ons use a full HTTP URL
for a card's `action.function`, while Chat apps built with
Google Chat API interaction events use a function name. The following table
summarizes these differences.

|  | Google Chat app built with Google Chat API interaction events | Google Workspace add-on that extends Google Chat |
|---|---|---|
| **Configuration** | You configure a single endpoint for all events in the Google Cloud console. When implementing card interactions, a card's `action` only contains the name of the function to execute. The common HTTP endpoint is invoked for card click events. To learn more, see [Open a dialog (Chat)](https://developers.google.com/workspace/chat/dialogs#open-dialog). — Example: `{<br>  "onClick": {<br>    "action": {<br>      "function": "submit"<br>    }<br>  }<br>}` | You can optionally configure per-event endpoints in the Google Cloud console, but this doesn't include card click events. When implementing card interactions, a card's `action` must contain the full URL of the HTTP endpoint to invoke. You can set a unique HTTP endpoint per button, or use a common endpoint and pass the action as a parameter in `action.parameters` . To learn more, see [Open a dialog (add-ons)](https://developers.google.com/workspace/add-ons/chat/dialogs#open_an_initial_dialog). — Example: `{<br>  "onClick": {<br>    "action": {<br>      "function": "https://...",<br>      "parameters": [{<br>        "key": "method",<br>        "value": "submit"<br>      }]<br>    }<br>  }<br>}` |

To ensure card interactions are functional for messages created before the conversion, configure a **Card Interaction URL** on the Google Chat API configuration page.

This URL is only used for interactions on messages created before you converted your app. When a user interacts with one of these messages, the original `action.function` value is passed as a parameter called `__action_method_name__`.

#### Example: Card click

If you configured the **Card Interaction URL** as `https://.../card-interaction-handler`, and a user clicks a card on a historical message with the following action:

```json
{
  "onClick": {
    "action": {
     "function": "submit"
    }
  }
}
```

An event is delivered to your configured **Card Interaction URL** with the following format:

```json
{
  "commonEventObject": {
    "parameters": {
      "__action_method_name__": "submit"
    }
  },
  "chat": {
    "buttonClickedPayload": { ... }
  }
}
```

#### Example: Multi-select menu

If a user interacts with a multi-select menu with an external data source:

```json
{
  "selectionInput": {
    "name": "contacts",
    "type": "MULTI_SELECT",
    "externalDataSource": {
      "function": "getContacts"
    }
  }
}
```

An event is delivered to your configured **Card Interaction URL** with the following format:

```json
{
  "commonEventObject": {
    "parameters": {
      "__action_method_name__": "getContacts",
    }
  },
  "chat": {
    "widgetUpdatedPayload": { ... }
  }
}
```

If you turn on **Use common HTTP endpoint url for all triggers** for your HTTP
triggers, then the common URL is also used for **Button Clicked** events.

### Verify requests for HTTP Google Workspace add-ons that extend Chat

For HTTP-based Google Chat apps, the logic to verify that requests originate
from Google needs to be updated when converting to a Google Workspace add-on.

- Google Chat API interaction event HTTP Google Chat app verification: [Verify requests from Google Chat](https://developers.google.com/workspace/chat/verify-requests-from-chat)
- Google Workspace add-on HTTP verification: [Verifying requests from Google](https://developers.google.com/workspace/add-ons/how-tos/verify-requests)

The key differences in request verification are:

| App Type | Supported Audience | Service Account Email |
|---|---|---|
| Google Chat app built with Google Chat API interaction events | Project number | `chat@system.gserviceaccount.com` |
| Google Workspace add-on extending Google Chat | HTTP endpoint only | Per-project service account email |

The unique service account email for your Google Workspace add-on can be found in the
**Convert to Google Workspace add-ons** section on the Google Chat API configuration page
in the Google Cloud console.

To verify requests in your upgraded Google Workspace add-on:

1. If using Cloud Run functions, grant the
`roles/cloudfunctions.invoker` role to the per-addon service account. See
[Authorize access with IAM](https://cloud.google.com/functions/docs/securing/managing-access-iam).
2. Update your token verification code to use the Google Workspace add-on service
account email to verify the signature of the Bearer token. See
[Validate requests from Google](https://developers.google.com/workspace/add-ons/guides/alternate-runtimes#validate-requests-from-google).
