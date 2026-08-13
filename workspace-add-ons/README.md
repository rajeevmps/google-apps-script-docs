# Workspace Add-ons Documentation — Index

Google Workspace Add-ons are a separate but closely related platform to plain Apps Script. A plain Apps Script project runs standalone or bound to a single Sheet/Doc/Form. A **Workspace Add-on** is instead a manifest-declared extension that can attach itself to Gmail, Calendar, Drive, Chat, Meet, and the Docs/Sheets/Slides/Forms editors simultaneously, rendering its UI as **Cards** (built with `CardService`) inside a common side-panel host, and reacting to **triggers** (homepage triggers, contextual triggers, event-driven triggers) fired by the host app. Add-ons can be built either as Apps Script projects (using the same `CardService` / `Card` / `Widget` classes documented under `reference/card-service/` in this repo) or as plain HTTP/Cloud Function endpoints that receive JSON event payloads and return JSON card responses — the "alternate runtimes" model used by Node.js, Python, etc. Chat apps and Meet add-ons extend the same card/event model to Google Chat and Google Meet respectively. This tree is the conceptual and platform-specific guide content for that whole surface, mirrored from `developers.google.com/workspace/add-ons/` (plus a handful of Meet SDK pages from `developers.google.com/meet/add-ons/`). It complements, but does not duplicate, the `CardService`/`Card`/`Widget` class reference already mirrored elsewhere in this repo.

**101 files** across 10 subfolders (100 content pages + this index).

## concepts/ (17 files)

Cross-cutting building blocks shared by every add-on host (Gmail, Calendar, Drive, Chat, and the Editors).

- [types.md](concepts/types.md) — The two add-on types (Google Workspace add-ons vs. Editor add-ons) and when to use each.
- [card-interfaces.md](concepts/card-interfaces.md) — Overview of the card-based UI framework common to all add-on surfaces.
- [cards.md](concepts/cards.md) — How to construct `Card` objects: headers, sections, fixed footers, card navigation stacks.
- [widgets.md](concepts/widgets.md) — Catalog of widget types (text, image, buttons, inputs, selection controls) usable inside a card.
- [homepages.md](concepts/homepages.md) — Building the homepage card shown when a user opens an add-on with no specific context.
- [actions.md](concepts/actions.md) — `Action` objects: attaching click/interaction handlers to widgets and returning response objects.
- [event-objects.md](concepts/event-objects.md) — Full field reference for event objects passed to callbacks, broken out per host (Calendar, Chat, Drive, Gmail, Docs/Sheets/Slides).
- [workspace-triggers.md](concepts/workspace-triggers.md) — Homepage and contextual triggers available to Workspace add-ons.
- [workspace-manifests.md](concepts/workspace-manifests.md) — Manifest file structure (`appsscript.json` and HTTP manifest JSON) for Workspace add-ons.
- [workspace-scopes.md](concepts/workspace-scopes.md) — OAuth scopes available to Workspace add-ons, with scope tables.
- [editor-auth-lifecycle.md](concepts/editor-auth-lifecycle.md) — Authorization mode lifecycle (`AuthMode.NONE`/`LIMITED`/`FULL`) specific to Editor add-ons.
- [editor-manifests.md](concepts/editor-manifests.md) — Manifest fields specific to Editor add-ons (brief stub linking to the full manifest reference).
- [editor-scopes.md](concepts/editor-scopes.md) — OAuth scopes available to Editor add-ons.
- [editor-triggers.md](concepts/editor-triggers.md) — Triggers usable in Editor add-ons (`onOpen`, `onInstall`, `onEdit`, etc.) and their restrictions.
- [html-interfaces.md](concepts/html-interfaces.md) — Overview/stub for building Editor add-on UI with classic HTML-service menus, dialogs, and sidebars.
- [menus.md](concepts/menus.md) — Custom Editor add-on menu items (brief stub).
- [dialogs.md](concepts/dialogs.md) — Add-on dialogs and sidebars built with HTML service for Editor add-ons.

## gmail/ (5 files)

