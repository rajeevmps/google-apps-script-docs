# Create third-party resources from the @ menu

This guide explains how to build a Google Workspace add-on that lets Google Docs users create resources, such as a support case or project task, in a third-party service from within Google Docs.

With a Google Workspace add-on, you can add your service to the @ menu in Docs. The add-on adds menu items that let users create resources in your service through a form dialog in Docs.

## How users create resources

To create a resource in your service from within a Google Docs document, users type `@` in a document and select your service from the @ menu.

When users type `@` in a document and select your service, you present them with a card that includes the form inputs that users need in order to create a resource. After the user submits the resource creation form, your add-on should create the resource in your service and generate a URL that points to it.

The add-on inserts a chip into the document for the created resource. When users hold the pointer over this chip, it invokes the add-on's associated link preview trigger. Make sure your add-on inserts chips with link patterns that are supported by your link preview triggers.

## Prerequisites

### Apps Script

- A Google Workspace add-on that supports link previews for the link patterns of the resources that users create. To build an add-on with link previews, refer to Preview links with smart chips.

### Node.js

- A Google Workspace add-on that supports link previews for the link patterns of the resources that users create. To build an add-on with link previews, refer to Preview links with smart chips.

**Note:** The Node.js code samples are written to run as a Cloud Function.

### Python

- A Google Workspace add-on that supports link previews for the link patterns of the resources that users create. To build an add-on with link previews, refer to Preview links with smart chips.

**Note:** The Python code samples in this guide are written to run as a Cloud Function using Python 3.9.

### Java

- A Google Workspace add-on that supports link previews for the link patterns of the resources that users create. To build an add-on with link previews, refer to Preview links with smart chips.

## Set up resource creation for your add-on

This section explains how to set up resource creation for your add-on, which includes the following steps:

1. Configure resource creation in your add-on's manifest.
2. Build the form cards that users need to create resources within your service.
3. Handle form submissions so that the function that creates the resource runs when users submit the form.

### Configure resource creation

To configure resource creation, specify the following sections and fields in your add-on's manifest:

1. Under the `addOns` section in the `docs` field, implement the `createActionTriggers` trigger that includes a `runFunction`. (You define this function in the following section, Build the form cards.)

To learn about what fields you can specify in the `createActionTriggers` trigger, see the reference documentation for Apps Script manifests or deployment resources for other runtimes.

2. In the `oauthScopes` field, add the scope `https://www.googleapis.com/auth/workspace.linkcreate` so that users can authorize the add-on to create resources. Specifically, this scope allows the add-on to read the information that users submit to the resource creation form and insert a smart chip into the document based on that information.

**Note:** If you add this scope to a published add-on, existing users are prompted to reauthorize the add-on to allow the added scope.

As an example, see the `addons` section of a manifest that configures resource creation for the following support case service:

```json
{
      "oauthScopes": [
        "https://www.googleapis.com/auth/workspace.linkpreview",
        "https://www.googleapis.com/auth/workspace.linkcreate"
      ],
      "addOns": {
        "docs": {
          "linkPreviewTriggers": [
            ...
          ],
          "createActionTriggers": [
            {
              "id": "createCase",
              "labelText": "Create support case",
              "localizedLabelText": {
                "es": "Crear caso de soporte"
              },
              "runFunction": "createCaseInputCard",
              "logoUrl": "https://www.example.com/images/case.png"
            }
          ]
        }
      }
    }
```

In the example, the Google Workspace add-on lets users create support cases. Each `createActionTriggers` trigger must have the following fields:

- A unique ID
- A text label that appears in the Docs @ menu
- A logo URL pointing to an icon that appears next to the label text in the @ menu
- A callback function that references either an Apps Script function or an HTTP endpoint that returns a card

### Build the form cards

To create resources in your service from the Docs @ menu, you must implement any functions that you specified in the `createActionTriggers` object.

When a user interacts with one of your menu items, the corresponding `createActionTriggers` trigger fires and its callback function presents a card with form inputs for creating the resource.

#### Supported elements and actions

To create the card interface, you use widgets to display information and inputs that users need in order to create the resource. Most Google Workspace add-on widgets and actions are supported with the following exceptions:

- Card footers aren't supported.
- Notifications aren't supported.
- For navigations, only the `updateCard` navigation is supported.

#### Example of card with form inputs

The following example shows an Apps Script callback function that displays a card when a user selects **Create support case** from the @ menu:

The `createCaseInputCard` function renders a card that includes text inputs, a drop-down menu, and a checkbox. It also has a text button with an `onClick` action that runs another function to handle the submission of the creation form.

After the user fills out the form and clicks **Create**, the add-on sends the form inputs to the `onClick` action function–called `submitCaseCreationForm` in the example–at which point the add-on can validate the inputs and use them to create the resource in the third-party service.

##### Apps Script

```javascript
/**
 * Produces a support case creation form card.
 * 
 * @param {!Object} event The event object.
 * @param {!Object=} errors An optional map of per-field error messages.
 * @param {boolean} isUpdate Whether to return the form as an update card navigation.
 * @return {!Card|!ActionResponse} The resulting card or action response.
 */
function createCaseInputCard(event, errors, isUpdate) {

  const cardHeader = CardService.newCardHeader()
    .setTitle('Create a support case')

  const cardSectionTextInput1 = CardService.newTextInput()
    .setFieldName('name')
    .setTitle('Name')
    .setMultiline(false);

  const cardSectionTextInput2 = CardService.newTextInput()
    .setFieldName('description')
    .setTitle('Description')
    .setMultiline(true);

  const cardSectionSelectionInput1 = CardService.newSelectionInput()
    .setFieldName('priority')
    .setTitle('Priority')
    .setType(CardService.SelectionInputType.DROPDOWN)
    .addItem('P0', 'P0', false)
    .addItem('P1', 'P1', false)
    .addItem('P2', 'P2', false)
    .addItem('P3', 'P3', false);

  const cardSectionSelectionInput2 = CardService.newSelectionInput()
    .setFieldName('impact')
    .setTitle('Impact')
    .setType(CardService.SelectionInputType.CHECK_BOX)
    .addItem('Blocks a critical customer operation', 'Blocks a critical customer operation', false);

  const cardSectionButtonListButtonAction = CardService.newAction()
    .setPersistValues(true)
    .setFunctionName('submitCaseCreationForm')
    .setParameters({});

  const cardSectionButtonListButton = CardService.newTextButton()
    .setText('Create')
    .setTextButtonStyle(CardService.TextButtonStyle.TEXT)
    .setOnClickAction(cardSectionButtonListButtonAction);

  const cardSectionButtonList = CardService.newButtonSet()
    .addButton(cardSectionButtonListButton);

  // Builds the form inputs with error texts for invalid values.
  const cardSection = CardService.newCardSection();
  if (errors?.name) {
    cardSection.addWidget(createErrorTextParagraph(errors.name));
  }
  cardSection.addWidget(cardSectionTextInput1);
  if (errors?.description) {
    cardSection.addWidget(createErrorTextParagraph(errors.description));
  }
  cardSection.addWidget(cardSectionTextInput2);
  if (errors?.priority) {
    cardSection.addWidget(createErrorTextParagraph(errors.priority));
  }
  cardSection.addWidget(cardSectionSelectionInput1);
  if (errors?.impact) {
    cardSection.addWidget(createErrorTextParagraph(errors.impact));
  }

  cardSection.addWidget(cardSectionSelectionInput2);
  cardSection.addWidget(cardSectionButtonList);

  const card = CardService.newCardBuilder()
    .setHeader(cardHeader)
    .addSection(cardSection)
    .build();

  if (isUpdate) {
    return CardService.newActionResponseBuilder()
      .setNavigation(CardService.newNavigation().updateCard(card))
      .build();
  } else {
    return card;
  }
}
```

