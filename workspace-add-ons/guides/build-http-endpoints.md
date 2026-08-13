# Build a Google Workspace add-on using HTTP endpoints

As an alternative to Google Apps Script, you can build an add-on in any coding language you want, as long as you can return properly formatted JSON for the interface to render as cards.

## Set up the runtime

Pick your hosting infrastructure and set up your HTTP endpoints. If you want to build and host your add-on on Google Cloud, we recommend that you use Cloud Run.

## Create a manifest

When you build your add-on in a different language, you must configure the add-on's manifest in Google Cloud.

Follow these steps to configure your add-on's manifest:

1. If you haven't already, create a Google Cloud project for your add-on.

2. In the Google Cloud console, enable the Google Workspace Marketplace SDK.

3. In the Google Cloud console, go to **Menu** menu > **APIs & Services** > **Enabled APIs & services** > **Google Workspace Marketplace SDK** > **HTTP Deployments**.

4. At the top, click **Create new deployment**.

5. Give your manifest a name and click **Next**.

6. Add your add-on's information in JSON format and click **Submit**.

For more information, see Manifests for Google Workspace add-ons.

### Set explicit scopes in your manifest

To build your HTTP add-on, you must explicitly set the relevant OAuth scopes in your add-on's manifest. You must add all the scopes required by your project to the `oauthScopes` array field of the `projects.deployments` resource.

We recommend that you always use the least-permissive set of scopes possible. To protect user information, add-ons should never ask for more scope permissions than they absolutely need. For more information, see Scopes.

## Manage granular permissions

HTTP add-on that use user authentication must support granular permissions to allow users to grant a subset of requested scopes. This gives users more granular control over the data that they share and provides better transparency and security.

The granular OAuth consent screen lets users specify which individual OAuth scopes to authorize. The consent screen includes a summary of your project, its policies, and the requested authorization scopes from the App Configuration page of the Google Workspace Marketplace SDK.

During add-on execution, the add-on receives a list of user authorized scopes.

The following code sample shows a list of authorized scopes:

```json
{
      "authorizationEventObject": {
          "userOAuthToken": "USER_OAUTH_TOKEN"
            "authorizedScopes": [
              "https://www.googleapis.com/auth/gmail.addons.execute",
              "https://www.googleapis.com/auth/script.locale"
            ]
      }
    }
```

Developers must check the list of authorized scopes to detect if there's any scopes missing for the current execution.

The following code sample shows how to detect missing scopes:

```javascript
// A NodeJS HTTP handler that reads the latest email and creates a calendar event.
    export async function createCalendarEventFromEmail(req, res) {
     // Ensure the required scopes are authorized.
     const authorizedScopes = req.body.authorizationEventObject.authorizedScopes || [];
     if (!authorizedScopes.includes('https://www.googleapis.com/auth/gmail.readonly') ||
       !authorizedScopes.includes('https://www.googleapis.com/auth/calendar.events.owned')) {
       res.send({
         'requesting_google_scopes': { 'scopes': ['https://www.googleapis.com/auth/gmail.readonly', 'https://www.googleapis.com/auth/calendar.events.owned'] }
       });
       return;
     }
    
     // Use the token for API calls and return a card response.
     // ...
    }
```

If the add-on detects any missing scopes, it should return the list of scopes as a response. The add-on shows a granular permissions prompt to the user with the missing scopes. The user can then choose which scopes they want to allow.

The following code sample shows how to request specific missing scopes:

```json
{
      "requesting_google_scopes": {
          "scopes": [
            "https://www.googleapis.com/auth/books",
            "https://www.googleapis.com/auth/youtube"
          ]
      }
    }
```

While developers can prompt for individual scopes, it's best practice to prompt for all scopes required for the current add-on execution. This way the add-on doesn't request unnecessary scopes and the user isn't prompted too often.

The following code sample shows how to request all the scopes from the manifest:

```json
{
      "requesting_google_scopes": {
         "all_scopes": true
      }
    }
```

The granular permissions prompt is then shown to the user with all the missing OAuth scopes. After the user addresses the prompt, the add-on is executed again with the granted scopes. Following the OAuth consent flow, the add-on automatically repeats the last action that originally prompted the request for more permissions.

### Constraints on granular permissions

The following constraints are enforced when working with the granular permissions flow:

- The OAuth scopes must be listed in the project manifest. Otherwise, when you try to invoke a scope it generates an error.

- You can't assume users granted all requested scopes for your app. If users don't grant access to all required scopes for the current execution, you must request permissions for the missing scopes.

- If there's only one scope required, the consent screen doesn't display the checkbox.

## Build JSON card

Design your add-on interface with the card framework. Use JSON instead of the Google Apps Script Card Service to build cards. For detailed information about JSON objects for cards, see the reference documentation.

To view examples of JSON cards, see JSON card interfaces.

## Create JSON response objects

Each unique entry point listed in your add-on's manifest needs a unique JSON response object.

The following are common Google Workspace add-on entry points with sample JSON response schemas.

### Common entry points for Gmail, Google Calendar, Google Drive, Editors, and Google Meet

| Entry point | Description | JSON response |
|---|---|---|
| `homepageTrigger.runFunction` | The user opens the add-on's homepage. | renderActions |
| `OnClick.action.function` | The user clicks on actions within the add-on. | onClick |
| `TextInput.autoCompleteAction.function` | The user enters text and the add-on provides automatic suggestions. | getAutocompletionResponse |

### Entry points for Gmail

| Entry point | Description | JSON response |
|---|---|---|
| `contextualTrigger.onTriggerFunction` | The user opens an email. | renderActions |
| `composeTrigger` | The user opens the compose view. | renderActions |

### Entry points for Calendar

| Entry point | Description | JSON response |
|---|---|---|
| `eventOpenTrigger` | The user opens an event. | renderActions |
| `eventUpdateTrigger` | The user updates an event. | calendarClientActionMarkup |
| `eventAttachmentTrigger` | The user clicks on the add-on attachment provider in the Calendar attachment drop-down menu. | calendarClientActionMarkup |

### Entry points for Drive

| Entry point | Description | JSON response |
|---|---|---|
| `onItemsSelectedTrigger` | The user selects a file. | renderActions |

### Entry points for Editors

| Entry point | Description | JSON response |
|---|---|---|
| `createActionTriggers` | The user has chosen to create a third-party resource from the @ Menu in a Google Workspace application. | link |
| `linkPreviewTriggers` | The user has interacted with a URL that matches a pattern specified in `LinkPreviewTriggers`. | linkPreview |
| `onFileScopeGrantedTrigger` | The user has completed granting file access in response to a `requestFileScopeForActiveDocument` action. | renderActions |

## Validate JSON requests

A request sent to your endpoint is a POST request with a JSON event object in the request body.

Properly guard your HTTPS endpoint to ensure requests to your add-on are only fulfilled for ones coming from Google. This is especially important if your HTTPS endpoint returns user data from your service.

Use `authorizationEventObject` ID tokens to access Google services and validate users and service accounts.

### ID tokens

