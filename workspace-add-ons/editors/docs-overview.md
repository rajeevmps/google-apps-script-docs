# Extend Google Docs with add-ons

## Page Summary
- Google Docs is a cloud-based document solution enabling real-time collaboration and offering robust tools for composing, editing, and sharing documents.
- Docs add-ons, built using Apps Script, extend functionality by enabling workflow customization, integration with third-party systems, and connectivity with other Google Workspace applications.
- Add-ons can manipulate document content, create custom interfaces, and automate tasks through triggers based on specific events.
- Google provides comprehensive documentation and resources, including code samples, to guide developers in building Docs add-ons.

## Introduction
[Google Docs](https://workspace.google.com/products/docs/) is a cloud-based document solution with real-time collaboration and powerful tools to compose, edit, and share documents.

You can extend Docs with add-ons that build customized workflow improvements, establish connectivity to third-party systems, and integrate your documents with other Google Workspace applications (like Google Slides).

You can see the Docs add-on others have built on the [Google Workspace Marketplace](https://workspace.google.com/marketplace/category/works-with-doc).

## What you can do
Here are a few things you can do with add-ons that extend Docs:

* Read, edit, visualize, and format text in Docs using the built-in Apps Script [Document service](/apps-script/reference/document). The service also lets you create and modify tables, images, drawings, and equations appearing in Docs.
* Create [custom menus](/workspace/add-ons/concepts/menus) and define multiple [custom dialogs and sidebars](/workspace/add-ons/concepts/dialogs) interfaces using standard HTML and CSS.
* Use add-on [triggers](#triggers) to run specified functions when certain triggering events occur.

Docs add-ons are built using Apps Script. To learn more about how to access and manage Google Docs with Apps Script, see [Extend Docs](/apps-script/guides/docs).

## Document structure
The documents created in Docs have internal, tree-like structures (similar to HTML or JSON) that define where and how text, images, tables, and other elements appear. The Apps Script [Document service](/apps-script/reference/document) defines several classes (such as [`Paragraph`](/apps-script/reference/document/paragraph) or [`Table`](/apps-script/reference/document/table)) to help manage the different element types.

See [Structure of a document](/apps-script/guides/docs#structure_of_a_document) to learn about these element classes and the rules that govern their arrangement.

## Triggers
Apps Script **triggers** let a script project execute a specified function when certain conditions are met, such as when a document is opened or when an add-on is installed.

See [add-on triggers](/workspace/add-ons/concepts/editor-triggers) for more information on what triggers can be used with Docs add-ons and what restrictions apply to their use.

## Getting started
When you're ready to take a look at some code, check out our [add-on samples](/workspace/add-ons/samples), including the [Docs add-on Quickstart](/workspace/add-ons/editors/docs/quickstart/translate) featuring Google Translate.
