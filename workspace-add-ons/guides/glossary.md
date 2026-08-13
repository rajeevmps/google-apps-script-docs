# Glossary

The following terms are used throughout this documentation.

### Calendar conferencing add-on

A special kind of add-on used to allow conferencing providers to present conferencing options in Google Calendar events. These add-ons require a well-developed conferencing solution for the add-on to connect to. Because of this requirement, most developers never have a need to create a Calendar conferencing add-on.

See Calendar conferencing add-ons for more information. Also see Upgrading your published add-ons for information on how to convert a Calendar conferencing add-on into a Google Workspace add-on.

### Card

A single "page" of an add-on UI. Cards are composed of different widget objects (buttons, text fields, headers, and so forth).

See Cards for more information.

### Card-based

An add-on whose user interface appears as a pane in the sidebar (or, on mobile, as another activity window reached through the menu). The add-on has a top toolbar that identifies the add-on and displays a card—essentially a "page" of the add-on's UI.

Google Workspace add-ons are card-based.

### Conference data

The set of information Google Calendar needs in order to let users create and join third-party conferences enabled by a Google Workspace add-on or Calendar conferencing add-on.

See Conference data for more information.

### Conference solution

A representation of a third-party conference that can be created from Google Calendar using Google Workspace add-on or Calendar conferencing add-on.

See Conference solutions for more information.

### Context

The current state of the host application. For example, which message currently open in Gmail, which Calendar event you are editing, or which Drive files you have selected are part of the host application's current context. Context, along with other information, is collected into an event object that is passed to the trigger function as a parameter.

### Contextual triggering

The practice of defining triggers that fire when the user enters a specific context, such as when they open an email thread in Gmail. Contextual triggering lets your add-on to provide a UI that is relevant to that context. Contextual triggers are configured in the add-on script project's manifest and thus are a type of _manifest trigger_.

### Editor add-ons

The original set of add-ons types that only allowed extensions of Google Docs, Sheets, Forms, or Slides. Editor add-ons are not card-based; rather, they required the developer to create a UI from raw HTML and CSS. Each editor add-on can only extend one host application.

See Editor add-ons for more details.

### Event object

The JSON object that is automatically created when homepages are requested, when the add-on enters contexts it needs to respond to, or as the result of user interactions with widgets in the add-on interface. Once created, event objects are passed to a specified trigger function or callback function. The purpose of event objects is to pass information from the user's client-side environment (such as information they've entered into the add-on interface widgets) to the add-on's server-side code, which then can act on that information and return the appropriate response.

See Event objects for more details.

### Gmail add-ons

An add-on that extends Gmail only. Gmail add-ons are card-based. Much of the functionality, behavior, and development details used to create Gmail add-ons is identical to the same details used to create Google Workspace add-ons.

See Gmail add-ons for more information. Also see Upgrading your published add-ons for information on how to convert a Gmail add-on into a Google Workspace add-on.

### Homepage

The root UI card of an add-on. Homepages are displayed when users open the add-on, and let your add-on show content outside of a specific context (for example, when the user is viewing their email threads in Gmail, but hasn't opened one). You define the appearance and behavior of your add-on homepage like any other card.

See Homepages for more information.

### Host or Host application

The Google Workspace application a Google Workspace add-on extends, such as Gmail or Google Calendar.

### HTML-based

An add-on whose user interface is defined using HTML and CSS instead of the Apps Script built-in Card service. Only older Editor add-ons are HTML-based.

### Link preview trigger

Link preview triggers fire when users interact with a third-party or non-Google URL within a Google host application, such as Google Docs. Link preview triggering lets you define URL patterns to preview from your service or API, and configure the preview content, including the smart chip and preview card. Link preview triggers are configured in the add-on script project's manifest and thus are a type of manifest trigger.

See Preview links with smart chips for more information.

### Manifest

A JSON file attached to an Apps Script project. The manifest is used to define project information the script needs to run correctly. For Google Workspace add-ons, the manifest is used to specify what hosts the add-on can extend and provide certain UI control settings.

### Manifest trigger

A trigger that is defined in a project's manifest, such as a homepage trigger or contextual trigger. Manifest triggers are used exclusively to create and display new cards when an add-on homepage is requested or the add-on enters a context that requires a display update.

Manifest triggers are distinct from other triggers in Apps Script because they aren't built-in (like simple triggers) and can't be created programmatically with the Apps Script Script service (like installable triggers).

### Non-contextual cards

Cards that show content when the user is outside a specific context; for example, when viewing their email threads in Gmail, but hasn't opened one. Homepages are a kind of non-contextual card.

### Sidebar

The section on the right of the host UI where a Google Workspace add-on's UI appears. Gmail and Editor add-ons can also define sidebars.

### Smart chip

A smart chip is a mention of a person, file, calendar event, or other entity within a Google Workspace application. When users hover over a chip, they can also preview additional content about the file or link. For example, when users hover over a chip to a Google Slides presentation, they see a screenshot of a slide, the owner of the presentation, and whether they've viewed the presentation before.

You can configure your add-on to use smart chips to preview links for a third-party or non-Google service. See Preview links in Google Docs.

### Trigger

A condition and automatic event response defined by an Apps Script project or add-on. Triggers fire when their associated event occurs (for example, when an add-on is opened) and cause a specified Apps Script function (the trigger function) to execute automatically. For Google Workspace add-ons, trigger functions often build new Cards in order to control what part of the add-on UI is displayed. Only certain event types can have triggers.

See add-on triggers for more information.

### Trigger function

An Apps Script function in a project that executes in response to a trigger being fired.

### Widget

A UI element such as a button, text field, or checkbox. Cards are constructed from a sequence of widget objects, defined by the Apps Script built-in Card service.

See Widgets for more information.

### Widget handler function

A function that links a particular widget to a particular action object. Each widget type has a set of defined widget handler functions it can use to connect to actions. Widget handler functions define what kind of user interaction triggers the resulting action, and are a crucial component of widget interactivity.

See Widget handler functions for more information.