##### Node.js

```javascript
/**
 * Produces a support case creation form card.
 * 
 * @param {!Object} event The event object.
 * @param {!Object=} errors An optional map of per-field error messages.
 * @param {boolean} isUpdate Whether to return the form as an update card navigation.
 * @return {!Card|!ActionResponse} The resulting card or action response.
 */
function createCaseInputCard(event, errors, isUpdate) {

  const cardHeader1 = {
    title: "Create a support case"
  };

  const cardSection1TextInput1 = {
    textInput: {
      name: "name",
      label: "Name"
    }
  };

  const cardSection1TextInput2 = {
    textInput: {
      name: "description",
      label: "Description",
      type: "MULTIPLE_LINE"
    }
  };

  const cardSection1SelectionInput1 = {
    selectionInput: {
      name: "priority",
      label: "Priority",
      type: "DROPDOWN",
      items: [{
        text: "P0",
        value: "P0"
      }, {
        text: "P1",
        value: "P1"
      }, {
        text: "P2",
        value: "P2"
      }, {
        text: "P3",
        value: "P3"
      }]
    }
  };

  const cardSection1SelectionInput2 = {
    selectionInput: {
      name: "impact",
      label: "Impact",
      items: [{
        text: "Blocks a critical customer operation",
        value: "Blocks a critical customer operation"
      }]
    }
  };

  const cardSection1ButtonList1Button1Action1 = {
    function: process.env.URL,
    parameters: [
      {
        key: "submitCaseCreationForm",
        value: true
      }
    ],
    persistValues: true
  };

  const cardSection1ButtonList1Button1 = {
    text: "Create",
    onClick: {
      action: cardSection1ButtonList1Button1Action1
    }
  };

  const cardSection1ButtonList1 = {
    buttonList: {
      buttons: [cardSection1ButtonList1Button1]
    }
  };

  // Builds the creation form and adds error text for invalid inputs.
  const cardSection1 = [];
  if (errors?.name) {
    cardSection1.push(createErrorTextParagraph(errors.name));
  }
  cardSection1.push(cardSection1TextInput1);
  if (errors?.description) {
    cardSection1.push(createErrorTextParagraph(errors.description));
  }
  cardSection1.push(cardSection1TextInput2);
  if (errors?.priority) {
    cardSection1.push(createErrorTextParagraph(errors.priority));
  }
  cardSection1.push(cardSection1SelectionInput1);
  if (errors?.impact) {
    cardSection1.push(createErrorTextParagraph(errors.impact));
  }

  cardSection1.push(cardSection1SelectionInput2);
  cardSection1.push(cardSection1ButtonList1);

  const card = {
    header: cardHeader1,
    sections: [{
      widgets: cardSection1
    }]
  };

  if (isUpdate) {
    return {
      renderActions: {
        action: {
          navigations: [{
            updateCard: card
          }]
        }
      }
    };
  } else {
    return {
      action: {
        navigations: [{
          pushCard: card
        }]
      }
    };
  }
}
```

##### Python

```python
def create_case_input_card(event, errors = {}, isUpdate = False):
    """Produces a support case creation form card.
    Args:
      event: The event object.
      errors: An optional dict of per-field error messages.
      isUpdate: Whether to return the form as an update card navigation.
    Returns:
      The resulting card or action response.
    """
    card_header1 = {
        "title": "Create a support case"
    }

    card_section1_text_input1 = {
        "textInput": {
            "name": "name",
            "label": "Name"
        }
    }

    card_section1_text_input2 = {
        "textInput": {
            "name": "description",
            "label": "Description",
            "type": "MULTIPLE_LINE"
        }
    }

    card_section1_selection_input1 = {
        "selectionInput": {
            "name": "priority",
            "label": "Priority",
            "type": "DROPDOWN",
            "items": [{
                "text": "P0",
                "value": "P0"
            }, {
                "text": "P1",
                "value": "P1"
            }, {
                "text": "P2",
                "value": "P2"
            }, {
                "text": "P3",
                "value": "P3"
            }]
        }
    }

    card_section1_selection_input2 = {
        "selectionInput": {
            "name": "impact",
            "label": "Impact",
            "items": [{
                "text": "Blocks a critical customer operation",
                "value": "Blocks a critical customer operation"
            }]
        }
    }

    card_section1_button_list1_button1_action1 = {
        "function": os.environ["URL"],
        "parameters": [
        {
            "key": "submitCaseCreationForm",
            "value": True
        }
        ],
        "persistValues": True
    }

    card_section1_button_list1_button1 = {
        "text": "Create",
        "onClick": {
            "action": card_section1_button_list1_button1_action1
        }
    }

    card_section1_button_list1 = {
        "buttonList": {
            "buttons": [card_section1_button_list1_button1]
        }
    }

    # Builds the creation form and adds error text for invalid inputs.
    card_section1 = []
    if "name" in errors:
        card_section1.append(create_error_text_paragraph(errors["name"]))
    card_section1.append(card_section1_text_input1)
    if "description" in errors:
        card_section1.append(create_error_text_paragraph(errors["description"]))
    card_section1.append(card_section1_text_input2)
    if "priority" in errors:
        card_section1.append(create_error_text_paragraph(errors["priority"]))
    card_section1.append(card_section1_selection_input1)
    if "impact" in errors:
        card_section1.append(create_error_text_paragraph(errors["impact"]))

    card_section1.append(card_section1_selection_input2)
    card_section1.append(card_section1_button_list1)

    card = {
        "header": card_header1,
        "sections": [{
            "widgets": card_section1
        }]
    }

    if isUpdate:
        return {
            "renderActions": {
                "action": {
                        "navigations": [{
                        "updateCard": card
                    }]
                }
            }
        }
    else:
        return {
            "action": {
                "navigations": [{
                    "pushCard": card
                }]
            }
        }
```

##### Java

