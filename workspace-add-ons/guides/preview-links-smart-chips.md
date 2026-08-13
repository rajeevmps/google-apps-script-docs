# Preview links with smart chips

Google Workspace add-ons can enhance link interactions in Docs, Sheets, and Slides by replacing them with smart chips or linked titles that reveal detailed previews.

## How users preview links

To preview links, users interact with _smart chips_ and _cards_.

When users type or paste a URL into a document or spreadsheet, Google Docs or Google Sheets prompts them to replace the link with a smart chip. The smart chip displays an icon and short title or description of the link's content. When the user hovers over the chip, they see a card interface that previews more information about the file or link.

### How users preview links in Slides

Third-party smart chips aren't supported for link previews in Slides. When users type or paste a URL into a presentation, Slides prompts them to replace the link with its title as linked text instead of a chip. When the user hovers over the link title, they see a card interface that previews information about the link.

## Prerequisites

### Apps Script

- A Google Workspace account.
- A Google Workspace add-on. To build an add-on, follow the quickstart.

### Node.js

- A Google Workspace account.
- A Google Workspace add-on. To build an add-on, follow the quickstart.

**Note:** The Node.js code samples in this guide are written to run as a Cloud Function.

### Python

- A Google Workspace account.
- A Google Workspace add-on. To build an add-on, follow the quickstart.

**Note:** The Python code samples in this guide are written to run as a Cloud Function using Python 3.9.

### Java

- A Google Workspace account.
- A Google Workspace add-on. To build an add-on, follow the quickstart.

## Optional: Set up authentication to a third-party service

If your add-on connects to a service that requires authorization, users must authenticate to the service to preview links. This means that when users paste a link from your service into a Docs, Sheets, or Slides file for the first time, your add-on must invoke the authorization flow.

To set up an OAuth service or custom authorization prompt, see Connect your add-on to a third-party service.

## Set up link previews for your add-on

This section explains how to set up link previews for your add-on, which includes the following steps:

1. Configure link previews in your add-on's manifest.
2. Build the smart chip and card interface for your links.

### Configure link previews

To configure link previews, specify the following sections and fields in your add-on's manifest:

1. Under the `addOns` section, add the `docs` field to extend Docs, the `sheets` field to extend Sheets, and the `slides` field to extend Slides.
2. In each field, implement the `linkPreviewTriggers` trigger that includes a `runFunction` (You define this function in the following section, Build the smart chip and card).

   To learn about what fields you can specify in the `linkPreviewTriggers` trigger, see the reference documentation for Apps Script manifests or deployment resources for other runtimes.

3. In the `oauthScopes` field, add the scope `https://www.googleapis.com/auth/workspace.linkpreview` so that users can authorize the add-on to preview links on their behalf.

As an example, see the `oauthScopes` and `addons` section of the following manifest that configures link previews for a support case service.

**Note:** For Slides, `labelText` and `localizedLabelText` don't render, but you must include `labelText` for when Slides starts supporting third-party smart chips. `localizedLabelText` is optional.

```json
{
  "oauthScopes": [
    "https://www.googleapis.com/auth/workspace.linkpreview"
  ],
  "addOns": {
    "common": {
      "name": "Preview support cases",
      "logoUrl": "https://www.example.com/images/company-logo.png",
      "layoutProperties": {
        "primaryColor": "#dd4b39"
      }
    },
    "docs": {
      "linkPreviewTriggers": [
        {
          "runFunction": "caseLinkPreview",
          "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "support/cases"
            },
            {
              "hostPattern": "*.example.com",
              "pathPrefix": "cases"
            },
            {
              "hostPattern": "cases.example.com"
            }
          ],
          "labelText": "Support case",
          "logoUrl": "https://www.example.com/images/support-icon.png",
          "localizedLabelText": {
            "es": "Caso de soporte"
          }
        }
      ]
    },
    "sheets": {
      "linkPreviewTriggers": [
        {
          "runFunction": "caseLinkPreview",
          "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "support/cases"
            },
            {
              "hostPattern": "*.example.com",
              "pathPrefix": "cases"
            },
            {
              "hostPattern": "cases.example.com"
            }
          ],
          "labelText": "Support case",
          "logoUrl": "https://www.example.com/images/support-icon.png",
          "localizedLabelText": {
            "es": "Caso de soporte"
          }
        }
      ]
    },
    "slides": {
      "linkPreviewTriggers": [
        {
          "runFunction": "caseLinkPreview",
          "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "support/cases"
            },
            {
              "hostPattern": "*.example.com",
              "pathPrefix": "cases"
            },
            {
              "hostPattern": "cases.example.com"
            }
          ],
          "labelText": "Support case",
          "logoUrl": "https://www.example.com/images/support-icon.png",
          "localizedLabelText": {
            "es": "Caso de soporte"
          }
        }
      ]
    }
  }
}
```