| Token field | Type | Description |
|---|---|---|
| `authorizationEventObject.userOAuthToken` | String | The end user OAuth access token, authorized with the requested scopes. See the example to get a user's Gmail data. |
| `authorizationEventObject.userIdToken` | String | An end user ID token. The user's email address is encoded in the end user ID token, formatted as a JSON web token. To receive this event object in the request, you must specify the scope `https://www.googleapis.com/auth/userinfo.email` in your add-on's manifest. See the example to get a user's email address. |
| `authorizationEventObject.systemIdToken` | String | An ID token for the Google Workspace add-on's service account for a specific deployment. It can be used to verify that the request comes from Google. See the example to validate requests from Google. |

### Example: Get the user's Gmail data

To access users' Google data, request the relevant scope in your add-on's manifest. Then use `authorizationEventObject.userOAuthToken` to pass the API calls.

In the following example, the add-on uses a contextual trigger to reference the email recipient while the user is reading an email. To learn more about contextual triggers in Gmail, see Extending the message UI.

#### Add triggers and scopes

First, update your manifest to include Gmail's contextual trigger and an OAuth scope to allow access to the current message.

```json
{
  "oauthScopes": [
    "https://www.googleapis.com/auth/gmail.addons.execute",
    "https://www.googleapis.com/auth/gmail.addons.current.message.metadata"
  ],
  "addOns": {
    "common": {...},
    "gmail": {
      "contextualTriggers": [
        {
          "unconditional": {},
          "onTriggerFunction": "https://us-central1-test-http-runtime.cloudfunctions.net/GmailExample/simpleMessageInfo"
        }
      ],
    }
  }
}
```

Specify the HTTPS endpoint for the add-on to apply when the user views an email message.

If you don't want to use URL paths to distinguish between different entry points, you can use query parameters, for example, `https://us-central1-test-http-runtime.cloudfunctions.net/HttpAddOn/exampleWidgets?trigger=onEmailOpen`.

When triggered, in this case by the user opening an email, the following event object is passed to the add-on as a JSON blob in the HTTP body.

```json
{
  "commonEventObject": {
     "hostApp": "GMAIL",
     "platform": "WEB"
  },
  "authorizationEventObject": {
    "userOAuthToken": "ya29...",
    "systemIdToken": "eyJhbGc...",
    "userIdToken": "jaaa45...",
  },
  "gmail": {
     "messageId": "msg-f:1234567",
     "threadId": "thread-f:2345678",
     "accessToken": "xedf241...",
  },
}
```

#### Extract the information

The event object doesn't have the user's email address or the contents of the email. To get this information, use the Gmail API to get the contents of the email with the `messageId`.

To authenticate with the Gmail API, send the OAuth2 token in the `Authorization` header as a bearer token. Send the OAuth2 access token from `authorizationEventObject.userOauthToken`.

When using one of the per-message scopes, also include the message token from `gmail.accessToken` in an additional `X-Goog-Gmail-Access-Token` header.

The following code sample shows how to get the contents of an email using the Gmail API:

##### Java

```java
import com.fasterxml.jackson.databind.JsonNode;
import com.google.api.client.auth.oauth2.BearerToken;
import com.google.api.client.auth.oauth2.Credential;
import com.google.api.client.googleapis.javanet.GoogleNetHttpTransport;
import com.google.api.client.json.jackson2.JacksonFactory;
import com.google.api.client.http.HttpHeaders;
import com.google.api.services.gmail.Gmail;
import com.google.api.services.gmail.model.Message;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GmailMessageDemoController {

   @PostMapping("/message")
   public JsonNode onViewMessage(@RequestBody JsonNode event)
           throws Exception {
       String messageId = event.at("/gmail/messageId").asText();
       String messageToken = event.at("//gmail/accessToken").asText();
       String accessToken = event.at("//authorizationEventObject/userOauthToken")
               .asText();
       Credential credential = new Credential(BearerToken.authorizationHeaderAccessMethod());
       credential.setAccessToken(accessToken);

       Gmail gmailClient = new Gmail.Builder(
               GoogleNetHttpTransport.newTrustedTransport(),
               JacksonFactory.getDefaultInstance(),
               credential)
               .setApplicationName("GSAO Demo")
               .build();
       HttpHeaders headers = new HttpHeaders()
               .set("X-Goog-Gmail-Access-Token", messageToken);
       Message message = gmailClient.users().messages().get("me", messageId)
               .setFormat("metadata")
               .setRequestHeaders(headers)
               .execute();
     // Build and return response...
   }
}
```

##### Node.JS

```javascript
import express from "express";
import { Request, Response } from "express";
import { google } from "googleapis";
import asyncHandler from "express-async-handler";
import { OAuth2Client } from "google-auth-library";

const gmail = google.gmail({version: "v1"});

const app = express();

app.post("/", asyncHandler(async (req, res) => {
   const currentMessageId = req.body.gmail.messageId;
   const event = req.body;
   const accessToken = event.authorizationEventObject.userOAuthToken;
   const messageToken = event.gmail.accessToken;
   const auth = new OAuth2Client();
   auth.setCredentials({access_token: accessToken});

   const gmailResponse = await gmail.users.messages.get({
       id: currentMessageId,
       userId: "me",
       format: "metadata",
       auth,
       headers: { "X-Goog-Gmail-Access-Token": messageToken }
   });

   const message = gmailResponse.data;
   const response = ...; // Build and return response
   res.json(response);
}));
```

### Example: Get the user's email address

To access a user's email address:

1. Add the relevant scope to your add-on's deployment resource.
2. Get the client ID that was created to validate the JSON web token.
3. Use `authorizationEventObject.userIdToken` to extract the user ID and email.

#### Add the scope

To get access to a user's email address, add the OAuth scope `https://www.googleapis.com/auth/userinfo.email` to your add-on's manifest:

```json
{
  "oauthScopes": [
    "https://www.googleapis.com/auth/userinfo.email",
  ],
  "addOns": {
    "common": {...},
  }
}
```

#### Get the client ID

To verify the user ID token and extract the user ID and email, you must use the client ID that was created to validate the JSON web token.

To get the client ID, visit the Google Workspace Marketplace SDK in the Google Cloud console:

1. Open the Google Cloud console and select your add-on's Google Cloud project.

2. Go to the Google Workspace Marketplace SDK's **HTTP Deployments** tab.

3. In the **Authorization Resource** section, go to the **Oauth Client Id** field and copy the ID.

Alternatively, if you've installed Google Cloud CLI, get the client ID by running the following `get-authorization` command:

```
gcloud workspace-add-ons get-authorization
```

#### Extract the user ID and email

The following code sample gets the user ID and email address. `CLIENT_ID_FOR_ADDON` is a placeholder for the client ID:

##### Java

```java
import com.google.api.client.googleapis.auth.oauth2.GoogleIdToken;
import com.google.api.client.googleapis.auth.oauth2.GoogleIdTokenVerifier;
import com.google.api.client.googleapis.auth.oauth2.GoogleTokenResponse;
import com.google.api.client.http.javanet.NetHttpTransport;
import com.google.api.client.json.jackson2.JacksonFactory;

final static String CLIENT_ID = "CLIENT_ID_FOR_ADDON";

//...

GoogleIdToken.Payload decodeIdToken(JsonNode event) throws Exception {
    String idToken = event.at("/authorizationEventObject/userIdToken").asText();
    GoogleIdTokenVerifier.Builder builder = new GoogleIdTokenVerifier.Builder(
                GoogleNetHttpTransport.newTrustedTransport(),
                JacksonFactory.getDefaultInstance());
    builder.setAudience(Collections.singletonList(CLIENT_ID);
    GoogleIdTokenVerifier verifier = builder.build();
    GoogleIdToken decodedToken = verifier.verify(idToken);
    GoogleIdToken.Payload payload = decodedToken.getPayload();
    return payload;
    // E.g. payload.getEmail() for email,  payload.getSubject() for user ID
}
```

