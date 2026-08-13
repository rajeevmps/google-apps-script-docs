# Collect and process information from Google Chat users

## Overview

Google Chat apps enable developers to gather user information through form-embedded cards with interactive elements. The guide explains how to build these forms, receive user data, and process submissions.

### Key Capabilities

Per the documentation: "Google Chat apps can collect user information using forms embedded within cards, offering interactive elements like text inputs, selection inputs, and date-time pickers."

## Building Forms Using Cards

### Form Input Widgets Available

Chat apps support the following form input widgets:

- **Text inputs** (`textInput`) for free-form or suggested text
- **Selection inputs** (`selectionInput`) including checkboxes, radio buttons, and drop-down menus
- **Date-time pickers** (`dateTimePicker`) for date and time entries
- **Button widgets** for form submission

### Selection Input Types

#### Drop-down Menus

Developers can populate items from:
- **Google Workspace data sources** (users, Chat spaces) via `platformDataSource`
- **External data sources** via `remoteDataSource` field

#### Multiselect Menus

These support:
- **Google Workspace data** using `platformDataSource` with `commonDataSource` set to "USER"
- **External data sources** via `externalDataSource` field
- **Dynamic suggestions** as users type
- Configuration options like `multiSelectMaxSelectedItems` and `multiSelectMinQueryLength`

## Receiving Data from Widgets

User input values are accessed through the event object structure:

```
event.commonEventObject.formInputs.WIDGET_NAME
```

### Data Type Mapping

| Widget | Data Type | Access Path | Example |
|--------|-----------|-------------|---------|
| `textInput` | `stringInputs` | `formInputs.contactName.stringInputs.value[0]` | "Kai O" |
| `selectionInput` | `stringInputs` | `formInputs.contactType.stringInputs.value[0]` | "Personal" |
| `dateTimePicker` | `dateInput` | `formInputs.contactBirthdate.dateInput.msSinceEpoch` | "1000425600000" |

## Suggesting Selection Items

When multiselect or drop-down menus use external data sources, apps can dynamically suggest items. The process involves:

1. Handling an event object when users type into the menu
2. Retrieving the user query from `event.commonEventObject.parameters["autocomplete_widget_query"]`
3. Querying the data source with user input
4. Returning suggestions via `RenderActions` with a `modifyCard` object

**Limitation:** "The Chat app can suggest up to 100 items."

## Transferring Data Between Cards

To pass information between cards, developers use `actionParameters` in button widgets:

```javascript
parameters: [
  { key: "actionName", value: "submitDialog" },
  { key: "contactName", value: name },
  { key: "contactBirthdate", value: birthdate },
  { key: "contactType", value: type }
]
```

This enables multi-step forms where each card section can reference previous user inputs.

## Responding to Form Submissions

After receiving form data, apps can:
- Send confirmation messages
- Update existing cards
- Close dialogs
- Return error messages

Example response structure:
```javascript
{
  hostAppDataAction: {
    chatDataAction: {
      createMessageAction: {
        message: { text: "✅ Contact added" }
      }
    }
  }
}
```

## Prerequisites

**For HTTP endpoints:** A Google Workspace add-on extending Google Chat (via HTTP quickstart)

**For Apps Script:** A Google Workspace add-on extending Google Chat (via Apps Script quickstart)

## Error Troubleshooting

### "Unspecified error invoking the add-on"

This error typically indicates:
- Unhandled exceptions in the HTTP endpoint
- Response time exceeding 30 seconds
- Malformed or invalid JSON responses

The documentation notes: "Verify that your endpoint responds to requests within 30 seconds. If endpoint takes longer than 30 seconds to run, Chat can't process response and interaction fails."

## Technical Implementation Details

### Node.js, Python, Java, and Apps Script Support

The guide provides code examples in multiple languages for:
- Building multiselect menus with external data sources
- Querying external data based on user input
- Handling widget update payloads
- Transferring data between card steps
- Responding to form submissions

### Validation

While mentioned, the guide references validation functionality but directs readers to additional documentation: "Optionally, you can add validation to form input widgets, to ensure that users input and format information correctly."

## Related Resources

- [Design an interactive card or dialog](/workspace/chat/design-interactive-card-dialog)
- [Build Google Chat interfaces](/workspace/add-ons/chat/build)
- [Troubleshoot and fix Google Chat errors](/workspace/chat/troubleshoot)
- [Chat apps documentation](/workspace/add-ons/chat)
