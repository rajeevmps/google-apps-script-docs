# Build Google Calendar interfaces

Google Workspace add-ons can provide customized interfaces when the user is viewing or editing calendars and Calendar events. This lets you provide the user with additional relevant information, automate tasks, and connect third-party systems to Calendar.

When building an Google Workspace add-on interface for Calendar, you can provide a homepage. You can use the same homepage for multiple hosts, or design a specific one for Calendar.

Your add-on can also define an interface that appears when the user has a Calendar event open.

## Access the add-on UI

Your UI can appear in several ways depending on the context. For example, an add-on can define a homepage interface, a Calendar event interface, an attachment selection interface, or all three:

- If a user clicks the add-on icon while in a calendar view, the add-on executes the corresponding `calendar.homepageTrigger` function (if present). This function builds and returns a homepage card to Calendar for display. If no `calendar.homepageTrigger` function is defined, a generic homepage card is displayed instead.
- If the user opens a Calendar event and then clicks the add-on icon, or the add-on is open when the user opens an event, the add-on executes the corresponding `eventOpenTrigger` function (if present). This function builds the add-on's Calendar event interface and returns to Calendar for display.
- If the add-on defines an `eventAttachmentTrigger` function, the add-on appears as an attachment provider when the user clicks Add attachment while editing a Calendar event. When the add-on is selected, the `eventAttachmentTrigger` function builds the add-on's attachment selection interface and returns it to Calendar for display.

## Build the add-on Calendar interface

Follow these steps to build your UI. You can extend Calendar with a Google Workspace add-on by following these steps:

1. Decide whether you want your add-on to have a Calendar-specific homepage. Also decide if you want to provide a custom interface while the user is editing Calendar events.
2. Add the appropriate `addOns.common` and `addOns.calendar` fields to the add-on script project manifest, including any scopes required.
3. If you are providing a Calendar-specific homepage, implement the `calendar.homepageTrigger` function to build this interface. You can also choose to use the `common.homepageTrigger` interface for multiple host applications.
4. If you are providing a Calendar event interface, implement a `calendar.eventOpenTrigger` function to build this interface. See Extending the Calendar event interface for details.
5. Implement the associated callback functions needed to respond to the user's UI interactions, such as button clicks.

## Calendar homepages

add-ons support displaying Google Workspace add-on homepages. To show your add-on's common homepage in Calendar, make sure there is an `addOns.calendar` field in the add-on's manifest.

Alternatively, add a `calendar.homepageTrigger` to the add-on manifest to provide a Calendar-specific homepage.

In either case, you must provide the name of a homepage trigger function in your add-on's script project. This function is automatically called to build the Calendar homepage when it is needed. Implement this function to build and return a single Card or an array of Card objects that make up the homepage. The homepage trigger function is passed an event object as a parameter that contains some general information such as the client's platform. Use the event object data to tailor the construction of the homepage.

## Extend the Calendar event interface

Calendar relies on a contextual trigger to determine what interface (if any) to display when the user edits a Calendar event. When the trigger fires, it executes the contextual trigger function specified by the `calendar.eventOpenTrigger` field in the add-on manifest.

Implement the function named in the `calendar.eventOpenTrigger` field. This function accepts an event object as an argument and must return either a single Card object or an array of Card objects for Calendar to display while the user has the event open.

### Event objects

An event object is created and passed to the `calendar.eventOpenTrigger` contextual trigger function when a user opens a Calendar event. The trigger function can use the information in this event object to determine how to construct add-on cards or control the add-on behavior. Event objects are also created and passed to homepageTrigger functions when an add-on is first opened, and when the user clicks or selects interactive widgets.

Note: The term "event" in "event object" refers to an action taken by the user in the add-on UI and its associated response, not a Calendar event. To keep the distinction clear, events in Calendar are always referred to as "Calendar events" in this documentation.

The full structure of event objects is described in Event objects. When Calendar is the acting host app of the add-on, contextual trigger and widget interaction event objects include the Calendar event object field that carries Calendar-specific client information.

## Update Calendar events

In addition to the contextual `calendar.eventOpenTrigger` that fires when a user opens a Calendar event for editing, you can also define an `calendar.eventUpdateTrigger` that fires when the user updates and saves a Calendar event. This trigger only fires if the user makes one or more of the following edits:

- Adds one or more attendees.
- Removes one or more attendees.
- Adds or switches to a different conferencing solution.

When this trigger fires, it executes the trigger function specified by the `calendar.eventUpdateTrigger` manifest field. The function is executed before the Calendar event edit is saved.

The `calendar.eventUpdateTrigger` is typically used to do one or more of the following:

- Update the add-on's Calendar event interface in response to user changes to the Calendar event.
- Sync Calendar event data with a third-party system, such as a conferencing system that is connected to Calendar.

If you need your add-on to make adjustments to a Calendar event's data (such as its attendee list), set the add-on `calendar.currentEventAccess` manifest field to `WRITE` or `READ_WRITE`. This also requires the add-on to have the `https://www.googleapis.com/auth/calendar.addons.current.event.write` scope.

## Add conferencing solutions

If you maintain a third-party conferencing system, you can integrate it with Calendar by adding conferencing solutions. This feature was previously in beta as Calendar conferencing add-ons.

Conferencing solutions represent third-party conference options that users can attach to Calendar events. The Third-party conferencing overview documentation provides details on how to build an add-on that adds new conferencing solutions. It isn't necessary to build a UI for this type of extension; added solutions appear as options in the drop-down menu of the Calendar event UI.
