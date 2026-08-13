# Extend Google Calendar with Google Workspace add-ons

Calendar provides tools for users to create, manage, and share event and calendar details. Managing complex calendars can be time-consuming when viewing, creating, updating, and sharing individual events, especially when importing or exporting event information from other applications.

Save time and effort for your users by extending Calendar with add-ons. When you build a Google Workspace add-on, you can define interfaces inserted directly into Calendar, exactly where the user needs them. These interfaces automate calendar tasks, present additional information, or let the user interact with a third-party system without switching browser tabs.

Add-ons can define the following kinds of extensions within Calendar:

- Non-contextual homepages.
- Contextual interfaces that appear when users click an event in the calendar view.
- Contextual interfaces that appear when users open an event to view or edit it.
- Custom conferencing solutions for Calendar events (see Third-party conferencing overview for details).

Calendar add-ons aren't supported on mobile clients.

## See what you can make

add-ons are built using Google Apps Script, and their interfaces defined using the Apps Script Card service. See Building add-ons for an overview. Add-on behavior is configured using a manifest, which includes Calendar-specific sections.

When configuring your Google Workspace add-on to extend Calendar, you must decide what interfaces to create and what actions it can take. The following guides provide more information:

- Building Calendar interfaces
- Calendar actions
- Manifests

Try a sample:

- Plan travels with an AI agent accessible across Google Workspace
- Build Gemini Enterprise agents that are tightly integrated with Google Workspace data stores, APIs, and add-ons
- Build Vertex AI agents that are tightly integrated with Workspace data stores, APIs, and add-ons

If you maintain a conferencing system, see Third-party conferencing overview for details on how to integrate your conference types within Calendar.
