# Build Google Workspace add-ons

Learn how to design, build, and publish Google Workspace add-ons:

1. Determine the Google Workspace applications where you want your add-on to be available to users.
2. Set up your add-on's projects and choose an owner and collaborators.
3. Design and configure your add-on's appearance and behavior.
4. Build the add-on.
5. Verify your add-on's OAuth scopes.
6. Test the add-on within one or more Google Workspace applications.
7. Publish the add-on.

Build an add-on with Apps Script or HTTP. To compare the two, watch the video "Apps Script vs. HTTP endpoints: Which should you choose? 🤔".

## Choose Google Workspace host applications

You can configure Google Workspace add-ons to appear in the following Google Workspace host applications:

- Gmail
- Google Calendar
- Google Chat
- Google Docs
- Google Drive
- Google Meet
- Google Sheets
- Google Slides

To build for Google Workspace applications, see [Extend the Google Workspace UI](/workspace/extend).

## Set up your add-on's projects and choose an owner and collaborators

If you build your add-on in Apps Script, you create both an Apps Script project and a Google Cloud project. If you build your add-on in a language other than Apps Script, you only need to create a Google Cloud project.

To build an add-on, you must configure both a script project and a Cloud project.

Before starting add-on development, choose a single user account to _own_ the projects and decide which other accounts are collaborators. The owner of the projects creates and manages the project files and associated settings, while collaborators can help with coding and testing.

**Warning:** If you don't add collaborators to your add-on projects, transfer ownership of them before the owner's account is shut down or removed. Otherwise, you might lose access to the add-on code and settings.

### Apps Script projects

Before building your add-on, review the [Apps Script quotas and limitations](/apps-script/guides/services/quotas) to align your project design with these guidelines. Apps Script is best for lightweight development of personal or internal add-ons with a small user base. If your add-on requires support for many users, low latency, or full control over your infrastructure, consider a [different runtime](/workspace/add-ons/guides/alternate-runtimes).

Build your add-on's Apps Script project files in a [shared drive](/apps-script/collaborating#collaborating_with_shared_drives) so that no single account has sole ownership. Placing your add-on script file in a shared drive ensures that all collaborators have access to the script project.

When you publish an add-on, a single user account is the publisher. The publishing account must have edit access to the script project, but it doesn't need to be the owner.