```java
/**
 * Produces a support case creation form.
 * 
 * @param event The event object.
 * @param errors A map of per-field error messages.
 * @param isUpdate Whether to return the form as an update card navigation.
 * @return The resulting card or action response.
 */
JsonObject createCaseInputCard(JsonObject event, Map<String, String> errors, boolean isUpdate) {
  JsonObject cardHeader = new JsonObject();
  cardHeader.add("title", new JsonPrimitive("Create a support case"));

  JsonObject cardSectionTextInput1 = new JsonObject();
  cardSectionTextInput1.add("name", new JsonPrimitive("name"));
  cardSectionTextInput1.add("label", new JsonPrimitive("Name"));

  JsonObject cardSectionTextInput1Widget = new JsonObject();
  cardSectionTextInput1Widget.add("textInput", cardSectionTextInput1);

  JsonObject cardSectionTextInput2 = new JsonObject();
  cardSectionTextInput2.add("name", new JsonPrimitive("description"));
  cardSectionTextInput2.add("label", new JsonPrimitive("Description"));
  cardSectionTextInput2.add("type", new JsonPrimitive("MULTIPLE_LINE"));

  JsonObject cardSectionTextInput2Widget = new JsonObject();
  cardSectionTextInput2Widget.add("textInput", cardSectionTextInput2);

  JsonObject cardSectionSelectionInput1ItemsItem1 = new JsonObject();
  cardSectionSelectionInput1ItemsItem1.add("text", new JsonPrimitive("P0"));
  cardSectionSelectionInput1ItemsItem1.add("value", new JsonPrimitive("P0"));

  JsonObject cardSectionSelectionInput1ItemsItem2 = new JsonObject();
  cardSectionSelectionInput1ItemsItem2.add("text", new JsonPrimitive("P1"));
  cardSectionSelectionInput1ItemsItem2.add("value", new JsonPrimitive("P1"));

  JsonObject cardSectionSelectionInput1ItemsItem3 = new JsonObject();
  cardSectionSelectionInput1ItemsItem3.add("text", new JsonPrimitive("P2"));
  cardSectionSelectionInput1ItemsItem3.add("value", new JsonPrimitive("P2"));

  JsonObject cardSectionSelectionInput1ItemsItem4 = new JsonObject();
  cardSectionSelectionInput1ItemsItem4.add("text", new JsonPrimitive("P3"));
  cardSectionSelectionInput1ItemsItem4.add("value", new JsonPrimitive("P3"));

  JsonArray cardSectionSelectionInput1Items = new JsonArray();
  cardSectionSelectionInput1Items.add(cardSectionSelectionInput1ItemsItem1);
  cardSectionSelectionInput1Items.add(cardSectionSelectionInput1ItemsItem2);
  cardSectionSelectionInput1Items.add(cardSectionSelectionInput1ItemsItem3);
  cardSectionSelectionInput1Items.add(cardSectionSelectionInput1ItemsItem4);

  JsonObject cardSectionSelectionInput1 = new JsonObject();
  cardSectionSelectionInput1.add("name", new JsonPrimitive("priority"));
  cardSectionSelectionInput1.add("label", new JsonPrimitive("Priority"));
  cardSectionSelectionInput1.add("type", new JsonPrimitive("DROPDOWN"));
  cardSectionSelectionInput1.add("items", cardSectionSelectionInput1Items);

  JsonObject cardSectionSelectionInput1Widget = new JsonObject();
  cardSectionSelectionInput1Widget.add("selectionInput", cardSectionSelectionInput1);

  JsonObject cardSectionSelectionInput2ItemsItem = new JsonObject();
  cardSectionSelectionInput2ItemsItem.add("text", new JsonPrimitive("Blocks a critical customer operation"));
  cardSectionSelectionInput2ItemsItem.add("value", new JsonPrimitive("Blocks a critical customer operation"));

  JsonArray cardSectionSelectionInput2Items = new JsonArray();
  cardSectionSelectionInput2Items.add(cardSectionSelectionInput2ItemsItem);

  JsonObject cardSectionSelectionInput2 = new JsonObject();
  cardSectionSelectionInput2.add("name", new JsonPrimitive("impact"));
  cardSectionSelectionInput2.add("label", new JsonPrimitive("Impact"));
  cardSectionSelectionInput2.add("items", cardSectionSelectionInput2Items);

  JsonObject cardSectionSelectionInput2Widget = new JsonObject();
  cardSectionSelectionInput2Widget.add("selectionInput", cardSectionSelectionInput2);

  JsonObject cardSectionButtonListButtonActionParametersParameter = new JsonObject();
  cardSectionButtonListButtonActionParametersParameter.add("key", new JsonPrimitive("submitCaseCreationForm"));
  cardSectionButtonListButtonActionParametersParameter.add("value", new JsonPrimitive(true));

  JsonArray cardSectionButtonListButtonActionParameters = new JsonArray();
  cardSectionButtonListButtonActionParameters.add(cardSectionButtonListButtonActionParametersParameter);

  JsonObject cardSectionButtonListButtonAction = new JsonObject();
  cardSectionButtonListButtonAction.add("function", new JsonPrimitive(System.getenv().get("URL")));
  cardSectionButtonListButtonAction.add("parameters", cardSectionButtonListButtonActionParameters);
  cardSectionButtonListButtonAction.add("persistValues", new JsonPrimitive(true));

  JsonObject cardSectionButtonListButtonOnCLick = new JsonObject();
  cardSectionButtonListButtonOnCLick.add("action", cardSectionButtonListButtonAction);

  JsonObject cardSectionButtonListButton = new JsonObject();
  cardSectionButtonListButton.add("text", new JsonPrimitive("Create"));
  cardSectionButtonListButton.add("onClick", cardSectionButtonListButtonOnCLick);

  JsonArray cardSectionButtonListButtons = new JsonArray();
  cardSectionButtonListButtons.add(cardSectionButtonListButton);

  JsonObject cardSectionButtonList = new JsonObject();
  cardSectionButtonList.add("buttons", cardSectionButtonListButtons);

  JsonObject cardSectionButtonListWidget = new JsonObject();
  cardSectionButtonListWidget.add("buttonList", cardSectionButtonList);

  // Builds the form inputs with error texts for invalid values.
  JsonArray cardSection = new JsonArray();
  if (errors.containsKey("name")) {
    cardSection.add(createErrorTextParagraph(errors.get("name").toString()));
  }
  cardSection.add(cardSectionTextInput1Widget);
  if (errors.containsKey("description")) {
    cardSection.add(createErrorTextParagraph(errors.get("description").toString()));
  }
  cardSection.add(cardSectionTextInput2Widget);
  if (errors.containsKey("priority")) {
    cardSection.add(createErrorTextParagraph(errors.get("priority").toString()));
  }
  cardSection.add(cardSectionSelectionInput1Widget);
  if (errors.containsKey("impact")) {
    cardSection.add(createErrorTextParagraph(errors.get("impact").toString()));
  }

  cardSection.add(cardSectionSelectionInput2Widget);
  cardSection.add(cardSectionButtonListWidget);

  JsonObject cardSectionWidgets = new JsonObject();
  cardSectionWidgets.add("widgets", cardSection);

  JsonArray sections = new JsonArray();
  sections.add(cardSectionWidgets);

  JsonObject card = new JsonObject();
  card.add("header", cardHeader);
  card.add("sections", sections);

  JsonObject navigation = new JsonObject();
  if (isUpdate) {
    navigation.add("updateCard", card);
  } else {
    navigation.add("pushCard", card);
  }

  JsonArray navigations = new JsonArray();
  navigations.add(navigation);

  JsonObject action = new JsonObject();
  action.add("navigations", navigations);

  JsonObject renderActions = new JsonObject();
  renderActions.add("action", action);

  if (!isUpdate) {
    return renderActions;
  }

  JsonObject update = new JsonObject();
  update.add("renderActions", renderActions);

  return update;
}
```