##### Node.JS

```javascript
const { OAuth2Client } = require('google-auth-library');
const CLIENT_ID = 'CLIENT_ID_FOR_ADDON';

// ...

async decodeIdToken(event) {
   const oAuth2Client = new OAuth2Client();
   const decodedToken = await oAuth2Client.verifyIdToken({
        idToken: event.authorizationEventObject.userIdToken,
        audience: CLIENT_ID
    });
    const payload = decodedToken.getPayload();
    // E.g. payload.email for email,  payload.sub for user ID
    return payload;
}
```

### Example: Validate requests from Google

You need the service account email to verify the `authorizationEventObject.systemIdToken`.

To get the service account email, visit the Google Workspace Marketplace SDK in the Google Cloud console:

1. Open the Google Cloud console and select your add-on's Google Cloud project.

2. Go to the Google Workspace Marketplace SDK's **HTTP Deployments** tab.

3. In the **Authorization Resource** section, go to the **Service Account Email** field and copy the email address.

The following code sample authenticates requests from Google with the add-on's system service account. `SERVICE_ACCOUNT_EMAIL` is a placeholder for the service account email and `HTTP_ENDPOINT` is a placeholder for the service URL of the add-on.

### Node.js

```javascript
/**
 * Determine whether a Google Workspace add-on request is legitimate.
 * 
 * @param {Object} req Request sent from Google Workspace add-on
 * @return {boolean} Whether the request is legitimate
 */
async function verifyAddOnRequest(req) {
  try {
    const authorization = req.headers.authorization;
    const idToken = authorization.substring('Bearer '.length, authorization.length);
    const ticket = await new OAuth2Client().verifyIdToken({idToken, audience: HTTP_ENDPOINT});
    return ticket.getPayload().email_verified
        && ticket.getPayload().email === SERVICE_ACCOUNT_EMAIL;
  } catch (unused) {
    return false;
  }
}
```

### Python

```python
def verifyAddOnRequest() -> bool:
  """Determine whether a Google Workspace add-on request is legitimate.

  Args:
    request: Request sent from Google Workspace add-on

  Returns:
    Whether the request is legitimate
  """
  try:
    bearer = request.headers.get('Authorization')[len("Bearer "):]
    token = id_token.verify_oauth2_token(bearer, requests.Request(), HTTP_ENDPOINT)
    return token['email'] == SERVICE_ACCOUNT_EMAIL

  except:
    return False
```

### Java

```java
/**
 * Determine whether a Google Workspace add-on request is legitimate.
 * 
 * @param event Event sent from Google Workspace add-on
 * @param authorization Authorization header from the request
 * @return {boolean} Whether the request is legitimate
 */
private boolean verifyAddOnRequest(JsonNode event, String authorization) throws Exception {
  JsonFactory factory = JacksonFactory.getDefaultInstance();

  GoogleIdTokenVerifier verifier =
    new GoogleIdTokenVerifier.Builder(new ApacheHttpTransport(), factory)
      .setAudience(Collections.singletonList(HTTP_ENDPOINT))
      .build();

  String bearer = authorization.substring("Bearer ".length(), authorization.length());
  GoogleIdToken idToken = GoogleIdToken.parse(factory, bearer);
  return idToken != null
    && verifier.verify(idToken)
    && idToken.getPayload().getEmailVerified()
    && idToken.getPayload().getEmail().equals(SERVICE_ACCOUNT_EMAIL);
}
```

## Test your add-on

To install and test your add-on from the Google Cloud console, see the Install an unpublished add-on section.

To test your add-on programmatically, view the Google Workspace add-ons API reference documentation. You can also use gcloud commands.

### Install an unpublished add-on

To install your add-on for testing or personal use, follow these steps:

1. In the add-on's Cloud project, go to the Google Workspace Marketplace SDK's **HTTP Deployments** tab.
2. Next to the deployment you want to test, click **Install**.

### Uninstall an unpublished add-on

To uninstall an unpublished add-on, follow these steps:

1. In the add-on's Cloud project, go to the Google Workspace Marketplace SDK's **HTTP Deployments** tab.
2. Next to the deployment you want to uninstall, click **Uninstall**.

## Sample JSON Schemas

You can incorporate the following schema samples into your development environment. For example, see Editing JSON with Visual Studio Code.

### JSON Card Interfaces