To create an Apps Script project, see [Script projects](/apps-script/guides/projects#create-and-delete).

### Google Cloud projects

Add collaborators to the [add-on's Cloud project](/apps-script/guides/cloud-platform-projects#adding_additional_owners_to_a_standard_gcp_project). This ensures that your team can always access the add-on's Cloud settings.

To create a Google Cloud project, see [Create a Google Cloud project](/workspace/guides/create-project).

## Design and configure your add-on appearance and behavior

Decide how your add-on looks and behaves before you build it. Consider which use cases the add-on solves. Start with a basic design to get working first, and then add refinements.

**Tip:** Start with a basic [homepage card](/workspace/add-ons/concepts/homepages), then add more widgets, cards, navigation, and other behavior. Consider contextual cards that a user action in the host application triggers, like opening a [Gmail message thread](/workspace/add-ons/gmail/extending-message-ui) or [Calendar event](/workspace/add-ons/calendar/building-calendar-interfaces#extending_the_event_interface).

Refer to the [Google Workspace add-on style guide](/workspace/add-ons/guides/workspace-style) for guidelines on how to design your add-on user experience.

### Configure the add-on manifest

Implement the design in the add-on manifest. Configure the add-on's appearance and behavior in the manifest, including the Google Workspace host applications that the add-on extends.

For details, see [Manifests for Google Workspace add-on](/workspace/add-ons/concepts/workspace-manifests).

As you add code and features, update the manifest as needed to define the required add-on appearance and behavior.

### Configure Google Chat app appearance and behavior

If you design an add-on that extends Google Chat, use Google Chat API to configure the appearance and behavior of a Chat app. For steps, see [Configure a Google Chat app](/workspace/add-ons/chat/configure).

## Build the add-on

Implement a card-based interface for the add-on. Use [Card service](/apps-script/reference/card-service/card-service) or if you use another code language, return formatted JSON for the interface to render as cards.

Implement any [trigger functions](/workspace/add-ons/guides/glossary#trigger_function) specified in the add-on manifest. If your add-on connects to a third-party service using OAuth, [configure the OAuth for that service](/workspace/add-ons/how-tos/non-google-services).

### Construct cards

Define an add-on user interface by creating [`Card`](/apps-script/reference/card-service/card) objects and adding [widgets](/workspace/add-ons/concepts/widgets). Trigger functions specified in your manifest must return either a single [`Card`](/apps-script/reference/card-service/card) object or an array of [`Card`](/apps-script/reference/card-service/card) objects that represent different 'pages' of the add-on interface. The add-on can also create and display new cards in response to user actions.

In Apps Script, create cards using the [`CardBuilder`](/apps-script/reference/card-service/card-builder) class. Each card requires a [`CardHeader`](/apps-script/reference/card-service/card-header) and one or more [`CardSections`](/apps-script/reference/card-service/card-section). Populate each card section with the individual widgets that make up the interface. [Interaction widgets](/workspace/add-ons/concepts/widgets#user_interaction_widgets) are usually linked to [actions](/workspace/add-ons/concepts/actions) to define their interaction behavior.

After you have added all the sections and widgets to your card via its [`CardBuilder`](/apps-script/reference/card-service/card-builder), call [`CardBuilder.build`](/apps-script/reference/card-service/card-builder#build\(\)) to create the corresponding `Card` object.

**Note:** Failing to call `build` after using builder classes in the [Card service](/apps-script/reference/card-service/card-service) results in type errors. Trigger functions must return [`Card`](/apps-script/reference/card-service/card) objects. Returning [`CardBuilder`](/apps-script/reference/card-service/card-builder) objects results in an error.

Use built-in [Apps Script services](/apps-script/guides/services/) such as [`CalendarApp`](/apps-script/reference/calendar/calendar-app) to retrieve information to display in the add-on cards. Use data from non-Google services.

If your add-on needs access to non-Google APIs that require OAuth, configure and connect to that service—see the [Connecting to Non-Google Services guide](/workspace/add-ons/how-tos/non-google-services).

#### Construction order

When you build a card, build from the top up. Use this construction order:

1. Build the widget.
2. Add the widget to card section.
3. Repeat until the card section has all of its widgets.
4. Add the card section to the card.

This is because when you add a widget to a card or card section, you are actually adding a _copy_ of that widget. Any changes you make to the widget object after adding it are not reflected in the final card.

**Warning:** Add a widget to a card or card section after you build it. Add a card section to a card after it's fully populated with widgets. Don't change widgets or sections after they are added. To change an added widget, recreate the section or card.

### Universal actions

Use [universal actions](/workspace/add-ons/how-tos/universal-actions) to provide context-independent functionality. Universal actions are menu items available in the add-on UI regardless of the card. All defined universal actions appear in the add-on's card menu.

See [Universal actions](/workspace/add-ons/how-tos/universal-actions) for more details.

## Verify the add-on OAuth scopes

[Scopes](/workspace/add-ons/concepts/workspace-scopes) define the actions the add-on can take on a user's behalf. Add-ons should only have the scopes they need to function.

In add-on projects, [set the add-on scopes](/apps-script/concepts/scopes#setting_explicit_scopes) to ensure the add-on uses the least-permissive set of scopes possible. Define the scopes in the add-on [manifest](/workspace/add-ons/concepts/workspace-manifests).

See [Scopes](/workspace/add-ons/concepts/workspace-scopes) for more details.

## Test the add-on

You can test unpublished add-ons by first [installing the unpublished add-on](/workspace/add-ons/how-tos/testing-workspace-addons#install_an_unpublished_add-on). After it's installed and authorized, use the add-on in your account to test its appearance and behavior in the host applications it extends. Verify that the add-on behaves as expected for contexts and user actions.

To start testing your add-on, see the following guides:

- [Test and debug Apps Script Google Workspace add-ons](/workspace/add-ons/how-tos/testing-workspace-addons)
- [Test and debug HTTP Google Workspace add-ons](/workspace/add-ons/guides/debug)
- [Test interactive features for Google Chat apps](/workspace/chat/test-interactive-features)

## Publish the add-on

Publishing makes your add-on available to others. Before you publish, review the [publication overview](/workspace/add-ons/how-tos/publish-add-on-overview). Publication is a complex process that requires preparation.

Google Workspace add-ons are published to the [Google Workspace Marketplace](https://workspace.google.com/marketplace/). Publicly available add-ons require [app review](/workspace/marketplace/about-app-review) before they are published.

See [Publishing Google Workspace add-on](/workspace/add-ons/how-tos/publish-add-on-overview) for more details.