### Handle form submissions

After a user submits the creation form, the function associated with the `onClick` action runs. For an ideal user experience, your add-on should handle both successful and erroneous form submissions.

#### Handle successful resource creation

The `onClick` function of your add-on should create the resource in your third-party service and generate a URL that points to it.

In order to communicate the resource's URL back to Docs for chip creation, the `onClick` function should return a `SubmitFormResponse` with a one-element array in `renderActions.action.links` that points to a link. The link title should represent the title of the created resource and the URL should point to that resource.

The following example shows a `SubmitFormResponse` for a created resource:

##### Apps Script

```javascript
/**
 * Returns a submit form response that inserts a link into the document.
 * 
 * @param {string} title The title of the link to insert.
 * @param {string} url The URL of the link to insert.
 * @return {!SubmitFormResponse} The resulting submit form response.
 */
function createLinkRenderAction(title, url) {
  return {
    renderActions: {
      action: {
        links: [{
          title: title,
          url: url
        }]
      }
    }
  };
}
```

##### Node.js

```javascript
/**
 * Returns a submit form response that inserts a link into the document.
 * 
 * @param {string} title The title of the link to insert.
 * @param {string} url The URL of the link to insert.
 * @return {!SubmitFormResponse} The resulting submit form response.
 */
function createLinkRenderAction(title, url) {
  return {
    renderActions: {
      action: {
        links: [{
          title: title,
          url: url
        }]
      }
    }
  };
}
```

##### Python

```python
def create_link_render_action(title, url):
    """Returns a submit form response that inserts a link into the document.
    Args:
      title: The title of the link to insert.
      url: The URL of the link to insert.
    Returns:
      The resulting submit form response.
    """
    return {
        "renderActions": {
            "action": {
                "links": [{
                    "title": title,
                    "url": url
                }]
            }
        }
    }
```

##### Java

```java
/**
 * Returns a submit form response that inserts a link into the document.
 * 
 * @param title The title of the link to insert.
 * @param url The URL of the link to insert.
 * @return The resulting submit form response.
 */
JsonObject createLinkRenderAction(String title, String url) {
  JsonObject link = new JsonObject();
  link.add("title", new JsonPrimitive(title));
  link.add("url", new JsonPrimitive(url));

  JsonArray links = new JsonArray();
  links.add(link);

  JsonObject action = new JsonObject();
  action.add("links", links);

  JsonObject renderActions = new JsonObject();
  renderActions.add("action", action);

  JsonObject linkRenderAction = new JsonObject();
  linkRenderAction.add("renderActions", renderActions);

  return linkRenderAction;
}
```

After the `SubmitFormResponse` is returned, the modal dialog closes and the add-on inserts a chip into the document. When users hold the pointer over this chip, it invokes the associated link preview trigger. Make sure your add-on doesn't insert chips with link patterns not supported by your link preview triggers.

#### Handle errors

If a user tries to submit a form with invalid fields, instead of returning a `SubmitFormResponse` with a link, the add-on should return a render action that displays an error using an `updateCard` navigation. This lets the user see what they did wrong and try again. See `updateCard(card)` for Apps Script and `updateCard` for other runtimes. Notifications and `pushCard` navigations aren't supported.

##### Example of error handling

The following example shows the code that's invoked when a user submits the form. If the inputs are invalid, the card updates and shows error messages. If the inputs are valid, the add-on returns a `SubmitFormResponse` with a link to the created resource.

###### Apps Script

```javascript
/**
 * Submits the creation form. If valid, returns a render action
 * that inserts a new link into the document. If invalid, returns an
 * update card navigation that re-renders the creation form with error messages.
 * 
 * @param {!Object} event The event object with form input values.
 * @return {!ActionResponse|!SubmitFormResponse} The resulting response.
 */
function submitCaseCreationForm(event) {
  const caseDetails = {
    name: event.formInput.name,
    description: event.formInput.description,
    priority: event.formInput.priority,
    impact: !!event.formInput.impact,
  };

  const errors = validateFormInputs(caseDetails);
  if (Object.keys(errors).length > 0) {
    return createCaseInputCard(event, errors, /* isUpdate= */ true);
  } else {
    const title = `Case ${caseDetails.name}`;
    // Adds the case details as parameters to the generated link URL.
    const url = 'https://example.com/support/cases/?' + generateQuery(caseDetails);
    return createLinkRenderAction(title, url);
  }
}

/**
* Build a query path with URL parameters.
*
* @param {!Map} parameters A map with the URL parameters.
* @return {!string} The resulting query path.
*/
function generateQuery(parameters) {
  return Object.entries(parameters).flatMap(([k, v]) =>
    Array.isArray(v) ? v.map(e => `${k}=${encodeURIComponent(e)}`) : `${k}=${encodeURIComponent(v)}`
  ).join("&");
}
```

```javascript
/**
 * Validates case creation form input values.
 * 
 * @param {!Object} caseDetails The values of each form input submitted by the user.
 * @return {!Object} A map from field name to error message. An empty object
 *     represents a valid form submission.
 */
function validateFormInputs(caseDetails) {
  const errors = {};
  if (!caseDetails.name) {
    errors.name = 'You must provide a name';
  }
  if (!caseDetails.description) {
    errors.description = 'You must provide a description';
  }
  if (!caseDetails.priority) {
    errors.priority = 'You must provide a priority';
  }
  if (caseDetails.impact && caseDetails.priority !== 'P0' && caseDetails.priority !== 'P1') {
    errors.impact = 'If an issue blocks a critical customer operation, priority must be P0 or P1';
  }

  return errors;
}

/**
 * Returns a text paragraph with red text indicating a form field validation error.
 * 
 * @param {string} errorMessage A description of input value error.
 * @return {!TextParagraph} The resulting text paragraph.
 */
function createErrorTextParagraph(errorMessage) {
  return CardService.newTextParagraph()
    .setText('<font color=\\"#BA0300\\"><b>Error:</b> ' + errorMessage + '</font>');
}
```

###### Node.js