In the example, the Google Workspace add-on previews links for a company's support case service. The add-on specifies three URL patterns to preview links. Whenever a link matches one of the URL patterns, the callback function `caseLinkPreview` builds and displays a card and a smart chip in Docs, Sheets, or Slides, and replaces the URL with the link title.

### Build the smart chip and card

To return a smart chip and card for a link, you must implement any functions that you specified in the `linkPreviewTriggers` object.

When a user interacts with a link that matches a specified URL pattern, the `linkPreviewTriggers` trigger fires and its callback function passes the event object `EDITOR_NAME.matchedUrl.url` as an argument. You use the payload of this event object to build the smart chip and card for your link preview.

For example, if a user previews the link `https://www.example.com/cases/123456` in Docs, the following event payload is returned:

```json
{
  "docs": {
    "matchedUrl": {
      "url": "https://www.example.com/support/cases/123456"
    }
  }
}
```

To create the card interface, you use widgets to display information about the link. You can also build actions that let users open the link or modify its contents. For a list of available widgets and actions, see Supported components for preview cards.

To build the smart chip and card for a link preview:

1. Implement the function that you specified in the `linkPreviewTriggers` section of your add-on's manifest:
   1. The function must accept an event object containing `EDITOR_NAME.matchedUrl.url` as an argument and return a single `Card` object.
   2. If your service requires authorization, the function must also invoke the authorization flow.
2. For each preview card, implement any callback functions that provide widget interactivity for the interface. For example, if you include a button that says "View link," you can create an action that specifies a callback function to open the link in a new window. To learn more about widget interactions, see Add-on actions.

**Note:** For link previews, the card response is cached for each user for 5 minutes. During that time, if a user previews a link, they receive the cached response. The cache is cleared when the user refreshes the file, or after 5 minutes. If the title of the returned card has changed, the app then prompts the user to refresh the title.

The following code creates the callback function `caseLinkPreview` for Docs:

### Apps Script

```javascript
/**
* Entry point for a support case link preview.
*
* @param {!Object} event The event object.
* @return {!Card} The resulting preview link card.
*/
function caseLinkPreview(event) {

  // If the event object URL matches a specified pattern for support case links.
  if (event.docs.matchedUrl.url) {

    // Uses the event object to parse the URL and identify the case details.
    const caseDetails = parseQuery(event.docs.matchedUrl.url);

    // Builds a preview card with the case name, and description
    const caseHeader = CardService.newCardHeader()
      .setTitle(`Case ${caseDetails["name"][0]}`);
    const caseDescription = CardService.newTextParagraph()
      .setText(caseDetails["description"][0]);

    // Returns the card.
    // Uses the text from the card's header for the title of the smart chip.
    return CardService.newCardBuilder()
      .setHeader(caseHeader)
      .addSection(CardService.newCardSection().addWidget(caseDescription))
      .build();
  }
}

/**
* Extracts the URL parameters from the given URL.
*
* @param {!string} url The URL to parse.
* @return {!Map} A map with the extracted URL parameters.
*/
function parseQuery(url) {
  const query = url.split("?")[1];
  if (query) {
    return query.split("&")
    .reduce(function(o, e) {
      var temp = e.split("=");
      var key = temp[0].trim();
      var value = temp[1].trim();
      value = isNaN(value) ? value : Number(value);
      if (o[key]) {
        o[key].push(value);
      } else {
        o[key] = [value];
      }
      return o;
    }, {});
  }
  return null;
}
```

### Node.js

```javascript
/**
 * 
 * A support case link preview.
 *
 * @param {!URL} url The event object.
 * @return {!Card} The resulting preview link card.
 */
function caseLinkPreview(url) {
  // Builds a preview card with the case name, and description
  // Uses the text from the card's header for the title of the smart chip.
  // Parses the URL and identify the case details.
  const name = `Case ${url.searchParams.get("name")}`;
  return {
    action: {
      linkPreview: {
        title: name,
        previewCard: {
          header: {
            title: name
          },
          sections: [{
            widgets: [{
              textParagraph: {
                text: url.searchParams.get("description")
              }
            }]
          }]
        }
      }
    }
  };
}
```

