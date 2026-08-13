# Extend the Editors with Google Workspace add-ons

### Page Summary

- Google Workspace add-ons extend Google Docs, Sheets, and Slides with custom interfaces to enhance productivity and automate tasks, saving users time and effort.

- These add-ons allow integration with third-party systems and the creation of Homepage, REST API, and Link preview interfaces directly within the Editors.

- Add-ons are built using Card service and configured using a manifest file, with specific sections to enable Editor functionality.

- They are not supported on mobile clients and offer functionalities such as building Editor interfaces and defining Editor actions.

---

Google Docs, Google Sheets, and Google Slides provide a cloud-based productivity solution with real-time collaboration. However, modifying and surfacing relevant information in the editors is often a time-consuming task.

You can save your users time and effort by extending Docs, Sheets, and Slides with add-ons. add-ons for Google Forms isn't available yet.

When you build a Google Workspace add-on, you can define custom interfaces that are inserted directly into the Editors. These interfaces help automate tasks, present additional information to the user, or let the user interact with a third-party system without having to switch to a new browser tab.

With Google Workspace add-ons, you can create the following Editor interfaces:

* Homepage interfaces
* REST API interfaces
* Link preview interfaces

**Note:** You can't use Google Workspace add-ons for Editors on mobile clients.

### See what you can make

Google Workspace add-ons are built using the [Card service](/apps-script/reference/card-service/card-service). See [Build add-ons](/workspace/add-ons/how-tos/building-workspace-addons) for an overview.

Google Workspace add-on behavior is configured using a [manifest](/workspace/add-ons/concepts/workspace-manifests). To enable Google Workspace add-on for Editors, include Editor-specific sections.

When configuring your add-on for editors, you must decide what interfaces to create for your add-on and what actions it can take. See the following guides for more information:

* [Build Google editor interfaces](/workspace/add-ons/editors/gsao/building-editor-interfaces)
* [Editor actions](/workspace/add-ons/editors/gsao/editor-actions)
* [Manifest structure for add-ons](/workspace/add-ons/concepts/workspace-manifests#manifest_structure_for_g_suite_add-ons)
* Try a sample:
  * [Plan travels with an AI agent accessible across Google Workspace](/workspace/add-ons/samples/travel-concierge)
  * [Build Gemini Enterprise agents that are tightly integrated with Google Workspace data stores, APIs, and add-ons](//codelabs.developers.google.com/ge-gws-agents)
  * [Build Vertex AI agents that are tightly integrated with Google Workspace data stores, APIs, and add-ons](//codelabs.developers.google.com/vertexai-gws-agents)