```javascript
/**
 * Submits the creation form. If valid, returns a render action
 * that inserts a new link into the document. If invalid, returns an
 * update card navigation that re-renders the creation form with error messages.
 * 
 * @param {!Object} event The event object with form input values.
 * @return {!ActionResponse|!SubmitFormResponse} The resulting response.
 */
function submitCaseCreationForm(event) {
  const caseDetails = {
    name: event.commonEventObject.formInputs?.name?.stringInputs?.value[0],
    description: event.commonEventObject.formInputs?.description?.stringInputs?.value[0],
    priority: event.commonEventObject.formInputs?.priority?.stringInputs?.value[0],
    impact: !!event.commonEventObject.formInputs?.impact?.stringInputs?.value[0],
  };

  const errors = validateFormInputs(caseDetails);
  if (Object.keys(errors).length > 0) {
    return createCaseInputCard(event, errors, /* isUpdate= */ true);
  } else {
    const title = `Case ${caseDetails.name}`;
    // Adds the case details as parameters to the generated link URL.
    const url = new URL('https://example.com/support/cases/');
    for (const [key, value] of Object.entries(caseDetails)) {
      url.searchParams.append(key, value);
    }
    return createLinkRenderAction(title, url.href);
  }
}
```

```javascript
/**
 * Validates case creation form input values.
 * 
 * @param {!Object} caseDetails The values of each form input submitted by the user.
 * @return {!Object} A map from field name to error message. An empty object
 *     represents a valid form submission.
 */
function validateFormInputs(caseDetails) {
  const errors = {};
  if (caseDetails.name === undefined) {
    errors.name = 'You must provide a name';
  }
  if (caseDetails.description === undefined) {
    errors.description = 'You must provide a description';
  }
  if (caseDetails.priority === undefined) {
    errors.priority = 'You must provide a priority';
  }
  if (caseDetails.impact && !(['P0', 'P1']).includes(caseDetails.priority)) {
    errors.impact = 'If an issue blocks a critical customer operation, priority must be P0 or P1';
  }

  return errors;
}

/**
 * Returns a text paragraph with red text indicating a form field validation error.
 * 
 * @param {string} errorMessage A description of input value error.
 * @return {!TextParagraph} The resulting text paragraph.
 */
function createErrorTextParagraph(errorMessage) {
  return {
    textParagraph: {
      text: '<font color=\\"#BA0300\\"><b>Error:</b> ' + errorMessage + '</font>'
    }
  }
}
```

###### Python

```python
def submit_case_creation_form(event):
    """Submits the creation form.

    If valid, returns a render action that inserts a new link
    into the document. If invalid, returns an update card navigation that
    re-renders the creation form with error messages.
    Args:
      event: The event object with form input values.
    Returns:
      The resulting response.
    """
    formInputs = event["commonEventObject"]["formInputs"] if "formInputs" in event["commonEventObject"] else None
    case_details = {
        "name":  None,
        "description": None,
        "priority": None,
        "impact": None,
    }
    if formInputs is not None:
        case_details["name"] = formInputs["name"]["stringInputs"]["value"][0] if "name" in formInputs else None
        case_details["description"] = formInputs["description"]["stringInputs"]["value"][0] if "description" in formInputs else None
        case_details["priority"] = formInputs["priority"]["stringInputs"]["value"][0] if "priority" in formInputs else None
        case_details["impact"] = formInputs["impact"]["stringInputs"]["value"][0] if "impact" in formInputs else False

    errors = validate_form_inputs(case_details)
    if len(errors) > 0:
        return create_case_input_card(event, errors, True) # Update mode
    else:
        title = f'Case {case_details["name"]}'
        # Adds the case details as parameters to the generated link URL.
        url = "https://example.com/support/cases/?" + urlencode(case_details)
        return create_link_render_action(title, url)
```

```python
def validate_form_inputs(case_details):
    """Validates case creation form input values.
    Args:
      case_details: The values of each form input submitted by the user.
    Returns:
      A dict from field name to error message. An empty object represents a valid form submission.
    """
    errors = {}
    if case_details["name"] is None:
        errors["name"] = "You must provide a name"
    if case_details["description"] is None:
        errors["description"] = "You must provide a description"
    if case_details["priority"] is None:
        errors["priority"] = "You must provide a priority"
    if case_details["impact"] is not None and case_details["priority"] not in ['P0', 'P1']:
        errors["impact"] = "If an issue blocks a critical customer operation, priority must be P0 or P1"
    return errors

def create_error_text_paragraph(error_message):
    """Returns a text paragraph with red text indicating a form field validation error.
    Args:
      error_essage: A description of input value error.
    Returns:
      The resulting text paragraph.
    """
    return {
        "textParagraph": {
            "text": '<font color=\\"#BA0300\\"\><b>Error:</b> ' + error_message + '</font>'
        }
    }
```

###### Java

```java
/**
 * Submits the creation form. If valid, returns a render action
 * that inserts a new link into the document. If invalid, returns an
 * update card navigation that re-renders the creation form with error messages.
 * 
 * @param event The event object with form input values.
 * @return The resulting response.
 */
JsonObject submitCaseCreationForm(JsonObject event) throws Exception {
  JsonObject formInputs = event.getAsJsonObject("commonEventObject").getAsJsonObject("formInputs");
  Map<String, String> caseDetails = new HashMap<String, String>();
  if (formInputs != null) {
    if (formInputs.has("name")) {
      caseDetails.put("name", formInputs.getAsJsonObject("name").getAsJsonObject("stringInputs").getAsJsonArray("value").get(0).getAsString());
    }
    if (formInputs.has("description")) {
      caseDetails.put("description", formInputs.getAsJsonObject("description").getAsJsonObject("stringInputs").getAsJsonArray("value").get(0).getAsString());
    }
    if (formInputs.has("priority")) {
      caseDetails.put("priority", formInputs.getAsJsonObject("priority").getAsJsonObject("stringInputs").getAsJsonArray("value").get(0).getAsString());
    }
    if (formInputs.has("impact")) {
      caseDetails.put("impact", formInputs.getAsJsonObject("impact").getAsJsonObject("stringInputs").getAsJsonArray("value").get(0).getAsString());
    }
  }

  Map<String, String> errors = validateFormInputs(caseDetails);
  if (errors.size() > 0) {
    return createCaseInputCard(event, errors, /* isUpdate= */ true);
  } else {
    String title = String.format("Case %s", caseDetails.get("name"));
    // Adds the case details as parameters to the generated link URL.
    URIBuilder uriBuilder = new URIBuilder("https://example.com/support/cases/");
    for (String caseDetailKey : caseDetails.keySet()) {
      uriBuilder.addParameter(caseDetailKey, caseDetails.get(caseDetailKey));
    }
    return createLinkRenderAction(title, uriBuilder.build().toURL().toString());
  }
}
```

