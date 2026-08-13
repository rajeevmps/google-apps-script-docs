# Extend Gmail with Google Workspace add-ons

The purpose of many emails is to get the recipient to do a specific task or reach a goal, such as adding a calendar event, filling out a form, making a reservation, or using other applications. However, recipients then have to complete the task without any further prompting, often doing a number of manual steps.

You can save time and effort for your users by automating these tasks with add-ons. When a user reads or composes a message in Gmail, a Google Workspace add-on can present an interactive, customized UI that lets the user act on the message in various ways, such as by:

- Displaying additional information for the user in the Gmail UI.
- Connecting to non-Google services, to retrieve information or take other actions.
- Providing the means to control the add-on behavior or send information to another service.

Note: You can also develop your own Chat apps to enhance the Gmail experience.

add-ons can define the following kinds of extensions within Gmail:

- Homepages and other non-contextual cards.
- Contextual interfaces that appear when users open Gmail messages.
- Contextual interfaces that appear when a user composes a message or reply.
- Automatically create new message drafts in response to user interactions.

Additionally, add-ons that extend Gmail do so on both desktop and mobile clients.

## Gmail homepages

Gmail supports displaying add-on homepages. To show your add-on's common homepage in Gmail, make sure there is a addOns.gmail field in the add-on's manifest.

Alternatively, add a gmail.homepageTrigger to the add-on manifest to provide a Gmail-specific homepage.

In either case, you must provide the name of a homepage trigger function in your add-on's script project. This function is automatically called to build the Gmail homepage when it is needed. You must implement this function to build and return a single Card or an array of Card objects that make up the homepage. The homepage trigger function is passed an event object as a parameter that contains some general information such as the client's platform. You can use the event object data to tailor the construction of the homepage.

## See what you can make

You can build add-ons using Apps Script, and define their interfaces using the Apps Script Card service. See Building Google Workspace add-ons for an overview. Google Workspace add-on behavior is configured using a manifest, which includes Gmail-specific sections.

When configuring your add-on to extend Gmail, you must decide what interfaces to create for your add-on and what actions it can take. See the following guides for more information:

- Extending the message UI
- Extending the compose UI with compose actions
- Compose draft messages
- Manifests
- Gmail scopes

Try a sample:

- Analyze and label Gmail messages with Gemini and Vertex AI
- Plan travels with an AI agent accessible across Google Workspace
- Build Gemini Enterprise agents that are tightly integrated with Google Workspace data stores, APIs, and add-ons
- Build Vertex AI agents that are tightly integrated with Google Workspace data stores, APIs, and add-ons
