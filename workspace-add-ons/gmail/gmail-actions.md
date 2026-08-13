# Gmail actions

Action objects let you build interactive behavior into Google Workspace add-ons. They define what happens when a user interacts with a widget (for example, a button) in the add-on UI.

An action is attached to a given widget using a widget handler function, which also defines the condition that triggers the action. When triggered, the action executes a designated callback function. The callback function is passed an event object that carries information about the user's client-side interactions. You must implement the callback function and have it return a specific response object.

For example, say you want a button that builds and displays a new card when clicked. For this, you must create a new button widget and use the button widget handler function `setOnClickAction(action)` to set a card-building Action. The Action you define specifies an Apps Script callback function that executes when the button is clicked. In this case, you implement the callback function to build the card you want and return an `ActionResponse` object. The response object tells the add-on to display the card the callback function built.

This page describes Gmail-specific widget actions you can include in your add-on.

## Gmail interactions

Google Workspace add-ons that extend Gmail can include an additional Gmail-specific widget action to compose draft messages. This action requires the associated action callback function to return a specialized response object:

| Action attempted | Callback function should return |
|---|---|
| Compose draft messages | `ComposeActionResponse` |

To use these widget actions and response objects, the Google Workspace add-on must include the `https://www.googleapis.com/auth/gmail.addons.current.action.compose` scope in its manifest.

### Compose a message

Add-ons that extend Gmail can define a widget that, when interacted with, generates draft messages in Gmail (either new messages or replies). To do this, associate the triggering widget with a callback function that returns a `ComposeActionResponse` object. When the callback function finishes executing, Gmail uses this response object to open and populate a draft compose window.

For more details and an example, see Compose draft messages.

Note: This behavior is distinct from extending the compose window UI. In that case the add-on is creating a contextual card interface alongside the compose window. Here, a draft is generated in response to a widget interaction.