```java
/**
 * Validates case creation form input values.
 * 
 * @param caseDetails The values of each form input submitted by the user.
 * @return A map from field name to error message. An empty object
 *     represents a valid form submission.
 */
Map<String, String> validateFormInputs(Map<String, String> caseDetails) {
  Map<String, String> errors = new HashMap<String, String>();
  if (!caseDetails.containsKey("name")) {
    errors.put("name", "You must provide a name");
  }
  if (!caseDetails.containsKey("description")) {
    errors.put("description", "You must provide a description");
  }
  if (!caseDetails.containsKey("priority")) {
    errors.put("priority", "You must provide a priority");
  }
  if (caseDetails.containsKey("impact") && !Arrays.asList(new String[]{"P0", "P1"}).contains(caseDetails.get("priority"))) {
    errors.put("impact", "If an issue blocks a critical customer operation, priority must be P0 or P1");
  }

  return errors;
}

/**
 * Returns a text paragraph with red text indicating a form field validation error.
 * 
 * @param errorMessage A description of input value error.
 * @return The resulting text paragraph.
 */
JsonObject createErrorTextParagraph(String errorMessage) {
  JsonObject textParagraph = new JsonObject();
  textParagraph.add("text", new JsonPrimitive("<font color=\\"#BA0300\\"><b>Error:</b> " + errorMessage + "</font>"));

  JsonObject textParagraphWidget = new JsonObject();
  textParagraphWidget.add("textParagraph", textParagraph);

  return textParagraphWidget;
}
```

## Complete example: Support case add-on

The following example shows a Google Workspace add-on that previews links to a company's support cases and lets users create support cases from within Google Docs.

The example does the following:

- Generates a card with form fields to create a support case from the Docs @ menu.
- Validates form inputs and returns error messages for invalid inputs.
- Inserts the created support case's name and link into the Docs document as a smart chip.
- Previews the link to the support case, such as `https://www.example.com/support/cases/1234`. The smart chip displays an icon, and the preview card includes the case name, priority, and description.

### Manifest

#### Apps Script

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

#### JSON

**Note:** To use the following manifest, replace the `$URL1` and `$URL2` values with the URLs of the deployed functions.

```json
{
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
          "runFunction": "$URL1",
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
          "runFunction": "$URL2",
          "logoUrl": "https://developers.google.com/workspace/add-ons/images/support-icon.png"
        }
      ]
    }
  }
}
```

### Code

#### Apps Script

```javascript
/**
 * Copyright 2024 Google LLC
 * 
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 * 
 *     https://www.apache.org/licenses/LICENSE-2.0
 * 
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

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

/**
 * Produces a support case creation form card.
 * 
 * @param {!Object} event The event object.
 * @param {!Object=} errors An optional map of per-field error messages.
 * @param {boolean} isUpdate Whether to return the form as an update card navigation.
 * @return {!Card|!ActionResponse} The resulting card or action response.
 */
function createCaseInputCard(event, errors, isUpdate) {

  const cardHeader = CardService.newCardHeader()
    .setTitle('Create a support case')

  const cardSectionTextInput1 = CardService.newTextInput()
    .setFieldName('name')
    .setTitle('Name')
    .setMultiline(false);

  const cardSectionTextInput2 = CardService.newTextInput()
    .setFieldName('description')
    .setTitle('Description')
    .setMultiline(true);

  const cardSectionSelectionInput1 = CardService.newSelectionInput()
    .setFieldName('priority')
    .setTitle('Priority')
    .setType(CardService.SelectionInputType.DROPDOWN)
    .addItem('P0', 'P0', false)
    .addItem('P1', 'P1', false)
    .addItem('P2', 'P2', false)
    .addItem('P3', 'P3', false);

  const cardSectionSelectionInput2 = CardService.newSelectionInput()
    .setFieldName('impact')
    .setTitle('Impact')
    .setType(CardService.SelectionInputType.CHECK_BOX)
    .addItem('Blocks a critical customer operation', 'Blocks a critical customer operation', false);

  const cardSectionButtonListButtonAction = CardService.newAction()
    .setPersistValues(true)
    .setFunctionName('submitCaseCreationForm')
    .setParameters({});

  const cardSectionButtonListButton = CardService.newTextButton()
    .setText('Create')
    .setTextButtonStyle(CardService.TextButtonStyle.TEXT)
    .setOnClickAction(cardSectionButtonListButtonAction);

  const cardSectionButtonList = CardService.newButtonSet()
    .addButton(cardSectionButtonListButton);

  // Builds the form inputs with error texts for invalid values.
  const cardSection = CardService.newCardSection();
  if (errors?.name) {
    cardSection.addWidget(createErrorTextParagraph(errors.name));
  }
  cardSection.addWidget(cardSectionTextInput1);
  if (errors?.description) {
    cardSection.addWidget(createErrorTextParagraph(errors.description));
  }
  cardSection.addWidget(cardSectionTextInput2);
  if (errors?.priority) {
    cardSection.addWidget(createErrorTextParagraph(errors.priority));
  }
  cardSection.addWidget(cardSectionSelectionInput1);
  if (errors?.impact) {
    cardSection.addWidget(createErrorTextParagraph(errors.impact));
  }

  cardSection.addWidget(cardSectionSelectionInput2);
  cardSection.addWidget(cardSectionButtonList);

  const card = CardService.newCardBuilder()
    .setHeader(cardHeader)
    .addSection(cardSection)
    .build();

  if (isUpdate) {
    return CardService.newActionResponseBuilder()
      .setNavigation(CardService.newNavigation().updateCard(card))
      .build();
  } else {
    return card;
  }
}

/**
 * Submits the creation form. If valid, returns a render action
 * that inserts a new link into the document. If invalid, returns an
 * update card navigation that re-renders the creation form with error messages.
 * 
 * @param {!Object} event The event object with form input values.
 * @return {!ActionResponse|!SubmitFormResponse} The resulting response.
 */
function submitCaseCreationForm(event) {
  const caseDetails = {
    name: event.formInput.name,
    description: event.formInput.description,
    priority: event.formInput.priority,
    impact: !!event.formInput.impact,
  };

  const errors = validateFormInputs(caseDetails);
  if (Object.keys(errors).length > 0) {
    return createCaseInputCard(event, errors, /* isUpdate= */ true);
  } else {
    const title = `Case ${caseDetails.name}`;
    // Adds the case details as parameters to the generated link URL.
    const url = 'https://example.com/support/cases/?' + generateQuery(caseDetails);
    return createLinkRenderAction(title, url);
  }
}

/**
* Build a query path with URL parameters.
*
* @param {!Map} parameters A map with the URL parameters.
* @return {!string} The resulting query path.
*/
function generateQuery(parameters) {
  return Object.entries(parameters).flatMap(([k, v]) =>
    Array.isArray(v) ? v.map(e => `${k}=${encodeURIComponent(e)}`) : `${k}=${encodeURIComponent(v)}`
  ).join("&");
}

/**
 * Validates case creation form input values.
 * 
 * @param {!Object} caseDetails The values of each form input submitted by the user.
 * @return {!Object} A map from field name to error message. An empty object
 *     represents a valid form submission.
 */
function validateFormInputs(caseDetails) {
  const errors = {};
  if (!caseDetails.name) {
    errors.name = 'You must provide a name';
  }
  if (!caseDetails.description) {
    errors.description = 'You must provide a description';
  }
  if (!caseDetails.priority) {
    errors.priority = 'You must provide a priority';
  }
  if (caseDetails.impact && caseDetails.priority !== 'P0' && caseDetails.priority !== 'P1') {
    errors.impact = 'If an issue blocks a critical customer operation, priority must be P0 or P1';
  }

  return errors;
}

/**
 * Returns a text paragraph with red text indicating a form field validation error.
 * 
 * @param {string} errorMessage A description of input value error.
 * @return {!TextParagraph} The resulting text paragraph.
 */
function createErrorTextParagraph(errorMessage) {
  return CardService.newTextParagraph()
    .setText('<font color=\\"#BA0300\\"><b>Error:</b> ' + errorMessage + '</font>');
}

/**
 * Returns a submit form response that inserts a link into the document.
 * 
 * @param {string} title The title of the link to insert.
 * @param {string} url The URL of the link to insert.
 * @return {!SubmitFormResponse} The resulting submit form response.
 */
function createLinkRenderAction(title, url) {
  return {
    renderActions: {
      action: {
        links: [{
          title: title,
          url: url
        }]
      }
    }
  };
}
```