- [overview.md](gmail/overview.md) — What Gmail add-ons can do and how they attach to the Gmail UI.
- [extending-message-ui.md](gmail/extending-message-ui.md) — Building contextual card interfaces shown alongside an open email message.
- [extending-compose-ui.md](gmail/extending-compose-ui.md) — Building contextual card interfaces shown while composing a message.
- [compose.md](gmail/compose.md) — Programmatically composing draft messages from an add-on.
- [gmail-actions.md](gmail/gmail-actions.md) — Gmail-specific actions (e.g. updating a draft) available to add-on cards.

## calendar/ (11 files)

- [overview.md](calendar/overview.md) — What Calendar add-ons can do and how they attach to the Calendar UI.
- [building-calendar-interfaces.md](calendar/building-calendar-interfaces.md) — Building contextual card interfaces shown alongside a calendar event.
- [calendar-actions.md](calendar/calendar-actions.md) — Calendar-specific actions available to add-on cards.
- [attachment/providing-icons.md](calendar/attachment/providing-icons.md) — Supplying icons for event attachments created by an add-on.
- [conferencing/overview.md](calendar/conferencing/overview.md) — Overview of the third-party conferencing add-on system (Calendar's "Add conferencing" dropdown).
- [conferencing/build-conference-addons.md](calendar/conferencing/build-conference-addons.md) — End-to-end guide to building a conferencing add-on.
- [conferencing/create-conference.md](calendar/conferencing/create-conference.md) — Handling the `onCreateConference` callback to generate new conference data.
- [conferencing/sync-calendar-changes.md](calendar/conferencing/sync-calendar-changes.md) — Keeping conference data in sync when a calendar event changes.
- [conferencing/add-settings.md](calendar/conferencing/add-settings.md) — Adding a per-conference settings UI for organizers.
- [conferencing/providing-logos.md](calendar/conferencing/providing-logos.md) — Supplying conference solution logos shown in the Calendar UI.
- [conferencing/conferencing-sample.md](calendar/conferencing/conferencing-sample.md) — Full worked sample (CreateConf.gs, Syncing.gs, appsscript.json) for a conferencing add-on.

## drive/ (3 files)

- [overview.md](drive/overview.md) — What Drive add-ons can do and how they attach to the Drive UI.
- [building-drive-interfaces.md](drive/building-drive-interfaces.md) — Building contextual card interfaces shown when a file is selected in Drive.
- [drive-actions.md](drive/drive-actions.md) — Drive-specific actions available to add-on cards.

## editors/ (10 files)

Docs, Sheets, Slides, and Forms add-ons (the "Editor add-ons" branch of the platform).

- [overview.md](editors/overview.md) — Overview of Editor add-ons and how they differ from Workspace add-ons.
- [building-editor-interfaces.md](editors/building-editor-interfaces.md) — Building card-based UI shared across Docs/Sheets/Slides/Forms editors.
- [editor-actions.md](editors/editor-actions.md) — Editor-specific actions, including requesting `drive.file` scope from a card button.
- [docs-overview.md](editors/docs-overview.md) — What Docs add-ons can do, document structure, and available triggers.
- [docs-quickstart-translate.md](editors/docs-quickstart-translate.md) — Full quickstart: build a Docs sidebar add-on that translates selected text (complete `translate.gs` + `sidebar.html` source).
- [sheets-overview.md](editors/sheets-overview.md) — What Sheets add-ons can do, spreadsheet structure, and available triggers.
- [slides-overview.md](editors/slides-overview.md) — What Slides add-ons can do, presentation structure, and available triggers.
- [slides-quickstart-translate.md](editors/slides-quickstart-translate.md) — Full quickstart: build a Slides sidebar add-on that translates selected text (complete source).
- [forms-overview.md](editors/forms-overview.md) — What Forms add-ons can do, form structure, question/static types, and quizzes.
- [forms-quickstart-notifications.md](editors/forms-quickstart-notifications.md) — Full quickstart: build a Forms add-on that emails notifications on new submissions.

## chat/ (18 files)

Building Google Chat apps (which share the add-ons card/event model).

- [overview.md](chat/overview.md) — What Chat apps are and the ways they can be built (Apps Script, HTTP, Pub/Sub, agent frameworks).
- [build.md](chat/build.md) — Overview of building Chat app interfaces with cards and dialogs.
- [configure.md](chat/configure.md) — Configuring a Chat app's identity, connection settings, and visibility in Google Chat.
- [commands.md](chat/commands.md) — Responding to slash commands and quick commands.
- [dialogs.md](chat/dialogs.md) — Building interactive modal dialogs in a Chat app.
- [send-messages.md](chat/send-messages.md) — Sending synchronous and asynchronous messages, including via the Chat REST API.
- [collect-information.md](chat/collect-information.md) — Collecting and processing user input through cards and dialogs.
- [preview-links.md](chat/preview-links.md) — Rendering link previews (smart chips) when users paste supported URLs into Chat.
- [convert.md](chat/convert.md) — Converting an existing interactive Chat app into a Google Workspace add-on.
- [quickstart-apps-script.md](chat/quickstart-apps-script.md) — Build a Chat app with Apps Script.
- [quickstart-http.md](chat/quickstart-http.md) — Build a Chat app backed by a plain HTTP endpoint.
- [quickstart-pubsub.md](chat/quickstart-pubsub.md) — Build a Chat app that receives events via Cloud Pub/Sub.
- [quickstart-adk-agent.md](chat/quickstart-adk-agent.md) — Build a Chat app powered by the Agent Development Kit (ADK).
- [quickstart-a2a-agent.md](chat/quickstart-a2a-agent.md) — Build a Chat app powered by an Agent2Agent (A2A) remote agent.
- [quickstart-a2ui-agent.md](chat/quickstart-a2ui-agent.md) — Build a Chat app using the Agent2UI (A2UI) protocol.
- [quickstart-dialogflow-es.md](chat/quickstart-dialogflow-es.md) — Build a Chat app backed by Dialogflow ES.
- [quickstart-dialogflow-cx.md](chat/quickstart-dialogflow-cx.md) — Build a Chat app backed by Dialogflow CX.
- [quickstart-ge-agent.md](chat/quickstart-ge-agent.md) — Build a Chat app powered by a Gemini Enterprise agent.

## meet/ (6 files)

Meet add-ons (Meet Add-ons SDK for Web — a JS-embedded side-panel/main-stage surface, distinct from the Card-based model but part of the same add-ons family; sourced from `developers.google.com/meet/add-ons/`).

- [overview.md](meet/overview.md) — What Meet add-ons are and the SDK's architecture.
- [concepts.md](meet/concepts.md) — Core concepts and the add-on architecture flow inside a Meet call.
- [quickstart.md](meet/quickstart.md) — Side-panel/main-stage SDK quickstart with npm/gstatic install and JS+Webpack / Next.js samples.
- [deploy-add-on.md](meet/deploy-add-on.md) — Deploying a Meet add-on (Cloud project setup, HTTP and Apps Script deployment manifests).
- [use-add-on.md](meet/use-add-on.md) — How end users open and use an add-on from the Meet Activities panel.
- [collaborate-in-the-add-on.md](meet/collaborate-in-the-add-on.md) — Multi-participant collaboration APIs (`ActivityStartingState`, `startActivity`) for synced in-call experiences.

## publish/ (2 files)

- [overview.md](publish/overview.md) — End-to-end process for publishing an add-on to the Google Workspace Marketplace.
- [update-published-add-on.md](publish/update-published-add-on.md) — Updating and managing a published add-on, including the "New deployment" vs. "New version" distinction.

## quickstart/ (2 files)

- [cats-quickstart-apps-script.md](quickstart/cats-quickstart-apps-script.md) — "Cats" quickstart: build a first Google Workspace add-on with Apps Script.
- [nodejs-quickstart.md](quickstart/nodejs-quickstart.md) — Build a first Google Workspace add-on with Node.js on an alternate (HTTP) runtime.

## guides/ (26 files)

Cross-cutting how-tos that apply across multiple add-on surfaces: getting started, card interaction patterns, style/testing/publishing mechanics, and platform policy.

- [starting-addons.md](guides/starting-addons.md) — How end users install and authorize add-ons.
- [using-addons.md](guides/using-addons.md) — How end users open and use an installed add-on.
- [building-workspace-addons.md](guides/building-workspace-addons.md) — Top-level guide to developing Google Workspace add-ons.
- [building-editor-addons.md](guides/building-editor-addons.md) — Top-level guide to developing Editor add-ons.
- [build-http-endpoints.md](guides/build-http-endpoints.md) — Building an add-on as a plain HTTP endpoint instead of an Apps Script project.
- [workspace-style-guide.md](guides/workspace-style-guide.md) — UX/visual style guidelines for Workspace add-on cards.
- [interactions.md](guides/interactions.md) — Building interactive cards that respond to widget events.
- [navigation.md](guides/navigation.md) — Navigating between cards (push/pop the card stack).
- [universal-actions.md](guides/universal-actions.md) — Adding universal actions to an add-on's overflow menu.
- [suggestions-autocomplete.md](guides/suggestions-autocomplete.md) — Adding autocomplete suggestions to text input widgets.
- [access-user-locale-timezone.md](guides/access-user-locale-timezone.md) — Reading the user's locale and timezone from the event object.
- [preview-links-smart-chips.md](guides/preview-links-smart-chips.md) — Rendering link-preview smart chips for a third-party service's URLs inside Docs/Sheets/Slides/Chat.
- [create-insert-resource-smart-chip.md](guides/create-insert-resource-smart-chip.md) — Letting users create and insert new third-party resources as smart chips.
- [connect-third-party-service.md](guides/connect-third-party-service.md) — Connecting an add-on to an external/third-party service (auth, API calls).
- [testing-workspace-addons.md](guides/testing-workspace-addons.md) — Testing a Workspace add-on before publishing.
- [debug-http.md](guides/debug-http.md) — Debugging an HTTP-based add-on.
- [query-error-logs.md](guides/query-error-logs.md) — Querying Cloud Logging error logs for a deployed add-on.
- [workspace-best-practices.md](guides/workspace-best-practices.md) — Recommended practices for Workspace add-on design and performance.
- [workspace-restrictions.md](guides/workspace-restrictions.md) — Platform quotas and restrictions for Workspace add-ons.
- [glossary.md](guides/glossary.md) — Glossary of add-on platform terminology.
- [upgrade-legacy-addons.md](guides/upgrade-legacy-addons.md) — Migrating a legacy (pre-Workspace) add-on to the current platform.
- [testing-editor-addons.md](guides/testing-editor-addons.md) — Testing an Editor add-on before publishing.
- [editor-best-practices.md](guides/editor-best-practices.md) — Recommended practices for Editor add-on design and performance.
- [editor-restrictions.md](guides/editor-restrictions.md) — Platform quotas and restrictions for Editor add-ons.
- [editor-style-guide.md](guides/editor-style-guide.md) — UX/visual style guidelines for Editor add-on HTML-service UI.
- [css-package.md](guides/css-package.md) — The `add-ons1.css` package for styling HTML-service dialogs/sidebars to match Google's look.

## Notes on scope and quality

- **Out of scope by design**: the `CardService`/`Card`/`Widget`/`AddOnsResponseService` *class reference* pages (`/apps-script/reference/card-service/...`) are intentionally excluded — they're mirrored separately in `reference/`. Google Workspace **Studio** (a distinct workflow-automation product living under the same `/workspace/add-ons/studio/` URL prefix) was also left out as outside the requested Gmail/Calendar/Drive/Editors/Chat/Meet/publishing scope.
- **Verbatim fidelity**: pages were fetched and, where the automated fetch tool initially returned a paraphrased/AI-summarized version instead of the true article body, re-fetched from raw HTML and converted with a custom parser to recover the full original text and code samples verbatim. One known residual gap: in `guides/create-insert-resource-smart-chip.md`, the single merged multi-language "Complete example" Java class could not be captured as one block (page-side truncation) — all of its methods are present verbatim in the per-language sections earlier in the same file, with a note at that spot.
- **No failed/404 URLs** were encountered across the full survey.
