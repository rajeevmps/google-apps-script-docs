# Triggers for Google Workspace add-ons

[Apps Script triggers](/apps-script/guides/triggers) cause a specified script function (the *trigger function*) to execute whenever a specified event occurs. Only certain events can cause triggers to fire, and each Google Workspace application supports a different set of events.

When a trigger fires, an *event object* is created. This JSON structure contains details about the event that occurred. The information in the event object structure is organized differently based on the trigger type.

Once the event object is created, Apps Script passes it as a parameter to the trigger function. The trigger function is a callback function that you must implement yourself, to take whatever actions are appropriate to respond to the event. For example, in a Google Workspace add-on that extends Gmail, you can define a trigger that creates a new card interface when the user opens a message thread. In this case, you implement a contextual callback function to create the cards making up the new UI using the data passed in the [event object](/workspace/add-ons/concepts/event-objects).

This page provides guidelines on using triggers in Google Workspace add-on projects.

## Manifest triggers

Unlike Editor add-ons, Google Workspace add-ons can't use Google Apps Script [simple triggers](/apps-script/guides/triggers). Instead, they use triggers designed specifically for Google Workspace add-ons: *manifest triggers*.

Manifest triggers are defined in the Google Workspace add-on [manifest](/workspace/add-ons/concepts/workspace-manifests). Examples include:

- **Homepage triggers** that build and display the add-on homepage.
- **Google Calendar eventOpen triggers** that display a new card or take other actions when an event is opened.
- **Calendar eventUpdate triggers** that display a new card or take other actions when a user edits and saves an event.
- **Google Drive onItemsSelected triggers** that display a new card or take other actions when a user selects files or folders.
- **Gmail compose triggers** that display an add-on card when the user opens the add-on in the compose window.
- **Gmail contextual triggers** that display a new card or take other actions when the user opens a message.
- **Editor onFileScopeGranted triggers** that display a new card when users grant authorization for the `drive.file` OAuth scope in the document.

In the list, only homepage triggers are non-contextual; the rest are contextual. See [Manifest](/workspace/add-ons/concepts/workspace-manifests) for more information about manifest trigger definitions.

In addition to manifest triggers, Google Workspace add-ons can use Apps Script [installable triggers](/apps-script/guides/triggers/installable).

### Restrictions

Manifest triggers have certain restrictions to their use.

- These triggers are only used in Google Workspace add-on projects.
- Since they are defined in the add-on manifest and not in code, you can't use the Apps Script [`Script`](/apps-script/reference/script) service to create or modify them.
- Gmail contextual triggers fire for every email message, regardless of content.
- Each add-on can only have one trigger of each type, per user, per document.