### Python

```python
def case_link_preview(url):
    """A support case link preview.
    Args:
      url: A matching URL.
    Returns:
      The resulting preview link card.
    """

    # Parses the URL and identify the case details.
    query_string = parse_qs(url.query)
    name = f'Case {query_string["name"][0]}'
    # Uses the text from the card's header for the title of the smart chip.
    return {
        "action": {
            "linkPreview": {
                "title": name,
                "previewCard": {
                    "header": {
                        "title": name
                    },
                    "sections": [{
                        "widgets": [{
                            "textParagraph": {
                                "text": query_string["description"][0]
                            }
                        }]
                    }],
                }
            }
        }
    }
```

### Java

```java
/**
 * A support case link preview.
 *
 * @param url A matching URL.
 * @return The resulting preview link card.
 */
JsonObject caseLinkPreview(URL url) throws UnsupportedEncodingException {
  // Parses the URL and identify the case details.
  Map<String, String> caseDetails = new HashMap<String, String>();
  for (String pair : url.getQuery().split("&")) {
      caseDetails.put(URLDecoder.decode(pair.split("=")[0], "UTF-8"), URLDecoder.decode(pair.split("=")[1], "UTF-8"));
  }

  // Builds a preview card with the case name, and description
  // Uses the text from the card's header for the title of the smart chip.
  JsonObject cardHeader = new JsonObject();
  String caseName = String.format("Case %s", caseDetails.get("name"));
  cardHeader.add("title", new JsonPrimitive(caseName));

  JsonObject textParagraph = new JsonObject();
  textParagraph.add("text", new JsonPrimitive(caseDetails.get("description")));

  JsonObject widget = new JsonObject();
  widget.add("textParagraph", textParagraph);

  JsonArray widgets = new JsonArray();
  widgets.add(widget);

  JsonObject section = new JsonObject();
  section.add("widgets", widgets);

  JsonArray sections = new JsonArray();
  sections.add(section);

  JsonObject previewCard = new JsonObject();
  previewCard.add("header", cardHeader);
  previewCard.add("sections", sections);

  JsonObject linkPreview = new JsonObject();
  linkPreview.add("title", new JsonPrimitive(caseName));
  linkPreview.add("previewCard", previewCard);

  JsonObject action = new JsonObject();
  action.add("linkPreview", linkPreview);

  JsonObject renderActions = new JsonObject();
  renderActions.add("action", action);

  return renderActions;
}
```

#### Supported components for preview cards

Google Workspace add-ons support the following widgets and actions for link preview cards:

### Apps Script

| Card Service field | Type |
|---|---|
| `TextParagraph` | Widget |
| `DecoratedText` | Widget |
| `Image` | Widget |
| `IconImage` | Widget |
| `ButtonSet` | Widget |
| `TextButton` | Widget |
| `ImageButton` | Widget |
| `Grid` | Widget |
| `Divider` | Widget |
| `OpenLink` | Action |
| `Navigation` | Action |

Only the `updateCard` method is supported for Navigation.

### JSON

| Card (`google.apps.card.v1`) field | Type |
|---|---|
| `TextParagraph` | Widget |
| `DecoratedText` | Widget |
| `Image` | Widget |
| `Icon` | Widget |
| `ButtonList` | Widget |
| `Button` | Widget |
| `Grid` | Widget |
| `Divider` | Widget |
| `OpenLink` | Action |
| `Navigation` | Action |

Only the `updateCard` method is supported for Navigation.

## Complete example: Support case add-on

The following example features a Google Workspace add-on that previews links to a company's support cases in Google Docs.

The example does the following:

- Previews links to support cases, such as `https://www.example.com/support/cases/1234`. The smart chip displays a support icon, and the preview card includes the case ID and a description.
- If the user's locale is set to Spanish, the smart chip localizes its `labelText` into Spanish.

### Manifest

### Apps Script

```json
{
  "timeZone": "America/New_York",
  "exceptionLogging": "STACKDRIVER",
  "runtimeVersion": "V8",
  "oauthScopes": [
    "https://www.googleapis.com/auth/workspace.linkpreview",
    "https://www.googleapis.com/auth/workspace.linkcreate"
  ],
  "addOns": {
    "common": {
      "name": "Manage support cases",
      "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png",
      "layoutProperties": {
        "primaryColor": "#dd4b39"
      }
    },
    "docs": {
      "linkPreviewTriggers": [
        {
          "runFunction": "caseLinkPreview",
          "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "support/cases"
            },
            {
              "hostPattern": "*.example.com",
              "pathPrefix": "cases"
            },
            {
              "hostPattern": "cases.example.com"
            }
          ],
          "labelText": "Support case",
          "localizedLabelText": {
            "es": "Caso de soporte"
          },
          "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
        }
      ],
      "createActionTriggers": [
        {
          "id": "createCase",
          "labelText": "Create support case",
          "localizedLabelText": {
            "es": "Crear caso de soporte"
          },
          "runFunction": "createCaseInputCard",
          "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
        }
      ]
    }
  }
}
```

