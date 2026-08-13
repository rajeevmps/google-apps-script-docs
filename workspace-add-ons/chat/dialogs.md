# Build interactive dialogs

## Overview
Google Chat app dialogs are interactive, windowed interfaces that display card-based UIs for collecting user information. These dialogs are exclusive to the user who opened them and support multi-step form processes.

## Key Features
- **Dialog triggers**: Dialogs can be initiated through slash commands (with "Opens a dialog" checkbox enabled) or button clicks with `OPEN_DIALOG` interaction
- **Card-based interface**: Dialogs utilize cards containing form inputs and widgets
- **Multi-step support**: Apps can display sequential dialogs for complex workflows
- **Response handling**: Upon submission, apps either close the dialog or display another dialog

## Prerequisites
**HTTP**: Requires a Google Workspace add-on extending Google Chat, built via the HTTP quickstart

**Apps Script**: Requires a Google Workspace add-on extending Google Chat, built via the Apps Script quickstart

## Implementation Steps

### Trigger Dialog Request
- Configure commands with the "Opens a dialog" checkbox
- Set button `onClick.action.interaction` to `"OPEN_DIALOG"`
- Pass `FUNCTION_URL` to handle interactions

### Open Initial Dialog
When receiving `dialogEventType` of `REQUEST_DIALOG`, return a `RenderActions` object with `pushCard` navigation containing form widgets (text inputs, date pickers, selection inputs) and a submit button.

### Handle Submission
Apps receive `ButtonClickedPayload` with `dialogEventType` set to `SUBMIT_DIALOG`. Response options include:

1. **Return another dialog**: Process form data and display a new card for multi-step flows
2. **Close dialog**: Return `EndNavigation` with action `"CLOSE_DIALOG"`

### Optional Enhancements
- Display temporary notifications when closing
- Send confirmation Chat messages
- Validate submitted data before processing
- Transfer data between dialogs using action parameters

## Code Examples Provided
The documentation includes complete code samples in:
- Node.js
- Python
- Java
- Apps Script

All samples demonstrate a contact management workflow with initial form, confirmation step, and submission handling.

## Status
Currently part of the Google Workspace Developer Preview Program; requires specific setup in Google Cloud Functions or Apps Script environments.