#### Node.js

```javascript
/**
 * Copyright 2024 Google LLC
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

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

/**
 * Responds to any HTTP request related to 3P resource creations.
 *
 * @param {Object} req An HTTP request context.
 * @param {Object} res An HTTP response context.
 */
exports.create3pResources = (req, res) => {
  const event = req.body;
  if (event.commonEventObject.parameters?.submitCaseCreationForm) {
    res.json(submitCaseCreationForm(event));
  } else {
    res.json(createCaseInputCard(event));
  }
};

/**
 * Produces a support case creation form card.
 * 
 * @param {!Object} event The event object.
 * @param {!Object=} errors An optional map of per-field error messages.
 * @param {boolean} isUpdate Whether to return the form as an update card navigation.
 * @return {!Card|!ActionResponse} The resulting card or action response.
 */
function createCaseInputCard(event, errors, isUpdate) {

  const cardHeader1 = {
    title: "Create a support case"
  };

  const cardSection1TextInput1 = {
    textInput: {
      name: "name",
      label: "Name"
    }
  };

  const cardSection1TextInput2 = {
    textInput: {
      name: "description",
      label: "Description",
      type: "MULTIPLE_LINE"
    }
  };

  const cardSection1SelectionInput1 = {
    selectionInput: {
      name: "priority",
      label: "Priority",
      type: "DROPDOWN",
      items: [{
        text: "P0",
        value: "P0"
      }, {
        text: "P1",
        value: "P1"
      }, {
        text: "P2",
        value: "P2"
      }, {
        text: "P3",
        value: "P3"
      }]
    }
  };

  const cardSection1SelectionInput2 = {
    selectionInput: {
      name: "impact",
      label: "Impact",
      items: [{
        text: "Blocks a critical customer operation",
        value: "Blocks a critical customer operation"
      }]
    }
  };

  const cardSection1ButtonList1Button1Action1 = {
    function: process.env.URL,
    parameters: [
      {
        key: "submitCaseCreationForm",
        value: true
      }
    ],
    persistValues: true
  };

  const cardSection1ButtonList1Button1 = {
    text: "Create",
    onClick: {
      action: cardSection1ButtonList1Button1Action1
    }
  };

  const cardSection1ButtonList1 = {
    buttonList: {
      buttons: [cardSection1ButtonList1Button1]
    }
  };

  // Builds the creation form and adds error text for invalid inputs.
  const cardSection1 = [];
  if (errors?.name) {
    cardSection1.push(createErrorTextParagraph(errors.name));
  }
  cardSection1.push(cardSection1TextInput1);
  if (errors?.description) {
    cardSection1.push(createErrorTextParagraph(errors.description));
  }
  cardSection1.push(cardSection1TextInput2);
  if (errors?.priority) {
    cardSection1.push(createErrorTextParagraph(errors.priority));
  }
  cardSection1.push(cardSection1SelectionInput1);
  if (errors?.impact) {
    cardSection1.push(createErrorTextParagraph(errors.impact));
  }

  cardSection1.push(cardSection1SelectionInput2);
  cardSection1.push(cardSection1ButtonList1);

  const card = {
    header: cardHeader1,
    sections: [{
      widgets: cardSection1
    }]
  };

  if (isUpdate) {
    return {
      renderActions: {
        action: {
          navigations: [{
            updateCard: card
          }]
        }
      }
    };
  } else {
    return {
      action: {
        navigations: [{
          pushCard: card
        }]
      }
    };
  }
}

/**
 * Submits the creation form. If valid, returns a render action
 * that inserts a new link into the document. If invalid, returns an
 * update card navigation that re-renders the creation form with error messages.
 * 
 * @param {!Object} event The event object with form input values.
 * @return {!ActionResponse|!SubmitFormResponse} The resulting response.
 */
function submitCaseCreationForm(event) {
  const caseDetails = {
    name: event.commonEventObject.formInputs?.name?.stringInputs?.value[0],
    description: event.commonEventObject.formInputs?.description?.stringInputs?.value[0],
    priority: event.commonEventObject.formInputs?.priority?.stringInputs?.value[0],
    impact: !!event.commonEventObject.formInputs?.impact?.stringInputs?.value[0],
  };

  const errors = validateFormInputs(caseDetails);
  if (Object.keys(errors).length > 0) {
    return createCaseInputCard(event, errors, /* isUpdate= */ true);
  } else {
    const title = `Case ${caseDetails.name}`;
    // Adds the case details as parameters to the generated link URL.
    const url = new URL('https://example.com/support/cases/');
    for (const [key, value] of Object.entries(caseDetails)) {
      url.searchParams.append(key, value);
    }
    return createLinkRenderAction(title, url.href);
  }
}

/**
 * Validates case creation form input values.
 * 
 * @param {!Object} caseDetails The values of each form input submitted by the user.
 * @return {!Object} A map from field name to error message. An empty object
 *     represents a valid form submission.
 */
function validateFormInputs(caseDetails) {
  const errors = {};
  if (caseDetails.name === undefined) {
    errors.name = 'You must provide a name';
  }
  if (caseDetails.description === undefined) {
    errors.description = 'You must provide a description';
  }
  if (caseDetails.priority === undefined) {
    errors.priority = 'You must provide a priority';
  }
  if (caseDetails.impact && !(['P0', 'P1']).includes(caseDetails.priority)) {
    errors.impact = 'If an issue blocks a critical customer operation, priority must be P0 or P1';
  }

  return errors;
}

/**
 * Returns a text paragraph with red text indicating a form field validation error.
 * 
 * @param {string} errorMessage A description of input value error.
 * @return {!TextParagraph} The resulting text paragraph.
 */
function createErrorTextParagraph(errorMessage) {
  return {
    textParagraph: {
      text: '<font color=\\"#BA0300\\"><b>Error:</b> ' + errorMessage + '</font>'
    }
  }
}

/**
 * Returns a submit form response that inserts a link into the document.
 * 
 * @param {string} title The title of the link to insert.
 * @param {string} url The URL of the link to insert.
 * @return {!SubmitFormResponse} The resulting submit form response.
 */
function createLinkRenderAction(title, url) {
  return {
    renderActions: {
      action: {
        links: [{
          title: title,
          url: url
        }]
      }
    }
  };
}
```