### JSON

**Note:** To use the following manifest, replace the `URL` value with the URL of the deployed function. You can deploy the function using the code sample.

```json
{
  "oauthScopes": [
    "https://www.googleapis.com/auth/workspace.linkpreview"
  ],
  "addOns": {
    "common": {
      "name": "Preview support cases",
      "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png",
      "layoutProperties": {
        "primaryColor": "#dd4b39"
      }
    },
    "docs": {
      "linkPreviewTriggers": [
        {
          "runFunction": "URL",
          "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "support/cases"
            },
            {
              "hostPattern": "*.example.com",
              "pathPrefix": "cases"
            },
            {
              "hostPattern": "cases.example.com"
            }
          ],
          "labelText": "Support case",
          "localizedLabelText": {
            "es": "Caso de soporte"
          },
          "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
        }
      ]
    }
  }
}
```

### Code

### Apps Script

```javascript
/**
* Entry point for a support case link preview.
*
* @param {!Object} event The event object.
* @return {!Card} The resulting preview link card.
*/
function caseLinkPreview(event) {

  // If the event object URL matches a specified pattern for support case links.
  if (event.docs.matchedUrl.url) {

    // Uses the event object to parse the URL and identify the case details.
    const caseDetails = parseQuery(event.docs.matchedUrl.url);

    // Builds a preview card with the case name, and description
    const caseHeader = CardService.newCardHeader()
      .setTitle(`Case ${caseDetails["name"][0]}`);
    const caseDescription = CardService.newTextParagraph()
      .setText(caseDetails["description"][0]);

    // Returns the card.
    // Uses the text from the card's header for the title of the smart chip.
    return CardService.newCardBuilder()
      .setHeader(caseHeader)
      .addSection(CardService.newCardSection().addWidget(caseDescription))
      .build();
  }
}

/**
* Extracts the URL parameters from the given URL.
*
* @param {!string} url The URL to parse.
* @return {!Map} A map with the extracted URL parameters.
*/
function parseQuery(url) {
  const query = url.split("?")[1];
  if (query) {
    return query.split("&")
    .reduce(function(o, e) {
      var temp = e.split("=");
      var key = temp[0].trim();
      var value = temp[1].trim();
      value = isNaN(value) ? value : Number(value);
      if (o[key]) {
        o[key].push(value);
      } else {
        o[key] = [value];
      }
      return o;
    }, {});
  }
  return null;
}
```

### Node.js

```javascript
/**
 * Responds to any HTTP request related to link previews.
 *
 * @param {Object} req An HTTP request context.
 * @param {Object} res An HTTP response context.
 */
exports.createLinkPreview = (req, res) => {
  const event = req.body;
  if (event.docs.matchedUrl.url) {
    const url = event.docs.matchedUrl.url;
    const parsedUrl = new URL(url);
    // If the event object URL matches a specified pattern for preview links.
    if (parsedUrl.hostname === 'example.com') {
      if (parsedUrl.pathname.startsWith('/support/cases/')) {
        return res.json(caseLinkPreview(parsedUrl));
      }
    }
  }
};

/**
 * 
 * A support case link preview.
 *
 * @param {!URL} url The event object.
 * @return {!Card} The resulting preview link card.
 */
function caseLinkPreview(url) {
  // Builds a preview card with the case name, and description
  // Uses the text from the card's header for the title of the smart chip.
  // Parses the URL and identify the case details.
  const name = `Case ${url.searchParams.get("name")}`;
  return {
    action: {
      linkPreview: {
        title: name,
        previewCard: {
          header: {
            title: name
          },
          sections: [{
            widgets: [{
              textParagraph: {
                text: url.searchParams.get("description")
              }
            }]
          }]
        }
      }
    }
  };
}
```

### Python

