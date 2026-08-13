# Workspace Add-ons — Index

Google Workspace Add-ons are Apps Script (or Cloud Function / HTTP-backed) projects that extend Gmail, Calendar, Drive, Docs/Sheets/Slides/Forms, Chat, and Meet with a common Card-based UI, installable from the Google Workspace Marketplace. This tree covers the conceptual and platform-specific guides for building them, sourced from `developers.google.com/workspace/add-ons/`. It is a separate but related doc tree from core Apps Script — the UI is built with the same [Card Service](../reference/card-service/README.md) / [Add-ons Response Service](../reference/add-ons-response-service/README.md) classes documented under `reference/`.

## Concepts

- [Cards](concepts/cards.md) · [Card Interfaces](concepts/card-interfaces.md) · [Widgets](concepts/widgets.md)
- [Homepages](concepts/homepages.md) · [Types](concepts/types.md) · [Actions](concepts/actions.md)
- [Dialogs](concepts/dialogs.md) · [Menus](concepts/menus.md) · [HTML Interfaces](concepts/html-interfaces.md)
- [Event Objects](concepts/event-objects.md)
- [Workspace Manifests](concepts/workspace-manifests.md) · [Workspace Scopes](concepts/workspace-scopes.md) · [Workspace Triggers](concepts/workspace-triggers.md)
- [Editor Manifests](concepts/editor-manifests.md) · [Editor Scopes](concepts/editor-scopes.md) · [Editor Triggers](concepts/editor-triggers.md) · [Editor Auth Lifecycle](concepts/editor-auth-lifecycle.md)

## General guides

- [Starting Add-ons](guides/starting-addons.md) · [Using Add-ons](guides/using-addons.md)
- [Building Workspace Add-ons](guides/building-workspace-addons.md) · [Building Editor Add-ons](guides/building-editor-addons.md)
- [Interactions](guides/interactions.md) · [Navigation](guides/navigation.md)
- [Universal Actions](guides/universal-actions.md) · [Suggestions & Autocomplete](guides/suggestions-autocomplete.md)
- [Preview Links & Smart Chips](guides/preview-links-smart-chips.md)
- [Access User Locale/Timezone](guides/access-user-locale-timezone.md)
- [Build HTTP Endpoints](guides/build-http-endpoints.md)
- [Workspace Style Guide](guides/workspace-style-guide.md)

## Gmail add-ons

- [Overview](gmail/overview.md) · [Gmail Actions](gmail/gmail-actions.md)
- [Compose](gmail/compose.md) · [Extending Compose UI](gmail/extending-compose-ui.md) · [Extending Message UI](gmail/extending-message-ui.md)

## Calendar add-ons

- [Overview](calendar/overview.md) · [Building Calendar Interfaces](calendar/building-calendar-interfaces.md) · [Calendar Actions](calendar/calendar-actions.md)
- [Attachments — Providing Icons](calendar/attachment/providing-icons.md)
- Conferencing: [Overview](calendar/conferencing/overview.md) · [Build Conference Add-ons](calendar/conferencing/build-conference-addons.md) · [Create Conference](calendar/conferencing/create-conference.md) · [Add Settings](calendar/conferencing/add-settings.md) · [Providing Logos](calendar/conferencing/providing-logos.md) · [Sync Calendar Changes](calendar/conferencing/sync-calendar-changes.md) · [Sample](calendar/conferencing/conferencing-sample.md)

## Drive add-ons

- [Overview](drive/overview.md) · [Building Drive Interfaces](drive/building-drive-interfaces.md) · [Drive Actions](drive/drive-actions.md)

## Editor add-ons (Docs/Sheets/Slides/Forms)

- [Overview](editors/overview.md) · [Building Editor Interfaces](editors/building-editor-interfaces.md) · [Editor Actions](editors/editor-actions.md)
- [Docs Overview](editors/docs-overview.md) · [Docs Quickstart: Translate](editors/docs-quickstart-translate.md)
- [Sheets Overview](editors/sheets-overview.md)
- [Slides Overview](editors/slides-overview.md) · [Slides Quickstart: Translate](editors/slides-quickstart-translate.md)
- [Forms Overview](editors/forms-overview.md) · [Forms Quickstart: Notifications](editors/forms-quickstart-notifications.md)

## Chat apps

- [Overview](chat/overview.md) · [Build](chat/build.md) · [Configure](chat/configure.md)
- [Commands](chat/commands.md) · [Dialogs](chat/dialogs.md) · [Send Messages](chat/send-messages.md)
- [Collect Information](chat/collect-information.md) · [Preview Links](chat/preview-links.md) · [Convert](chat/convert.md)
- Quickstarts: [Apps Script](chat/quickstart-apps-script.md) · [HTTP](chat/quickstart-http.md) · [Pub/Sub](chat/quickstart-pubsub.md) · [Dialogflow ES](chat/quickstart-dialogflow-es.md) · [Dialogflow CX](chat/quickstart-dialogflow-cx.md) · [ADK Agent](chat/quickstart-adk-agent.md) · [A2A Agent](chat/quickstart-a2a-agent.md) · [A2UI Agent](chat/quickstart-a2ui-agent.md) · [Generative AI Agent](chat/quickstart-ge-agent.md)

## Meet add-ons

- [Overview](meet/overview.md) · [Concepts](meet/concepts.md) · [Quickstart](meet/quickstart.md)
- [Deploy Add-on](meet/deploy-add-on.md) · [Use Add-on](meet/use-add-on.md) · [Collaborate in the Add-on](meet/collaborate-in-the-add-on.md)

## Publishing

- [Overview](publish/overview.md) · [Update a Published Add-on](publish/update-published-add-on.md)

## Quickstarts (general)

- [Cats Quickstart (Apps Script)](quickstart/cats-quickstart-apps-script.md) · [Node.js Quickstart](quickstart/nodejs-quickstart.md)
