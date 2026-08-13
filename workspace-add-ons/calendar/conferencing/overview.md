# Third-party conferencing overview

Note: This functionality was built for conference providers specifically, and was originally available as Calendar conferencing add-ons.

When creating or editing a Google Calendar event, users have the option to create a Google Meet meeting and associate it with the event. Once added, event attendees can join the associated Meet with a click.

However, if a user wants to use a third-party conference (such as WebEx) instead of Meet, the process is more complex. Typically this requires the user to create the conference outside of Calendar and then copy a conference code into the Calendar event description. Event attendees then must follow a specific set of steps to enter the conference using the code provided.

Google Workspace add-ons can help users avoid this complexity. You can build a Google Workspace add-on that extends Calendar with third-party conference solutions. Each added conference solution adds a new conferencing option for Calendar events, allowing users to create and join those conferences directly from Calendar.

If you are a conference provider, you can create a Google Workspace add-on to define a connection between Calendar and your product. You can then publish the add-on in the Google Workspace Marketplace, where users and administrators can discover and install it.

## Conference solutions

A conference solution represents a type of third-party conference that users can join. Each solution is shown as a conferencing option a user can choose when creating or editing a Calendar event.

Examples of conference solutions an add-on might define include the following:

- A standard video conference.
- An audio-only conference.
- A personal conference.
- A publicly streamed conference.

Any type of conference that the third-party service provides can have an associated solution, and collections of solutions can be bundled together in a single add-on.

## How conference solutions work

When a conference solution is added to a add-on, there is no need to provide a detailed UI for it. Instead, whenever a user creates or edits a Calendar event, any solutions defined in the add-ons the user has installed appear as conferencing options.

When a user selects a conference solution, the add-on connects to the third-party conferencing system using its API and creates the conference, syncing data between the conference and the Calendar event. If the event is later updated or deleted, the add-on detects this and makes the corresponding updates on the conferencing system. Once a conference is attached to an event, attendees can join the conference from Calendar.

Optionally, the add-on can provide a settings page to allow users to control specific conferencing behavior.

## Conference data

Google Workspace add-ons that provide conference solutions to Calendar require specific information—conference data—to let users join third-party conferences. When you define a conference solution in your add-on, you specify an `onCreateFunction` that builds and returns a `ConferenceData` object. The `ConferenceData` object must contain either all the conference data Calendar needs, or a `ConferenceError` object that describes an error that occurred when communicating with the third-party conferencing system.

The following table describes each type of conference data your add-on can use and lists the `ConferenceData` service object that represents it. Each `ConferenceData` object your add-on uses must have all elements marked as Required:

| Component | Type | Description |
|---|---|---|
| Conference errors | `ConferenceError` | Required if an error occurred, in which case no other data is needed. Use this to report a problem that happened when the add-on tried to connect to the conferencing system. |
| Conference ID | string | Required if not an error. Use this ID to identify the conference within the third-party conferencing system. |
| Conference parameters | `ConferenceParameter[]` | Use these key-value pairs to pass any system-specific information to and from the third-party conferencing system. For example, the system may require the email of the conference moderator, or a meeting key. |
| Conference notes | string | Use this to append a text notice to the conference. Typically you use these to add instructions for conference administrators or legal notices. |
| Entry points | `EntryPoint[]` | Required if not an error, in which case at least one `EntryPoint` must be defined. Use EntryPoints to describe a specific way to join the conference (for example, by phone, video, or SIP). Each entry point requires a URI and an `EntryPointType`. |

## Further reading

The following documentation can help you learn more:

- Build a add-on with conference solutions. Build conference add-ons provides an overview of the steps required to build a add-on that implements third-party conference solutions.
- Get a closer look. View the source code of a conferencing add-on example.
- Learn more about what Apps Script can do. Review the Google Apps Script documentation.
- Wondering what other developers have built? Visit the Google Workspace Marketplace for Calendar.
