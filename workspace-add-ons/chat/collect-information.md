# Collect and process information from Google Chat users

## Page Summary

- Google Chat apps can collect user information using forms embedded within cards, offering interactive elements like text inputs, selection inputs, and date-time pickers.
- These apps can utilize data from both Google Workspace and external sources, enhancing their functionality and data integration capabilities.
- Upon form submission, the app receives user input data, enabling it to process, transfer data to other cards, or provide direct responses within the Chat interface.
- Multiselect menus support dynamic suggestions as users type, streamlining interactions and data entry processes, especially when utilizing external data sources.
- Developers can leverage Node.js or Apps Script along with a Google Workspace add-on to build and deploy these interactive Google Chat apps.

This guide describes how Google Chat apps can collect and process information
from users by building form inputs in card-based interfaces.

**Note:** In Google Chat, add-ons appear to users as
Google Chat apps. You can also build your Chat app using 
*Google Chat API interaction events*. To learn more, see the
[Extend Google Chat overview](https://developers.google.com/workspace/add-ons/chat).

![A dialog featuring a variety of different widgets.](https://developers.google.com/static/workspace/add-ons/images/dialogs-card-1.png)

![](https://developers.google.com/static/workspace/add-ons/images/dialogs-card-1.png)

Chat apps request information from users to perform actions in or
outside of Chat, including in the following ways:

- Configure settings. For example, to let users customize notification settings
or configure and add the Chat app to one or more
spaces.
- Create or update information in other Google Workspace applications. For
example, let users create a Google Calendar event.
- Let users access and update resources in other apps or web services. For
example, a Chat app can help users update the
status of a support ticket directly from a Chat space.

## Prerequisites

**HTTP**

A Google Workspace add-on that extends Google Chat. To build one,
complete the [HTTP
quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-http).

**Apps Script**

A Google Workspace add-on that extends Google Chat. To build one,
complete the [Apps Script quickstart](https://developers.google.com/workspace/add-ons/chat/quickstart-apps-script).

## Build forms using cards

To collect information, Chat apps design forms and their inputs,
and build them into cards. To display cards to users,
Chat apps can use the following Chat interfaces:

- Chat messages that contain one or more cards.
- [Dialogs](https://developers.google.com/workspace/add-ons/chat/dialogs), which are cards that open
 in a new window from messages and homepages.

Chat apps can build the cards using the following widgets:

- Form input widgets that request information from users. Optionally, you can
add [validation](https://developers.google.com/workspace/chat/design-interactive-card-dialog#card-validation)
to form input widgets, to ensure that users input and format information
correctly. Chat apps can use the following form input widgets:
    - [Text inputs](https://developers.google.com/workspace/chat/design-interactive-card-dialog#collect-text)
  (`textInput`) for free-form or suggested text.
    - [Selection inputs](https://developers.google.com/workspace/chat/design-interactive-card-dialog#let-users-select)
  (`selectionInput`) are selectable UI elements such as checkboxes,
  radio buttons, and drop-down menus. Selection input widgets can also
  populate and suggest items from Google Workspace data (such as a
  Chat space) or a dynamic data source. For details, see
  the following sections Add a drop-down menu and
  Add a multiselect menu.
    - [Date time pickers](https://developers.google.com/workspace/chat/design-interactive-card-dialog#collect-dates)
  (`dateTimePicker`) for date and time entries.
- A [button](https://developers.google.com/workspace/chat/design-interactive-card-dialog#add-button) widget
so that users can submit values that they've input in the card.
After a user clicks the button, the Chat app can then
process the information it receives.

In the following example, a card collects contact information using a text
input, date time picker, and selection input:

For more examples of interactive widgets that you can use to collect
information, see
[Design an interactive card or dialog](https://developers.google.com/workspace/chat/design-interactive-card-dialog)
in the Google Chat API documentation.

### Add a drop-down menu

To customize selection items or let users select a single item from a dynamic
data source, Chat apps can use drop-down menus, which are a type
of `SelectionInput` widget. For example, the following card displays a
drop-down menu where users can dynamically select from a list of contacts:

You can populate items for a drop-down menu from the following data
sources:

- Google Workspace data, which includes
users or Chat spaces.
- External data sources, such as a relational
database.

#### Populate items from a Google Workspace data source

To populate items from Google Workspace data sources, such as
Google Workspace users, specify the `platformDataSource` field within a
[`DataSourceConfig`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataSourceConfig)
object. Unlike other selection input types, you
omit
[`SelectionItem`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectionitem)
objects, because these selection items are dynamically sourced from
Google Workspace.

The following code shows a drop-down menu of Google Workspace users:

**JSON**

```json
{
  "sections": [
    {
      "header": "Section Header",
      "widgets": [
        {
          "selectionInput": {
            "name": "contacts",
            "type": "DROPDOWN",
            "label": "Select contact from organization",
            "data_source_configs": [
              {
                "platformDataSource": {
                  "commonDataSource": "USER"
                },
                "min_characters_trigger": 1
              }
            ]
          }
        }
      ]
    }
  ]
}
```

#### Populate items from an external data source

Drop-down menus can also populate items from a third-party or external data
source. To use an external data source, you specify the
[`remoteDataSource`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataSourceConfig.FIELDS.google.apps.card.v1.Action.google.apps.card.v1.DataSourceConfig.remoteDataSource)
field within a
[`DataSourceConfig`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataSourceConfig)
object that contains the function that queries and returns items from the data
source.

To reduce the requests to an external data source, you can include
suggested items that appear in the drop-down menu before users type in
the menu. To populate suggested items from an external data source, specify static
[`SelectionItem`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectionitem)
objects.

The following code shows a drop-down menu that queries and populates
items from an external data source:

**JSON**

```json
{
  "sections": [
    {
      "header": "Section Header",
      "widgets": [
        {
          "selectionInput": {
            "name": "crm_leads",
            "type": "DROPDOWN",
            "label": "Select CRM Lead",
            "data_source_configs": [
              {
                "remoteDataSource": {
                  "function": "getCrmLeads"
                },
                "min_characters_trigger": 2
              }
            ],
            "items": [
              {
                "text": "Suggested Lead 1",
                "value": "lead-1"
              }
            ]
          }
        }
      ]
    }
  ]
}
```

For a complete example that shows how to return suggested items, see the section
Suggest selection items.

### Add a multiselect menu

To customize selection items or let users select items from a dynamic data
source, Chat apps can use multiselect menus, which are a type of
`SelectionInput` widget. For example, the following card displays a multiselect
menu where users can dynamically select from a list of contacts:

You can populate items for a multiselect menu from the following data
sources:

- Google Workspace data, which includes users
or Chat spaces of which the user is a member. The menu only
populates items from the same Google Workspace organization.
- External data sources, such as a relational database.
For example, you can use multiselect menus to help a user select from a
list of sales leads from a customer relationship management (CRM) system.

#### Populate items from a Google Workspace data source

To use Google Workspace data sources, specify the
[`platformDataSource`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.SelectionInput.PlatformDataSource)
field in the `SelectionInput` widget. Unlike other selection input types, you
omit
[`SelectionItem`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectionitem)
objects, because these selection items are dynamically sourced from
Google Workspace.

The following code shows a multiselect menu of Google Workspace users.
To populate users, the selection input sets `commonDataSource` to `USER`:

**JSON**

```json
{
  "selectionInput": {
    "name": "contacts",
    "type": "MULTI_SELECT",
    "label": "Selected contacts",
    "multiSelectMaxSelectedItems": 5,
    "multiSelectMinQueryLength": 1,
    "platformDataSource": {
      "commonDataSource": "USER"
    }
  }
}
```

The following code shows a multiselect menu of Chat
spaces. To populate spaces, the selection input specifies the
`hostAppDataSource` field. The multiselect menu also sets
`defaultToCurrentSpace` to `true`, which makes the current space the default
selection in the menu:

**JSON**

```json
{
  "selectionInput": {
    "name": "spaces",
    "type": "MULTI_SELECT",
    "label": "Selected contacts",
    "multiSelectMaxSelectedItems": 3,
    "multiSelectMinQueryLength": 1,
    "platformDataSource": {
      "hostAppDataSource": {
        "chatDataSource": {
          "spaceDataSource": {
            "defaultToCurrentSpace": true
          }
        }
      }
    }
  }
}
```

#### Populate items from an external data source

Multiselect menus can also populate items from a third-party or external data
source. To use an external data source, you specify the
[`externalDataSource`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.SelectionInput.FIELDS.google.apps.card.v1.Action.google.apps.card.v1.SelectionInput.externalDataSource)
field in the `SelectionInput` widget that contains the function that queries
and returns items from the data source.

To reduce the requests to an external data source, you can include
suggested items that appear in the multiselect menu before users type in
the menu. For example, you can populate recently searched contacts for the
user. To populate suggested items from an external data source, specify static
[`SelectionItem`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectionitem)
objects.

The following code sample shows a multiselect menu that queries and populates
items from an external data source:

**Node.js**

```javascript
selectionInput: {
  name: "contacts",
  type: "MULTI_SELECT",
  label: "Selected contacts",
  multiSelectMaxSelectedItems: 3,
  multiSelectMinQueryLength: 1,
  externalDataSource: { function: FUNCTION_URL },
  // Suggested items loaded by default.
  // The list is static here but it could be dynamic.
  items: [getSuggestedContact("3")]
}
```

**Python**

```python
'selectionInput': {
  'name': "contacts",
  'type': "MULTI_SELECT",
  'label': "Selected contacts",
  'multiSelectMaxSelectedItems': 3,
  'multiSelectMinQueryLength': 1,
  'externalDataSource': { 'function': FUNCTION_URL },
  # Suggested items loaded by default.
  # The list is static here but it could be dynamic.
  'items': [get_suggested_contact("3")]
}
```

**Java**

```java
.setSelectionInput(new GoogleAppsCardV1SelectionInput()
  .setName("contacts")
  .setType("MULTI_SELECT")
  .setLabel("Selected contacts")
  .setMultiSelectMaxSelectedItems(3)
  .setMultiSelectMinQueryLength(1)
  .setExternalDataSource(new GoogleAppsCardV1Action().setFunction(FUNCTION_URL))
  // Suggested items loaded by default.
  // The list is static here but it could be dynamic.
  .setItems(List.of(getSuggestedContact("3")))))))))));
```

**Apps Script**

```javascript
selectionInput: {
  name: "contacts",
  type: "MULTI_SELECT",
  label: "Selected contacts",
  multiSelectMaxSelectedItems: 3,
  multiSelectMinQueryLength: 1,
  externalDataSource: { function: "queryContacts" },
  // Suggested items loaded by default.
  // The list is static here but it could be dynamic.
  items: [getSuggestedContact("3")]
}
```

For a complete example that shows how to return suggested items, see the section
Suggest selection items.

## Receive data from interactive widgets

Whenever users click a button, its Chat apps
[action](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#action)
is triggered with information about the interaction. In the
[`commonEventObject`](https://developers.google.com/workspace/add-ons/concepts/event-objects#common_event_object)
of the event payload, the `formInputs` object contains any values that the
user inputs.

You can retrieve the values from the object
`commonEventObject.formInputs.WIDGET_NAME`, where
`WIDGET_NAME` is the `name` field that you specified for the widget.
The values are returned as a specific data type for the widget.

The following shows a portion of an event object where a user entered values
for each widget:

```json
{
  "commonEventObject": { "formInputs": {
    "contactName": { "stringInputs": {
      "value": ["Kai 0"]
    }},
    "contactBirthdate": { "dateInput": {
      "msSinceEpoch": 1000425600000
    }},
    "contactType": { "stringInputs": {
      "value": ["Personal"]
    }}
  }}
}
```

To receive the data, your Chat app handles the event
object to get the values that users enter into widgets. The following table
shows how to get the value for a given form input widget. For each widget, the
table shows the data type that the widget accepts, where the value is stored in
the event object, and an example value.

| Form input widget | Type of input data | Input value from the event object | Example value |
|---|---|---|---|
| `textInput` | `stringInputs` | `event.commonEventObject.formInputs.contactName.stringInputs.value[0]` | `Kai O` |
| `selectionInput` | `stringInputs` | To get the first or only value, `event.commonEventObject.formInputs.contactType.stringInputs.value[0]` | `Personal` |
| `dateTimePicker` that only accepts dates. | `dateInput` | `event.commonEventObject.formInputs.contactBirthdate.dateInput.msSinceEpoch` . | `1000425600000` |

After the Chat app receives data, it can do any of the
following:

- For cards that contain a multiselect menu,
populate or suggest items based on what the user types
into the menu.
- Transfer the data to another card, so that the user can review
their information or continue to the next section of the form.
- Respond to the user to confirm that the user successfully
completed the form.

### Suggest selection items

If a card contains a multiselect menu or a drop-down menu that
populates items from an external data source,
the Chat app can return suggested items based on what
users type into the menu. For example, if a user starts typing `Atl` for a menu
that populates cities in the United States, your
Chat app can autosuggest `Atlanta` before the user
finishes typing. The Chat app can suggest up to 100
items.

To suggest and dynamically populate items in a selection input, the
`SelectionInput` widget on the card must specify a function that queries the
external data source. For multiselect menus, you specify the
[`externalDataSource`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.SelectionInput.FIELDS.google.apps.card.v1.Action.google.apps.card.v1.SelectionInput.externalDataSource)
field. For drop-down menus, you specify the
[`remoteDataSource`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataSourceConfig.FIELDS.google.apps.card.v1.Action.google.apps.card.v1.DataSourceConfig.remoteDataSource)
field within a
[`DataSourceConfig`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.DataSourceConfig)
object.

You can also configure the number of characters that a user types before the
menu returns suggestions. For multiselect menus, set the
`multiSelectMinQueryLength` field. For drop-down menus, set the
`min_characters_trigger` field within the `DataSourceConfig`.

To return suggested items, the function must do the following:

1. Handle an [event object](https://developers.google.com/workspace/add-ons/chat/build#event-objects), which
the Chat app receives when users type into the menu.
2. From the event object, get the value that the user types, which is
represented in the
`event.commonEventObject.parameters["autocomplete_widget_query"]` field.
3. Query the data source using the user input value to get one or more
`SelectionItems` to suggest to the user.
4. Return suggested items by returning the action
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions) with a `modifyCard`
object.

The following code sample shows how a Chat app
dynamically suggests items in the multiselect menu on a card. When a user types
into the menu, the function or endpoint provided in the widget's
`externalDataSource` field queries an external data source, and suggests items
that the user can select.

**Node.js**

```javascript
/**
 * Web app that responds to events sent from a Google Chat space.
 *
 * @param {Object} req Request sent from Google Chat space
 * @param {Object} res Response to send back
 */
app.post('/', async (req, res) => {
  // Stores the Google Chat event
  const chatEvent = req.body.chat;

  // Handle user interaction with multiselect.
  if(chatEvent.widgetUpdatedPayload) {
    return res.json(queryContacts(req.body));
  }

  // Replies with a card that contains the multiselect menu.
  return res.json({ hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    cardsV2: [{
      cardId: "contactSelector",
      card: { sections:[{ widgets: [{
        selectionInput: {
          name: "contacts",
          type: "MULTI_SELECT",
          label: "Selected contacts",
          multiSelectMaxSelectedItems: 3,
          multiSelectMinQueryLength: 1,
          externalDataSource: { function: FUNCTION_URL },
          // Suggested items loaded by default.
          // The list is static here but it could be dynamic.
          items: [getSuggestedContact("3")]
        }
      }]}]}
    }]
  }}}}});
});

/**
 * Get contact suggestions based on text typed by users.
 *
 * @param {Object} event the event object that contains the user's query
 * @return {Object} suggestions
 */
function queryContacts(event) {
  const query = event.commonEventObject.parameters["autocomplete_widget_query"];
  return { action: { modifyOperations: [{ updateWidget: { selectionInputWidgetSuggestions: { suggestions: [
    // The list is static here but it could be dynamic.
    getSuggestedContact("1"), getSuggestedContact("2"), getSuggestedContact("3"), getSuggestedContact("4"), getSuggestedContact("5")
  // Only return items based on the query from the user.
  ].filter(e => !query || e.text.includes(query)) }}}]}};
}

/**
 * Generate a suggested contact given an ID.
 *
 * @param {String} id The ID of the contact to return.
 * @return {Object} The contact formatted as a selection item in the menu.
 */
function getSuggestedContact(id) {
  return {
    value: id,
    startIconUri: "https://www.gstatic.com/images/branding/product/2x/contacts_48dp.png",
    text: "Contact " + id
  };
}
```

**Python**

```python
@app.route('/', methods=['POST'])
def post() -> Mapping[str, Any]:
  """Handle requests from Google Chat

  Returns:
      Mapping[str, Any]: The response
  """
  # Stores the Google Chat event
  chatEvent = request.get_json().get('chat')

  # Handle user interaction with multiselect.
  if chatEvent.get('widgetUpdatedPayload') is not None:
    return json.jsonify(query_contacts(request.get_json()))

  # Replies with a card that contains the multiselect menu.
  return json.jsonify({ 'hostAppDataAction': { 'chatDataAction': { 'createMessageAction': {
    'message': { 'cardsV2': [{
      'cardId': "contactSelector",
      'card': { 'sections':[{ 'widgets': [{
        'selectionInput': {
          'name': "contacts",
          'type': "MULTI_SELECT",
          'label': "Selected contacts",
          'multiSelectMaxSelectedItems': 3,
          'multiSelectMinQueryLength': 1,
          'externalDataSource': { 'function': FUNCTION_URL },
          # Suggested items loaded by default.
          # The list is static here but it could be dynamic.
          'items': [get_suggested_contact("3")]
        }
      }]}]}
    }]}
  }}}})

def query_contacts(event: dict) -> dict:
  """Get contact suggestions based on text typed by users.

  Args:
      event (Mapping[str, Any]): The event object that contains the user's query

  Returns:
      Mapping[str, Any]: The response with contact suggestions.
  """
  query = event.get("commonEventObject").get("parameters").get("autocomplete_widget_query")
  return { 'action': { 'modifyOperations': [{ 'updateWidget': { 'selectionInputWidgetSuggestions': { 'suggestions': list(
    filter(lambda e: query is None or query in e["text"], [
      # The list is static here but it could be dynamic.
      get_suggested_contact("1"), get_suggested_contact("2"), get_suggested_contact("3"), get_suggested_contact("4"), get_suggested_contact("5")
    # Only return items based on the query from the user
    ])
  )}}}]}}

def get_suggested_contact(id: str) -> dict:
  """Generate a suggested contact given an ID.

  Args:
      id (str): The ID of the contact to return.

  Returns:
      Mapping[str, Any]: The contact formatted as a selection item in the menu.
  """
  return {
    'value': id,
    'startIconUri': "https://www.gstatic.com/images/branding/product/2x/contacts_48dp.png",
    'text': "Contact " + id
  }
```

**Java**

```java
@SpringBootApplication
@RestController
// Web app that responds to events sent from a Google Chat space.
public class App {
  private static final String FUNCTION_URL = "your-function-url";

  public static void main(String[] args) {
    SpringApplication.run(App.class, args);
  }

  /**
   * Handle requests from Google Chat
   * 
   * @param event the event object sent by Google Chat
   * @return The response to be sent back to Google Chat
   */
  @PostMapping("/")
  @ResponseBody
  public GenericJson onEvent(@RequestBody JsonNode event) throws Exception {
    // Stores the Google Chat event
    JsonNode chatEvent = event.at("/chat");

    // Handle user interaction with multiselect.
    if (!chatEvent.at("/widgetUpdatedPayload").isEmpty()) {
      return queryContacts(event);
    }

    // Replies with a card that contains the multiselect menu.
    Message message = new Message().setCardsV2(List.of(new CardWithId()
      .setCardId("contactSelector")
      .setCard(new GoogleAppsCardV1Card()
        .setSections(List.of(new GoogleAppsCardV1Section().setWidgets(List.of(new GoogleAppsCardV1Widget()
          .setSelectionInput(new GoogleAppsCardV1SelectionInput()
            .setName("contacts")
            .setType("MULTI_SELECT")
            .setLabel("Selected contacts")
            .setMultiSelectMaxSelectedItems(3)
            .setMultiSelectMinQueryLength(1)
            .setExternalDataSource(new GoogleAppsCardV1Action().setFunction(FUNCTION_URL))
            // Suggested items loaded by default.
            // The list is static here but it could be dynamic.
            .setItems(List.of(getSuggestedContact("3")))))))))));

    return new GenericJson() {{
      put("hostAppDataAction", new GenericJson() {{
        put("chatDataAction", new GenericJson() {{
          put("createMessageAction", new GenericJson() {{
            put("message", message);
          }});
        }});
      }});
    }};
  }

  /**
   * Get contact suggestions based on text typed by users.
   *
   * @param event the event object that contains the user's query.
   * @return The response with contact suggestions.
   */
  GenericJson queryContacts(JsonNode event) throws Exception {
    String query = event.at("/commonEventObject/parameters/autocomplete_widget_query").asText();
    List<GoogleAppsCardV1SelectionItem> suggestions = List.of(
      // The list is static here but it could be dynamic.
      getSuggestedContact("1"), getSuggestedContact("2"), getSuggestedContact("3"), getSuggestedContact("4"), getSuggestedContact("5")
    // Only return items based on the query from the user
    ).stream().filter(e -> query == null || e.getText().indexOf(query) > -1).toList();

    return new GenericJson() {{
      put("action", new GenericJson() {{
        put("modifyOperations", List.of(new GenericJson() {{
          put("updateWidget", new GenericJson() {{
            put("selectionInputWidgetSuggestions", new GenericJson() {{
              put("suggestions", suggestions);
            }});
          }});
        }}));
      }});
    }};
  }

  /**
   * Generate a suggested contact given an ID.
   * 
   * @param id The ID of the contact to return.
   * @return The contact formatted as a selection item in the menu.
   */
  GoogleAppsCardV1SelectionItem getSuggestedContact(String id) {
    return new GoogleAppsCardV1SelectionItem()
      .setValue(id)
      .setStartIconUri("https://www.gstatic.com/images/branding/product/2x/contacts_48dp.png")
      .setText("Contact " + id);
  }
}
```

**Apps Script**

```javascript
/**
* Responds to a Message trigger in Google Chat.
*
* @param {Object} event the event object from Google Chat
* @return {Object} Response from the Chat app.
*/
function onMessage(event) {
  // Replies with a card that contains the multiselect menu.
  return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
    cardsV2: [{
      cardId: "contactSelector",
      card: { sections:[{ widgets: [{
        selectionInput: {
          name: "contacts",
          type: "MULTI_SELECT",
          label: "Selected contacts",
          multiSelectMaxSelectedItems: 3,
          multiSelectMinQueryLength: 1,
          externalDataSource: { function: "queryContacts" },
          // Suggested items loaded by default.
          // The list is static here but it could be dynamic.
          items: [getSuggestedContact("3")]
        }
      }]}]}
    }]
  }}}}};
}

/**
* Get contact suggestions based on text typed by users.
*
* @param {Object} event the event object that contains the user's query
* @return {Object} suggestions
*/
function queryContacts(event) {
  const query = event.commonEventObject.parameters["autocomplete_widget_query"];
  return { action: { modifyOperations: [{ updateWidget: { selectionInputWidgetSuggestions: { suggestions: [
    // The list is static here but it could be dynamic.
    getSuggestedContact("1"), getSuggestedContact("2"), getSuggestedContact("3"), getSuggestedContact("4"), getSuggestedContact("5")
  // Only return items based on the query from the user.
  ].filter(e => !query || e.text.includes(query)) }}}]}};
}

/**
* Generate a suggested contact given an ID.
*
* @param {String} id The ID of the contact to return.
* @return {Object} The contact formatted as a selection item in the menu.
*/
function getSuggestedContact(id) {
  return {
    value: id,
    startIconUri: "https://www.gstatic.com/images/branding/product/2x/contacts_48dp.png",
    text: "Contact " + id
  };
}
```

### Transfer data to another card

After a user submits information from a card, you might need to return
additional cards to do any of the following:

- Help users to complete longer forms by creating distinct sections.
- Let users preview and confirm information from the initial card, so that they
can review their answers before submitting.
- Dynamically populate the remaining parts of the form. For example, to prompt
users to create an appointment, a Chat app could
display an initial card that requests the reason for the appointment, and
then populates another card that provides available times based on the
appointment type.

To transfer the data input from the initial card, you can build the `button`
widget with
[`actionParameters`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.Action.ActionParameter)
that contain the widget's `name` and the value the user inputs, as shown
in the following example:

**Node.js**

```javascript
{ buttonList: { buttons: [{
  text: "SUBMIT",
  onClick: { action: {
    function: FUNCTION_URL,
    parameters: [
      { key: "actionName", value: "submitDialog" },
      // Pass input values as parameters for last dialog step (submission)
      { key: "contactName", value: name },
      { key: "contactBirthdate", value: birthdate },
      { key: "contactType", value: type }
    ]
  }}
}]}}
```

**Python**

```python
{ 'buttonList': { 'buttons': [{
  'text': "SUBMIT",
  'onClick': { 'action': {
    'function': FUNCTION_URL,
    'parameters': [
      { 'key': "actionName", 'value': "submitDialog" },
      # Pass input values as parameters for last dialog step (submission)
      { 'key': "contactName", 'value': name },
      { 'key': "contactBirthdate", 'value': birthdate },
      { 'key': "contactType", 'value': type }
    ]
  }}
}]}}
```

**Java**

```java
new GoogleAppsCardV1Widget().setButtonList(new GoogleAppsCardV1ButtonList().setButtons(List.of(
  new GoogleAppsCardV1Button()
    .setText("SUBMIT")
    .setOnClick(new GoogleAppsCardV1OnClick().setAction(new GoogleAppsCardV1Action()
      .setFunction(FUNCTION_URL)
      .setParameters(List.of(
        new GoogleAppsCardV1ActionParameter().setKey("actionName").setValue("submitDialog"),
        // Pass input values as parameters for last dialog step (submission)
        new GoogleAppsCardV1ActionParameter().setKey("contactName").setValue(name),
        new GoogleAppsCardV1ActionParameter().setKey("contactBirthdate").setValue(birthdate),
        new GoogleAppsCardV1ActionParameter().setKey("contactType").setValue(type))))))))))));
```

**Apps Script**

```javascript
{ buttonList: { buttons: [{
  text: "SUBMIT",
  onClick: { action: {
    function: "submitDialog",
    // Pass input values as parameters for last dialog step (submission)
    parameters: [
      { key: "contactName", value: name },
      { key: "contactBirthdate", value: birthdate },
      { key: "contactType", value: type }
    ]
  }}
}]}}
```

When a user clicks the button, your Chat app receives
an event object from which you can receive data.

## Respond to a form submission

After receiving the data from a card message or dialog, the
Chat app responds by either acknowledging receipt or
returning an error.

In the following example, a Chat app sends a text
message to confirm that it has successfully received a form submitted from a
card message.

**Node.js**

```javascript
return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
  text: "✅ " + event.commonEventObject.parameters["contactName"] + " has been added to your contacts."
}}}}};
```

**Python**

```python
return { 'hostAppDataAction': { 'chatDataAction': { 'createMessageAction': { 'message': {
  'text': "✅ " + event.get('commonEventObject').get('parameters')["contactName"] + " has been added to your contacts."
}}}}}
```

**Java**

```java
return new GenericJson() {{
  put("hostAppDataAction", new GenericJson() {{
    put("chatDataAction", new GenericJson() {{
      put("createMessageAction", new GenericJson() {{
        put("message", new Message()
          .setText( "✅ " + event.at("/commonEventObject/parameters/contactName").asText() +
                    " has been added to your contacts."));
      }});
    }});
  }});
}};
```

**Apps Script**

```javascript
return { hostAppDataAction: { chatDataAction: { createMessageAction: { message: {
  text: "✅ " + event.commonEventObject.parameters["contactName"] + " has been added to your contacts."
}}}}};
```

To process and close a dialog, you return an
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions)
object that specifies whether you want to send a confirmation message, update
the original message or card, or just close the dialog. For steps, see
[Close a dialog](https://developers.google.com/workspace/add-ons/chat/dialogs#close).

## Troubleshoot

This section provides troubleshooting steps for specific error codes and runtime
behaviors when interacting with dialogs in Chat.

### Dialog interactions return "Unspecified error invoking the add-on"

When interacting with a dialog, if you see error logs with message
"Unspecified error invoking the add-on." and code 13, it usually indicates
an internal error or that the Chat app's HTTP endpoint
failed to process the request or return a valid response.

To troubleshoot this error:

- Check your HTTP endpoint's logs for any unhandled exceptions or crashes.
- Verify that your endpoint responds to requests within 30 seconds. If
endpoint takes longer than 30 seconds to run, Chat can't
process response and interaction fails. For details see
[Rate limits and best practices](https://developers.google.com/workspace/chat/limits).
- Ensure your endpoint returns a valid response. For dialog submissions,
endpoint must return a
[`RenderActions`](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#renderactions)
object in correct JSON format. If response is malformed or doesn't contain
required fields, dialog interaction might fail.

When a Google Chat app or
 [card](https://developers.google.com/workspace/chat/create-messages#create) returns an error, the
 Chat interface surfaces a message saying "Something went wrong."
 or "Unable to process your request." Sometimes the Chat UI
 doesn't display any error message, but the Chat app or
 card produces an unexpected result; for example, a card message might not
 appear.

Although an error message might not display in the Chat UI,
 descriptive error messages and log data are available to help you fix errors
 when error logging for Chat apps is turned on. For help viewing,
 debugging, and fixing errors, see
 [Troubleshoot and fix Google Chat errors](https://developers.google.com/workspace/chat/troubleshoot).