#### Python

Python's Cloud Function deployment uses two separate function files: one for resource creation (`create_3p_resources`) and one for link previews (`create_link_preview`).

##### create_3p_resources

```python
# Copyright 2024 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License")
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https:#www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from typing import Any, Mapping
from urllib.parse import urlencode

import os
import flask
import functions_framework

@functions_framework.http
def create_3p_resources(req: flask.Request):
    """Responds to any HTTP request related to 3P resource creations.
    Args:
      req: An HTTP request context.
    Returns:
      An HTTP response context.
    """
    event = req.get_json(silent=True)
    parameters = event["commonEventObject"]["parameters"] if "parameters" in event["commonEventObject"] else None
    if parameters is not None and parameters["submitCaseCreationForm"]:
        return submit_case_creation_form(event)
    else:
        return create_case_input_card(event)

def create_case_input_card(event, errors = {}, isUpdate = False):
    """Produces a support case creation form card.
    Args:
      event: The event object.
      errors: An optional dict of per-field error messages.
      isUpdate: Whether to return the form as an update card navigation.
    Returns:
      The resulting card or action response.
    """
    card_header1 = {
        "title": "Create a support case"
    }

    card_section1_text_input1 = {
        "textInput": {
            "name": "name",
            "label": "Name"
        }
    }

    card_section1_text_input2 = {
        "textInput": {
            "name": "description",
            "label": "Description",
            "type": "MULTIPLE_LINE"
        }
    }

    card_section1_selection_input1 = {
        "selectionInput": {
            "name": "priority",
            "label": "Priority",
            "type": "DROPDOWN",
            "items": [{
                "text": "P0",
                "value": "P0"
            }, {
                "text": "P1",
                "value": "P1"
            }, {
                "text": "P2",
                "value": "P2"
            }, {
                "text": "P3",
                "value": "P3"
            }]
        }
    }

    card_section1_selection_input2 = {
        "selectionInput": {
            "name": "impact",
            "label": "Impact",
            "items": [{
                "text": "Blocks a critical customer operation",
                "value": "Blocks a critical customer operation"
            }]
        }
    }

    card_section1_button_list1_button1_action1 = {
        "function": os.environ["URL"],
        "parameters": [
        {
            "key": "submitCaseCreationForm",
            "value": True
        }
        ],
        "persistValues": True
    }

    card_section1_button_list1_button1 = {
        "text": "Create",
        "onClick": {
            "action": card_section1_button_list1_button1_action1
        }
    }

    card_section1_button_list1 = {
        "buttonList": {
            "buttons": [card_section1_button_list1_button1]
        }
    }

    # Builds the creation form and adds error text for invalid inputs.
    card_section1 = []
    if "name" in errors:
        card_section1.append(create_error_text_paragraph(errors["name"]))
    card_section1.append(card_section1_text_input1)
    if "description" in errors:
        card_section1.append(create_error_text_paragraph(errors["description"]))
    card_section1.append(card_section1_text_input2)
    if "priority" in errors:
        card_section1.append(create_error_text_paragraph(errors["priority"]))
    card_section1.append(card_section1_selection_input1)
    if "impact" in errors:
        card_section1.append(create_error_text_paragraph(errors["impact"]))

    card_section1.append(card_section1_selection_input2)
    card_section1.append(card_section1_button_list1)

    card = {
        "header": card_header1,
        "sections": [{
            "widgets": card_section1
        }]
    }

    if isUpdate:
        return {
            "renderActions": {
                "action": {
                        "navigations": [{
                        "updateCard": card
                    }]
                }
            }
        }
    else:
        return {
            "action": {
                "navigations": [{
                    "pushCard": card
                }]
            }
        }

def submit_case_creation_form(event):
    """Submits the creation form.

    If valid, returns a render action that inserts a new link
    into the document. If invalid, returns an update card navigation that
    re-renders the creation form with error messages.
    Args:
      event: The event object with form input values.
    Returns:
      The resulting response.
    """
    formInputs = event["commonEventObject"]["formInputs"] if "formInputs" in event["commonEventObject"] else None
    case_details = {
        "name":  None,
        "description": None,
        "priority": None,
        "impact": None,
    }
    if formInputs is not None:
        case_details["name"] = formInputs["name"]["stringInputs"]["value"][0] if "name" in formInputs else None
        case_details["description"] = formInputs["description"]["stringInputs"]["value"][0] if "description" in formInputs else None
        case_details["priority"] = formInputs["priority"]["stringInputs"]["value"][0] if "priority" in formInputs else None
        case_details["impact"] = formInputs["impact"]["stringInputs"]["value"][0] if "impact" in formInputs else False

    errors = validate_form_inputs(case_details)
    if len(errors) > 0:
        return create_case_input_card(event, errors, True) # Update mode
    else:
        title = f'Case {case_details["name"]}'
        # Adds the case details as parameters to the generated link URL.
        url = "https://example.com/support/cases/?" + urlencode(case_details)
        return create_link_render_action(title, url)

def validate_form_inputs(case_details):
    """Validates case creation form input values.
    Args:
      case_details: The values of each form input submitted by the user.
    Returns:
      A dict from field name to error message. An empty object represents a valid form submission.
    """
    errors = {}
    if case_details["name"] is None:
        errors["name"] = "You must provide a name"
    if case_details["description"] is None:
        errors["description"] = "You must provide a description"
    if case_details["priority"] is None:
        errors["priority"] = "You must provide a priority"
    if case_details["impact"] is not None and case_details["priority"] not in ['P0', 'P1']:
        errors["impact"] = "If an issue blocks a critical customer operation, priority must be P0 or P1"
    return errors

def create_error_text_paragraph(error_message):
    """Returns a text paragraph with red text indicating a form field validation error.
    Args:
      error_essage: A description of input value error.
    Returns:
      The resulting text paragraph.
    """
    return {
        "textParagraph": {
            "text": '<font color=\\"#BA0300\\"\><b>Error:</b> ' + error_message + '</font>'
        }
    }

def create_link_render_action(title, url):
    """Returns a submit form response that inserts a link into the document.
    Args:
      title: The title of the link to insert.
      url: The URL of the link to insert.
    Returns:
      The resulting submit form response.
    """
    return {
        "renderActions": {
            "action": {
                "links": [{
                    "title": title,
                    "url": url
                }]
            }
        }
    }
```

##### create_link_preview

```python
# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License")
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https:#www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

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

#### Java

The Java implementation for the complete example follows the same structure as the Apps Script and Node.js versions, combining a `caseLinkPreview` handler with the `createCaseInputCard`, `submitCaseCreationForm`, `validateFormInputs`, `createErrorTextParagraph`, and `createLinkRenderAction` methods shown in full earlier in this document (in the "Example of card with form inputs," "Example of a SubmitFormResponse for a created resource," and "Example of error handling" sections), assembled into a single `Create3pResources` HTTP function class using the Gson library for JSON construction.

## Related resources

- Preview links with smart chips
- Test your add-on
- Google Docs manifest
- Card interfaces for link previews