```python
from typing import Any, Mapping
from urllib.parse import urlparse, parse_qs

import flask
import functions_framework

@functions_framework.http
def create_link_preview(req: flask.Request):
    """Responds to any HTTP request related to link previews.
    Args:
      req: An HTTP request context.
    Returns:
      An HTTP response context.
    """
    event = req.get_json(silent=True)
    if event["docs"]["matchedUrl"]["url"]:
        url = event["docs"]["matchedUrl"]["url"]
        parsed_url = urlparse(url)
        # If the event object URL matches a specified pattern for preview links.
        if parsed_url.hostname == "example.com":
            if parsed_url.path.startswith("/support/cases/"):
                return case_link_preview(parsed_url)

    return {}

def case_link_preview(url):
    """A support case link preview.
    Args:
      url: A matching URL.
    Returns:
      The resulting preview link card.
    """

    # Parses the URL and identify the case details.
    query_string = parse_qs(url.query)
    name = f'Case {query_string["name"][0]}'
    # Uses the text from the card's header for the title of the smart chip.
    return {
        "action": {
            "linkPreview": {
                "title": name,
                "previewCard": {
                    "header": {
                        "title": name
                    },
                    "sections": [{
                        "widgets": [{
                            "textParagraph": {
                                "text": query_string["description"][0]
                            }
                        }]
                    }],
                }
            }
        }
    }
```

### Java

```java
import com.google.cloud.functions.HttpFunction;
import com.google.cloud.functions.HttpRequest;
import com.google.cloud.functions.HttpResponse;
import com.google.gson.Gson;
import com.google.gson.JsonArray;
import com.google.gson.JsonObject;
import com.google.gson.JsonPrimitive;

import java.io.UnsupportedEncodingException;
import java.net.URL;
import java.net.URLDecoder;
import java.util.HashMap;
import java.util.Map;

public class CreateLinkPreview implements HttpFunction {
  private static final Gson gson = new Gson();

  /**
   * Responds to any HTTP request related to link previews.
   *
   * @param request An HTTP request context.
   * @param response An HTTP response context.
   */
  @Override
  public void service(HttpRequest request, HttpResponse response) throws Exception {
    JsonObject event = gson.fromJson(request.getReader(), JsonObject.class);
    String url = event.getAsJsonObject("docs")
        .getAsJsonObject("matchedUrl")
        .get("url")
        .getAsString();
    URL parsedURL = new URL(url);
    // If the event object URL matches a specified pattern for preview links.
    if ("example.com".equals(parsedURL.getHost())) {
      if (parsedURL.getPath().startsWith("/support/cases/")) {
        response.getWriter().write(gson.toJson(caseLinkPreview(parsedURL)));
        return;
      }
    }

    response.getWriter().write("{}");
  }

  /**
   * A support case link preview.
   *
   * @param url A matching URL.
   * @return The resulting preview link card.
   */
  JsonObject caseLinkPreview(URL url) throws UnsupportedEncodingException {
    // Parses the URL and identify the case details.
    Map<String, String> caseDetails = new HashMap<String, String>();
    for (String pair : url.getQuery().split("&")) {
        caseDetails.put(URLDecoder.decode(pair.split("=")[0], "UTF-8"), URLDecoder.decode(pair.split("=")[1], "UTF-8"));
    }

    // Builds a preview card with the case name, and description
    // Uses the text from the card's header for the title of the smart chip.
    JsonObject cardHeader = new JsonObject();
    String caseName = String.format("Case %s", caseDetails.get("name"));
    cardHeader.add("title", new JsonPrimitive(caseName));

    JsonObject textParagraph = new JsonObject();
    textParagraph.add("text", new JsonPrimitive(caseDetails.get("description")));

    JsonObject widget = new JsonObject();
    widget.add("textParagraph", textParagraph);

    JsonArray widgets = new JsonArray();
    widgets.add(widget);

    JsonObject section = new JsonObject();
    section.add("widgets", widgets);

    JsonArray sections = new JsonArray();
    sections.add(section);

    JsonObject previewCard = new JsonObject();
    previewCard.add("header", cardHeader);
    previewCard.add("sections", sections);

    JsonObject linkPreview = new JsonObject();
    linkPreview.add("title", new JsonPrimitive(caseName));
    linkPreview.add("previewCard", previewCard);

    JsonObject action = new JsonObject();
    action.add("linkPreview", linkPreview);

    JsonObject renderActions = new JsonObject();
    renderActions.add("action", action);

    return renderActions;
  }
}
```

## Related resources

- Preview links from Google Books with smart chips
- Test your add-on
- Google Docs manifest
- Card interfaces for link previews