#### Generic Card

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "description": "The card object used to build UIs for Google Workspace add-ons.",
  "definitions": {
    "textParagraph": {
      "$id": "/properties/textParagraph",
      "type": "object",
      "description": "Text paragraph widget.",
      "required": [
        "text"
      ],
      "properties": {
        "text": {
          "type": "string",
          "description": "The text of the paragraph. Can contain formatted text."
        }
      }
    },
    "image": {
      "$id": "/properties/image",
      "type": "object",
      "description": "Image widget.",
      "required": [
        "imageUrl"
      ],
      "properties": {
        "imageUrl": {
          "type": "string",
          "description": "Sets the image to use by providing its URL or data string."
        },
        "altText": {
          "type": "string",
          "description": "Sets the alternative text of the image for accessibility."
        },
        "onClick": {
          "type": "object",
          "description": "Sets an action that executes when the object is clicked.",
          "$ref": "#/definitions/onClick"
        }
      }
    },
    "icon": {
      "$id": "/properties/icon",
      "type": "object",
      "description": "The icon, can be specified by KnownIcon string or a URL.",
      "oneOf": [
        {
          "properties": {
            "knownIcon": {
              "type": "string",
              "description": "The icon specified by the string name of a list of known icons"
            },
            "iconUrl": {
              "type": "string",
              "description": "The icon specified by a URL."
            }
          }
        }
      ],
      "properties": {
        "altText": {
          "type": "string",
          "description": "The description of icon which is used for accessibility."
        }
      }
    },
    "divider": {
      "$id": "/properties/divider",
      "type": "object",
      "description": "A horizontal divider."
    },
    "button": {
      "$id": "/properties/button",
      "type": "object",
      "description": "A button. Can be a text button or an image button.",
      "required": ["onClick", "text"],
      "properties": {
        "text": {
          "type": "string",
          "description": "The text of the button."
        },
        "icon": {
          "type": "object",
          "description": "The icon image",
          "$ref": "#/definitions/icon"
        },
        "color": {
          "type": "object",
          "description": "If set, the button is filled with solid background.",
          "$ref": "#/definitions/color"
        },
        "onClick": {
          "type": "object",
          "description": "The onClick action of the button.",
          "$ref": "#/definitions/onClick"
        },
        "disabled": {
          "type": "boolean",
          "description": "If true, the button is displayed in a disabled state and doesn't respond to user actions"
        }
      }
    },
    "buttonList": {
      "$id": "/properties/buttonList",
      "type": "object",
      "properties": {
        "buttons": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/button"
          },
          "description": "A list of buttons laid out horizontally"
        }
      }
    },
    "decoratedText": {
      "$id": "/properties/decoratedText",
      "type": "object",
      "required": [
        "text"
      ],
      "properties": {
        "button" : {
          "type": "object",
          "description": "A button that can be clicked to trigger an action",
          "$ref": "#/definitions/button"
        },
        "switchControl": {
          "type": "object",
          "description": "A switch widget can be clicked to change its state or trigger an action.",
          "$ref": "#/definitions/switchControl"
        },
        "icon": {
          "type": "object",
          "description": "The icon displayed in front of the text.",
          "$ref": "#/definitions/icon"
        },
        "imageType": {
          "type": "string",
          "enum": [
            "SQUARE",
            "CIRCLE"
          ],
          "description": "Define the cropping of the image."
        },
        "topLabel": {
          "type": "string",
          "description": "The formatted text label that shows above the main text."
        },
        "text": {
          "type": "string",
          "description": "The main widget formatted text."
        },
        "wrapText": {
          "type": "boolean",
          "description": "The wrap text setting. If true, the text is wrapped and displayed in multiline.\nOtherwise the text is truncated."
        },
        "bottomLabel": {
          "type": "string",
          "description": "The formatted text label that shows below the main text."
        },
        "onClick": {
          "type": "object",
          "description": "Only the top/bottom label + content region is clickable.",
          "$ref": "#/definitions/onClick"
        }
      }
    },
    "switchControl": {
      "$id": "/properties/switchControl",
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "description": "The name of the switch widget which is used in formInput."
        },
        "value": {
          "type": "string",
          "description": "The value is what is passed back in the Apps Script callback."
        },
        "selected": {
          "type": "boolean",
          "description": "If the switch is selected."
        },
        "onChangeAction": {
          "type": "object",
          "description": "The action when the switch state is changed.",
          "$ref": "#/definitions/action"
        },
        "controlType": {
          "type": "string",
          "description": "The control type, it could be either Switch or Checkbox.",
          "enum": [
            "SWITCH",
            "CHECKBOX"
          ]
        }
      }
    },
    "onClick": {
      "$id": "/properties/onClick",
      "type": "object",
      "properties": {
        "action": {
          "type": "object",
          "$ref": "#/definitions/action",
          "description": "An action is triggered by this onClick, if specified."
        },
        "openLink": {
          "type": "object",
          "$ref": "#/definitions/openLink",
          "description": "This onClick triggers an open link action if specified."
        },
        "openDynamicLinkAction": {
          "type": "object",
          "$ref": "#/definitions/action",
          "description": "An add-on triggers this action when the action needs to open a link.\nThis differs from the openLink above in that this needs to talk to server to get the link.\nThus some preparation work is required for web client to do before the open link action response comes back."
        },
        "card": {
          "type": "object",
          "$ref": "#/definitions/card",
          "description": "A new card is pushed to the card stack after clicking if specified."
        }
      }
    },
    "openLink": {
      "$id": "/properties/openLink",
      "description": "Opens a URL",
      "required": ["url"],
      "properties": {
        "url": {
          "type": "string",
          "description": "The URL to open."
        },
        "openAs": {
          "type": "string",
          "description": "When an onClick opens a link, then the client can either open it as a \n full size (window if that is the frame used by the client), or an \n overlay (such as a pop-up). The implementation depends on the client\nplatform capabilities, and the value selected may be ignored if the\nclient does not support it. FULL_SIZE is supported by all clients.",
          "enum": [
            "FULL_SIZE",
            "OVERLAY"
          ]
        },
        "onClose": {
          "type": "string",
          "enum": [
            "NOTHING",
            "RELOAD"
          ]
        }
      }
    },
    "textInput": {
      "$id": "/properties/textInput",
      "type": "object",
      "description": "A text input is a UI item where the users can input text.",
      "required": ["name"],
      "properties": {
        "name": {
          "type": "string",
          "description": "The name of the text input which is used in formInput."
        },
        "label": {
          "type": "string",
          "description": "At least one of label and hintText is required to be specified."
        },
        "hintText": {
          "type": "string",
          "description": "The hint text."
        },
        "value": {
          "type": "string",
          "description": "The default value when no input from user."
        },
        "type": {
          "type": "string",
          "enum": [
            "SINGLE_LINE",
            "MULTIPLE_LINE"
          ],
          "description": "The style of the text (for example, single line or multiple line)."
        },
        "onChangeAction": {
          "type": "object",
          "description": "The onChange action (for example, invoke an Apps Script)",
          "$ref": "#/definitions/action"
        },
        "initialSuggestions": {
          "type": "object",
          "description": "The initial suggestions made before any user input",
          "$ref": "#/definitions/suggestions"
        },
        "autoCompleteAction": {
          "type": "object",
          "$ref": "#/definitions/action",
          "description": "The refresh function which returns suggestions based on the user's input text."
        },
        "multipleSuggestions": {
          "type": "boolean",
          "description": "When set to true, a user can input multiple suggestions items."
        }
      }
    },
    "suggestions": {
      "$id": "/properties/suggestions",
      "description": "A container wrapping elements necessary for showing suggestion items used in text input autocomplete.",
      "properties": {
        "items": {
          "type": "array",
          "description": "A list of suggestion items which will be used in are used in autocomplete.",
          "items": {
            "$ref": "#/definitions/suggestionItem"
          }
        }
      }
    },
    "suggestionItem": {
      "$id": "/properties/suggestionItem",
      "type": "object",
      "description": "A Suggestion Item. Only supports text for now.",
      "properties": {
        "text": {
          "type": "string",
          "description": "Text."
        }
      }
    },
    "selectionInput": {
      "$id": "/properties/selectionInput",
      "description": "A widget which creates a UI item (for example, a drop-down list) with options for users to select.",
      "required": ["name"],
      "properties": {
        "name": {
          "type": "string",
          "description": ""
        },
        "label": {
          "type": "string",
          "description": "The label displayed ahead of the switch control."
        },
        "type": {
          "type": "string",
          "description": "The type of the selection.",
          "enum": [
            "CHECK_BOX",
            "RADIO_BUTTON",
            "SWITCH",
            "DROPDOWN"
          ]
        },
        "items": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/selectionItem"
          },
          "description": "The item/items in the switch control."
        },
        "onChangeAction": {
          "type": "object",
          "description": "If specified, form is submitted when selection changes",
          "$ref": "#/definitions/action"
        }
      }
    },
    "selectionItem": {
      "type":"object",
      "$id": "/properties/selectionItem",
      "description": "The item in the switch control.",
      "properties": {
        "text": {
          "type": "string",
          "description": "The text to be displayed"
        },
        "value": {
          "type": "string",
          "description": "The value associated with this item which is sent back to Apps Script.\nThe client should use this as a form input value."
        },
        "selected": {
          "type": "boolean",
          "description": "If more than one items are selected for RADIO_BUTTON or DROPDOWN,\nthe first selected item is treated as selected and the after ones are all ignored."
        }
      }
    },
    "dateTimePicker": {
      "$id": "/properties/dateTimePicker",
      "description": "The widget to allow users to specify date and time",
      "properties": {
        "name": {
          "type": "string",
          "description": "The name of the text input which is used in formInput, and uniquely identifies this input."
        },
        "label": {
          "type": "string",
          "description": "The label for the field, which is displayed to the user."
        },
        "type": {
          "type": "string",
          "description": "The type of the date time picker.",
          "enum": [
            "DATE_AND_TIME",
            "DATE_ONLY",
            "TIME_ONLY"
          ]
        },
        "valueMsEpoch": {
          "type": "number",
          "description": "The value to display which can be the default value before user input or previous user input.\nIt is represented in milliseconds (Epoch time)"
        },
        "timezoneOffsetDate": {
          "type": "number",
          "description": "The number representing the time-zone offset from UTC, in minutes."
        },
        "onChangeAction": {
          "type": "object",
          "description": "Triggered when the user clicks on the Save, or Clear button from the date time picker dialog.",
          "$ref": "#/definitions/action"
        }
      }
    },
    "borderStyle": {
      "$id": "/properties/borderStyle",
      "type": "object",
      "description": "A border style.",
      "required": ["type"],
      "properties": {
        "type": {
          "type": "string",
          "description": "The border type.",
          "enum": [
            "NO_BORDER",
            "STROKE"
          ]
        },
        "strokeColor": {
          "description": "The border color.",
          "$ref": "#/definitions/color"
        },
        "cornerRadius": {
          "type": "number",
          "description": "The border corner radius."
        }
      }
    },
    "imageCropStyle": {
      "$id": "/properties/imageCropStyle",
      "type": "object",
      "description": "A crop style that can be applied to images.",
      "required": ["type"],
      "properties": {
        "type": {
          "type": "string",
          "description": "The crop type.",
          "enum": [
            "SQUARE",
            "CIRCLE",
            "RECTANGLE_CUSTOM",
            "RECTANGLE_4_3"
          ]
        },
        "aspectRatio": {
          "type": "number",
          "description": "The aspect ratio for a custom rectangular crop."
        }
      }
    },
    "imageComponent": {
      "$id": "/properties/imageComponent",
      "type": "object",
      "description": "An image and its properties.",
      "required": ["imageUri"],
      "properties": {
        "imageUri": {
          "type": "string",
          "description": "The URL for the image resource."
        },
        "altText": {
          "type": "string",
          "description": "The accessibility label for the image."
        },
        "cropStyle": {
          "$ref": "#/definitions/imageCropStyle",
          "description": "The crop style to apply to the image."
        },
        "borderStyle": {
          "$ref": "#/definitions/borderStyle",
          "description": "The border style to apply to the image."
        }
      }
    },
    "grid": {
      "$id": "/properties/grid",
      "type": "object",
      "description": "A grid that displays a collection of grid items.",
      "required": [],
      "properties": {
        "title": {
          "type": "string",
          "description": "The title of the grid."
        },
        "items": {
          "description": "List of grid items.",
          "type": "array",
          "items": {
            "$ref": "#/definitions/griditem"
          }
        },
        "borderStyle": {
          "description": "The border style for the grid items.",
          "$ref": "#/definitions/borderStyle"
        },
        "columnCount": {
          "type": "number",
          "description": "The number of columns in the grid."
        },
        "onClick": {
          "description": "The action that executes when a grid item is clicked.",
          "$ref": "#/definitions/onClick"
        }
      }
    },
    "griditem": {
      "$id": "/properties/griditem",
      "type": "object",
      "description": "An item that can be displayed in a grid widget.",
      "required": [],
      "properties": {
        "id": {
          "type": "string",
          "description": "An identifier for the grid item."
        },
        "image": {
          "description": "The image to display in the grid item.",
          "$ref": "#/definitions/imageComponent"
        },
        "title": {
          "type": "string",
          "description": "The title of the grid item."
        },
        "subtitle": {
          "type": "string",
          "description": "The subtitle of the grid item."
        },
        "textAlignment": {
          "description": "The text alignment for the grid item's text.",
          "$ref": "#/definitions/horizontalAlignment"
        },
        "layout": {
          "type": "string",
          "description": "The grid item layout.",
          "enum": [
            "TEXT_BELOW",
            "TEXT_ABOVE"
          ]
        }
      }
    },
    "horizontalAlignment": {
      "$id": "/properties/horizontalAlignment",
      "type": "string",
      "description": "Horizontal alignment options.",
      "enum": [
        "START",
        "CENTER",
        "END"
      ]
    },
    "widget": {
      "$id": "/properties/widget",
      "type": "object",
      "properties": {
        "textParagraph": {
          "type": "object",
          "description": "Display a text paragraph in this widget",
          "$ref": "#/definitions/textParagraph"
        },
        "image": {
          "type": "object",
          "description": "Display an image in this widget",
          "$ref": "#/definitions/image"
        },
        "decoratedText": {
          "type": "object",
          "description": "Display a decorated text item in this widget",
          "$ref": "#/definitions/decoratedText"
        },
        "buttonList": {
          "type": "object",
          "description": "A List of buttons",
          "$ref": "#/definitions/buttonList"
        },
        "textInput": {
          "type": "object",
          "description": "Display a text input in this widget",
          "$ref": "#/definitions/textInput"
        },
        "selectionInput": {
          "type": "object",
          "description": "Display a switch control in this widget",
          "$ref": "#/definitions/selectionInput"
        },
        "dateTimePicker": {
          "type": "object",
          "description": "Display a date/time picker in this widget",
          "$ref": "#/definitions/dateTimePicker"
        },
        "horizontalAlignment": {
          "description": "The horizontal alignment of this widget.",
          "$ref": "#/definitions/horizontalAlignment"
        },
        "divider": {
          "description": "Inserts a divider.",
          "$ref": "#/definitions/divider"
        },
        "grid": {
          "description": "Display a grid control in this widget.",
          "$ref": "#/definitions/grid"
        }
      }
    },
    "section": {
      "$id": "/properties/section",
      "type": "object",
      "required": [
        "widgets"
      ],
      "properties": {
        "header": {
          "type": "string",
          "description": "The text header of a section"
        },
        "collapsible": {
          "type": "boolean",
          "description": "Whether section can be collapsed or not."
        },
        "widgets": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/widget"
          },
          "description": "The widgets within a section. Example of a widget is TextParagraph or Image."
        },
        "uncollapsibleWidgetsCount": {
          "type": "number",
          "description": "The number of uncollapsable widgets"
        }
      }
    },
    "color": {
      "$id": "/properties/color",
      "type": "object",
      "description": "Represents a color in the RGBA color space.",
      "required": [
        "red",
        "green",
        "blue"
      ],
      "properties": {
        "red": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "The amount of red in the color as a value in the interval [0, 1]"
        },
        "green": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "The amount of green in the color as a value in the interval [0, 1]"
        },
        "blue": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "The amount of blue in the color as a value in the interval [0, 1]"
        },
        "alpha": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "The alpha value of the color as a value in the interval [0, 1]. 1 is sloid color and 0 is transparent"
        }
      }
    },
    "cardHeader": {
      "$id": "/properties/cardHeader",
      "type": "object",
      "description": "Optional header in the card.",
      "required": [
        "title"
      ],
      "properties": {
        "title": {
          "type": "string",
          "description": "Required title in the header."
        },
        "subtitle": {
          "type": "string",
          "description": "Optional - renders beneath the title. If not specified, title will take up both lines."
        },
        "imageUrl": {
          "type": "string",
          "description": "Optional - renders an image on the right of the title."
        },
        "imageType": {
          "type": "string",
          "enum": [
            "SQUARE",
            "CIRCLE"
          ],
          "description": "Define the cropping of the image in the header."
        },
        "imageAltText": {
          "type": "string",
          "description": "The Alternative text of this image"
        }
      }
    },
    "cardAction": {
      "$id": "/properties/cardAction",
      "description": "A Card action is the action associated with the card.",
      "properties": {
        "actionLabel": {
          "type": "string",
          "description": "The label used to be displayed in the action menu item."
        },
        "onClick": {
          "type": "object",
          "description": "The onClick action for this action item.",
          "$ref": "#/definitions/onClick"
        }
      }
    },
    "cardFixedFooter": {
      "$id": "/properties/cardFixedFooter",
      "description": "A persistent (sticky) footer that is added to the bottom of the card.",
      "properties": {
        "primaryButton": {
          "type": "object",
          "description": "The Primary button of the fixed footer.",
          "$ref": "#/definitions/button"
        },
        "secondaryButton": {
          "type": "object",
          "description": "The Secondary button of the fixed footer.",
          "$ref": "#/definitions/button"
        }
      }
    },
    "card": {
      "$id": "/properties/card",
      "type": "object",
      "required": [
        "sections"
      ],
      "properties": {
        "header": {
          "type": "object",
          "description": "The Header of the card.",
          "$ref": "#/definitions/cardHeader"
        },
        "sections": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/section"
          },
          "description": "A card consist of 1 or more sections. Widgets are defined within a section."
        },
        "cardActions": {
          "type": "object",
          "description": "The actions of this card.",
          "$ref": "#/definitions/cardAction"
        },
        "name": {
          "type": "string",
          "description": "Name of the card which is used as an identifier for the card in the card navigation."
        },
        "fixedFooter": {
          "type": "object",
          "description": "The fixed footer that is shown at the bottom of this card.",
          "$ref": "#/definitions/cardFixedFooter"
        },
        "displayStyle": {
          "type": "string",
          "description": "The Display Style for the peekCardHeader.",
          "enum": [
            "DISPLAY_STYLE_UNSPECIFIED",
            "PEEK",
            "REPLACE"
          ]
        },
        "peekCardHeader": {
          "type": "object",
          "description": "When displaying contextual content, the peek card header acts as a placeholder so that the user can\nnavigate forward between the homepage cards and the contextual cards.",
          "$ref": "#/definitions/cardHeader"
        }
      }
    },
    "action": {
      "$id": "/properties/action",
      "type": "object",
      "description": "An action that describes the behavior when a form is submitted - triggered from an onclick event on an input widget (e.g. button).",
      "required": [
        "function"
      ],
      "properties": {
        "function": {
          "description": "The apps script callback function or the HTTPS endpoint if using HTTP deployments.",
          "type": "string"
        }
      }
    }
  },
  "type": "object",
  "$ref": "#/definitions/card"
}
```

#### Expense App

```json
{
  "action": {
    "navigations": [
      {
        "pushCard": {
          "sections": [
            {
              "header": "Budget Performance",
              "widgets": [
                {
                  "decoratedText": {
                    "text": "**Current Quarter**  \nBudget $18,000 (Ends in 5 days)  \nSpent: $410.75  \n",
                    "wrapText": true
                  }
                },
                {
                  "decoratedText": {
                    "text": "**Top Expense Category**"
                  }
                },
                {
                  "decoratedText": {
                    "text": "Flights · 30%",
                    "icon": {
                      "iconUrl" : "http://ssl.gstatic.com/travel-trips-fe/icon_flight_grey_64.png"
                    }
                  }
                },
                {
                  "decoratedText": {
                    "text": "Hotels · 50%",
                    "icon": {
                      "iconUrl" : "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png"
                    }
                  }
                }
              ]
            },
            {
              "header": "Expense Awaiting Your Approval",
              "widgets": [
                {
                  "decoratedText": {
                    "text": "Submitted by Pam Bee",
                    "icon": {
                      "iconUrl" : "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQDQGRxqHJ2XZenPL496tC1EkP2b8wtvENQ4QIClnde2Hq1C7u3"
                    }
                  }
                },
                {
                  "decoratedText": {
                    "text": "**Team Lunch (Internal)**  \nCost: **$85.00 USD**  \nDate: **10/16/2019**  \nExpense no. #7453"
                  }
                },
                {
                  "buttonList": {
                    "buttons": [
                      {
                        "text": "Approve",
                        "color": {
                          "red": 0,
                          "green": 0.4784,
                          "blue": 0.353
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/approve"
                          }
                        }
                      },
                      {
                        "text": "Decline",
                        "color": {
                          "red": 1,
                          "green": 0.07843,
                          "blue": 0.07843
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/decline"
                          }
                        }
                      },
                      {
                        "text": "View Details",
                        "color": {
                          "red": 0.650,
                          "green": 0.650,
                          "blue": 0.650
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/view"
                          }
                        }
                      }
                    ]
                  }
                }
              ]
            },
            {
              "widgets": [
                {
                  "decoratedText": {
                    "text": "Submitted by Dwight Smith",
                    "icon": {
                      "iconUrl" : "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcQDQGRxqHJ2XZenPL496tC1EkP2b8wtvENQ4QIClnde2Hq1C7u3"
                    }
                  }
                },
                {
                  "decoratedText": {
                    "text": "**Flight to New York**  \nCost: **530.00 USD**  \nDate: **11/21/2019**  \nExpense no. #9866"
                  }
                },
                {
                  "buttonList": {
                    "buttons": [
                      {
                        "text": "Approve",
                        "color": {
                          "red": 0,
                          "green": 0.4784,
                          "blue": 0.353
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/approve"
                          }
                        }
                      },
                      {
                        "text": "Decline",
                        "color": {
                          "red": 1,
                          "green": 0.07843,
                          "blue": 0.07843
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/decline"
                          }
                        }
                      },
                      {
                        "text": "View Details",
                        "color": {
                          "red": 0.650,
                          "green": 0.650,
                          "blue": 0.650
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/view"
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
```

#### Form Submit

```javascript
/**
 * A sample Google Workspace add-on with a form submit with a happy/sad button.
 */
exports.homepage = (req, res) => {
  console.log("event: ", req.body);
  console.log("headers: ",JSON.stringify(req.headers));
  let parameters = req.body.commonEventObject.parameters;
  if (parameters) {
    let happy = parameters.happy;
    if (happy == '1') {
      res.status(200).send(createHappyCard());
    } else {
      res.status(200).send(createSadCard());
    }
  } else {
    res.status(200).send(createQuestionCard());
  }
};

function createSadCard() {
  return {
    "renderActions": {
      "action": {
        "navigations": [
          {
            "pushCard": {
              "sections": [
                {
                  "widgets": [
                    {
                      "image": {
                        "imageUrl": "https://cdn.pixabay.com/photo/2017/08/15/12/58/emoticon-2643814_960_720.jpg"
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
  };
}

function createHappyCard() {
  return {
    "renderActions": {
      "action": {
        "navigations": [
          {
            "pushCard": {
              "sections": [
                {
                  "widgets": [
                    {
                      "image": {
                        "imageUrl": "https://dg.imgix.net/do-you-think-you-re-happy-jgdbfiey-en/landscape/do-you-think-you-re-happy-jgdbfiey-9bb0198eeccd0a3c3c13aed064e2e2b3.jpg"
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
  };
}

function createQuestionCard() {
  return {
    "action": {
      "navigations": [
        {
          "pushCard": {
            "sections": [
              {
                "widgets": [
                  {
                    "textParagraph": {
                      "text": "Are you having a good day today?"
                    }
                  },
                  {
                    "buttonList": {
                      "buttons": [
                        {
                          "text": "Happy",
                          "color": {
                            "red": 0,
                            "green": 0.4784,
                            "blue": 0.353
                          },
                          "onClick": {
                            "action": {
                              "function": "https://us-central1-elevated-surge-267316.cloudfunctions.net/HttpGSAO",
                              "parameters": [
                                {
                                  "key": "happy",
                                  "value": "1"
                                }
                              ]
                            }
                          }
                        },
                        {
                          "text": "Sad",
                          "color": {
                            "red": 1,
                            "green": 0.07843,
                            "blue": 0.07843
                          },
                          "onClick": {
                            "action": {
                              "function": "https://us-central1-elevated-surge-267316.cloudfunctions.net/HttpGSAO",
                              "parameters": [
                                {
                                  "key": "happy",
                                  "value": "0"
                                }
                              ]
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
  };
}
```

#### Approval

```json
{
  "action": {
    "navigations": [
      {
        "pushCard": {
          "sections": [
            {
              "widgets": [
                {
                  "textParagraph": {
                    "text": "You have a new request:"
                  }
                },
                {
                  "textParagraph": {
                    "text": "[John Dolittle - New Device Request](https://www.domain.com/request/12345)"
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Type:",
                    "text": "Computer (laptop)"
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "When:",
                    "text": "Submitted Aug 10"
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Reason:",
                    "text": "Keyboard is not working"
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Specs:",
                    "text": "Cheetah Pro 15"
                  }
                },
                {
                  "buttonList": {
                    "buttons": [
                      {
                        "text": "Approve",
                        "color": {
                          "red": 0,
                          "green": 0.4784,
                          "blue": 0.353
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/approve"
                          }
                        }
                      },
                      {
                        "text": "Deny",
                        "color": {
                          "red": 1,
                          "green": 0.07843,
                          "blue": 0.07843
                        },
                        "onClick": {
                          "openLink": {
                            "url": "https://www.domain.com/deny"
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
```

#### Contacts List

```javascript
/**
 * A sample Google Workspace add-on that creates a top level card with a list of
 * contacts. Clicking on a contact will navigate (client side) to a full contact
 * card.
 */
exports.homepage = (req, res) => {
  res.status(200).send(createListCard());
};

function createContactCard(name, title, email, phone, location) {
  return {
    "header": {
      "imageType": "CIRCLE",
      "imageUrl": "https://ssl.gstatic.com/images/branding/product/1x/avatar_square_blue_512dp.png",
      "title": name,
      "subtitle": title
    },
    "sections": [
      {
        "widgets": [
          {
            "decoratedText": {
              "topLabel": "Email:",
              "text": email
            }
          },
          {
            "decoratedText": {
              "topLabel": "Phone Number:",
              "text": phone
            }
          },
          {
            "decoratedText": {
              "topLabel": "Location:",
              "text": location
            }
          }
        ]
      }
    ]
  };
}

function createContactListEntry(name, title, email, phone, location) {
  return {
    "decoratedText": {
      "topLabel": title,
      "text": name,
      "onClick": {
        "card": createContactCard(name, title, email, phone, location)
      },
      "icon": {
        "iconUrl": "https://ssl.gstatic.com/images/branding/product/1x/avatar_square_blue_512dp.png"
      }
    }
  };
}

function createListCard() {
  var LIST1 = createContactListEntry("John Dolittle", "President", "john@gmail.com", "800-555-0100", "Markham, ON");
  var LIST2 = createContactListEntry("Huckleberry Finn", "CFO", "huck@gmail.com", "800-555-0111", "Kingston, ON");
  var LIST3 = createContactListEntry("Grace Harlowe", "Senior Director", "grace@gmail.com", "800-555-0122", "Toronto, ON");
  return {
    "action": {
      "navigations": [
        {
          "pushCard": {
            "sections": [
              {
                "widgets": [
                  LIST1,
                  LIST2,
                  LIST3
                ]
              }
            ]
          }
        }
      ]
    }
  };
}
```

#### Third-party Authorization

```json
{
  "custom_authorization_prompt": {
    "action": {
      "navigations": [
        {
          "pushCard": {
            "sections": [
              {
                "widgets": [
                  {
                    "image": {
                      "imageUrl": "https://www.example.com/images/logo",
                      "altText": "Example organization logo"
                    }
                  },
                  {
                    "divider": {}
                  },
                  {
                    "textParagraph": {
                      "text": "Sign in to get started."
                    }
                  },
                  {
                    "buttonList": {
                      "buttons": [
                        {
                          "text": "Sign in",
                          "onClick": {
                            "openLink": {
                              "url": "https://www.example.com/auth",
                              "onClose": "RELOAD",
                              "openAs": "OVERLAY"
                            }
                          },
                          "color": {
                            "red": 0,
                            "green": 0,
                            "blue": 1,
                            "alpha": 1
                          }
                        }
                      ]
                    }
                  },
                  {
                    "textParagraph": {
                      "text": "If you don't have an account, <a href=\"https://www.example.com/signup\">sign up</a> here."
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
```

### JSON Widgets

#### Generic Widgets

```json
{
  "$schema": "/Users/dummy_user/Documents/JSON_schema/renderActionSchema.json",
  "action": {
    "navigations": [
      {
        "pushCard": {
          "header": {
            "title": "Main Card"
          },
          "name": "Main Card",
          "peekCardHeader": {
            "title": "This is a peek card",
            "imageType": "SQUARE",
            "imageUrl": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
            "imageAltText": "Image of Cards",
            "subtitle": "No Subtitle"
          },
          "cardActions": [
            {
              "actionLabel": "This is Card action - 1",
              "onClick": {
                "openDynamicLinkAction": {
                  "function": "https://dummy-function-from-resources.net/openLinkCallback"
                }
              }
            },
            {
              "actionLabel": "This is Card action - 2",
              "onClick": {
                "action": {
                  "function": "https://dummy-function-from-resources.net/generic_submit_form_response"
                }
              }
            },
            {
              "actionLabel": "This is Card action - 3",
              "onClick": {
                "openLink": {
                  "onClose": "RELOAD",
                  "openAs": "OVERLAY",
                  "url": "https://dummy-function-from-resources.net/open_link_sample"
                }
              }
            },
            {
              "actionLabel": "This is Card action - 4",
              "onClick": {
                "card": {
                  "header": {
                    "title": "This card is shown after card action 4 is clicked"
                  },
                  "sections": [
                    {
                      "widgets": [
                        {
                          "textParagraph": {
                            "text": "This is a sample text for the card that's shown after action 4 of the card is clicked"
                          }
                        }
                      ]
                    }
                  ]
                }
              }
            }
          ],
          "fixedFooter": {
            "primaryButton": {
              "text": "Primary Button",
              "color": {
                "red": 0,
                "blue": 0,
                "green": 0
              },
              "onClick": {
                "openLink": {
                  "url": "www.google.ca",
                  "onClose": "NOTHING",
                  "openAs": "FULL_SIZE"
                }
              }
            },
            "secondaryButton": {
              "text": "Secondary Button - Disabled",
              "disabled": true,
              "color": {
                "red": 0.32421,
                "blue": 0.23421,
                "green": 0.2353614
              },
              "onClick": {
                "openLink": {
                  "url": "www.google.com",
                  "onClose": "NOTHING",
                  "openAs": "FULL_SIZE"
                }
              }
            }
          },
          "sections": [
            {
              "header": "Section 1 - Date Time",
              "collapsible": true,
              "widgets": [
                {
                  "dateTimePicker": {
                    "name": "Date Time Picker - EST",
                    "label": "Date Time Picker - EST",
                    "valueMsEpoch": 1585166673000,
                    "onChangeAction": {
                      "function": "https://dummy-function-from-resources.net/sample_notification"
                    },
                    "timezoneOffsetDate": -240,
                    "type": "DATE_AND_TIME"
                  }
                },
                {
                  "dateTimePicker": {
                    "name": "Date Picker - CST",
                    "label": "Date Time Picker - CST",
                    "valueMsEpoch": 1585166673000,
                    "onChangeAction": {
                      "function": "https://dummy-function-from-resources.net/sample_notification"
                    },
                    "timezoneOffsetDate": -300,
                    "type": "DATE_AND_TIME"
                  }
                },
                {
                  "dateTimePicker": {
                    "name": "Date Time Picker - PST",
                    "label": "Date Time Picker - PST",
                    "valueMsEpoch": 1585166673000,
                    "onChangeAction": {
                      "function": "https://dummy-function-from-resources.net/sample_notification"
                    },
                    "timezoneOffsetDate": -420,
                    "type": "DATE_AND_TIME"
                  }
                }
              ]
            },
            {
              "header": "Section 2 - Decorated Text",
              "collapsible": true,
              "uncollapsibleWidgetsCount": 2,
              "widgets": [
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text CHECKBOX",
                    "switchControl": {
                      "controlType": "CHECKBOX",
                      "name": "Name - Check Box Sample",
                      "value": "Value - Check Box Sample"
                    },
                    "text": "Text - Decorated Text",
                    "bottomLabel": "Bottom Label - Decorated Text CHECKBOX",
                    "wrapText": false,
                    "onClick": {
                      "card": {
                        "header": {
                          "title": "Decorated Text - On Click Action Card"
                        },
                        "sections": [
                          {
                            "widgets": [
                              {
                                "image": {
                                  "imageUrl": "https://cataas.com/cat/says/hello%20world!",
                                  "altText": "Hello World - Cat Image"
                                }
                              }
                            ]
                          }
                        ]
                      }
                    }
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text SWITCH",
                    "switchControl": {
                      "controlType": "SWITCH",
                      "name": "Name - SWITCH Sample",
                      "value": "Value - SWITCH Sample"
                    },
                    "text": "Text - Decorated Text",
                    "bottomLabel": "Bottom Label - Decorated Text SWITCH",
                    "wrapText": false,
                    "onClick": {
                      "card": {
                        "header": {
                          "title": "Decorated Text - On Click Action Card"
                        },
                        "sections": [
                          {
                            "widgets": [
                              {
                                "image": {
                                  "imageUrl": "https://cataas.com/cat/says/hello%20world!",
                                  "altText": "Hello World - Cat Image",
                                  "onClick": {
                                    "action": {
                                      "function": "https://dummy-function-from-resources.net/pop_to_root"
                                    }
                                  }
                                }
                              }
                            ]
                          }
                        ]
                      }
                    }
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text Button",
                    "bottomLabel": "Bottom Label - Decorated Text Button",
                    "text": "Text - Decorated Text Button",
                    "button": {
                      "icon": {
                        "altText": "Assessment Blue",
                        "icon_url": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png"
                      },
                      "text": "Assessment Blue",
                      "onClick": {
                        "openLink": {
                          "url": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
                          "openAs": "OVERLAY",
                          "onClose": "RELOAD"
                        }
                      }
                    }
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text CHECKBOX",
                    "switchControl": {
                      "controlType": "CHECKBOX",
                      "name": "Name - Check Box Sample",
                      "value": "Value - Check Box Sample"
                    },
                    "text": "Text - Decorated Text",
                    "bottomLabel": "Bottom Label - Decorated Text CHECKBOX",
                    "wrapText": false,
                    "onClick": {
                      "card": {
                        "header": {
                          "title": "Decorated Text - On Click Action Card"
                        },
                        "sections": [
                          {
                            "widgets": [
                              {
                                "image": {
                                  "imageUrl": "https://cataas.com/cat/says/hello%20world!",
                                  "altText": "Hello World - Cat Image"
                                }
                              }
                            ]
                          }
                        ]
                      }
                    }
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text Icon",
                    "bottomLabel": "Bottom Label - Decorated Text Icon",
                    "text": "Text - Decorated Text Icon",
                    "icon": {
                      "iconUrl": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
                      "altText": "Arrow Right Blue"
                    }
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text Wrap",
                    "bottomLabel": "Bottom Label - Decorated Text Wrap",
                    "text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam fringilla facilisis ne.",
                    "wrapText": true
                  }
                },
                {
                  "decoratedText": {
                    "topLabel": "Top Label - Decorated Text Non-Wrap",
                    "bottomLabel": "Bottom Label - Decorated Text Non-Wrap",
                    "text": "Nunc ultrices massa ut nisl porttitor, ut euismod nisl tincidunt. Vivamus pharetra, est sed sagittis consequat, arcu nisi.",
                    "wrapText": false
                  }
                }
              ]
            },
            {
              "header": "Section 3 - Button List",
              "collapsible": true,
              "widgets": [
                {
                  "buttonList": {
                    "buttons": [
                      {
                        "icon": {
                          "iconUrl": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
                          "altText": "G - Button"
                        },
                        "color": {
                          "red": 0,
                          "blue": 0,
                          "green": 1
                        },
                        "disabled": false,
                        "onClick": {
                          "openLink": {
                            "url": "www.google.ca/"
                          }
                        },
                        "text": "Green - Google.ca"
                      },
                      {
                        "color": {
                          "red": 1,
                          "blue": 0,
                          "green": 0
                        },
                        "disabled": false,
                        "onClick": {
                          "action": {
                            "function": "https://dummy-function-from-resources.net/pop_to_card_2"
                          }
                        },
                        "text": "Pop to Card 2"
                      },
                      {
                        "color": {
                          "red": 0,
                          "blue": 1,
                          "green": 0
                        },
                        "disabled": false,
                        "onClick": {
                          "openLink": {
                            "url": "www.google.ca/"
                          }
                        },
                        "text": "Blue - Google"
                      },
                      {
                        "color": {
                          "red": 1,
                          "blue": 1,
                          "green": 1
                        },
                        "disabled": true,
                        "onClick": {
                          "openLink": {
                            "url": "www.google.ca/"
                          }
                        },
                        "text": "Disabled Button"
                      }
                    ]
                  }
                }
              ]
            },
            {
              "header": "Section 4 - Images",
              "collapsible": true,
              "widgets": [
                {
                  "image": {
                    "imageUrl": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
                    "onClick": {
                      "openLink": {
                        "url": "http://ssl.gstatic.com/travel-trips-fe/icon_hotel_grey_64.png",
                        "openAs": "FULL_SIZE"
                      }
                    }
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
```
