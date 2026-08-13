# Build Editor add-ons

Before building your Editor add-on, review the Apps Script quotas and limitations to align your project design with these guidelines. Familiarize yourself with these limits early to prevent issues. Apps Script is ideal for lightweight add-on development for yourself, your team, or your organization. However, if you build a large-scale add-on that needs to handle many users, requires low latency, or demands full control over your infrastructure, consider a different runtime.

Follow these steps to build an Editor add-on:

1. Create an Apps Script project.
2. Code the add-on appearance and behavior using the Apps Script HTML service.
3. Test the add-on.
4. Publish the add-on.

## Create a script project

An Editor add-on is a standalone Apps Script project. The standalone script guide describes how to create new projects. Alternatively, open a new script. The application places the project file (initially named `Untitled project`) in your root Drive folder.

**Note:** To publish your add-on, use a standard Google Cloud (GCP) project.

### Collaboration

When you collaborate on an add-on, a single user account owns the project. When you publish the add-on, a single user account is the publisher. The publishing account must have edit access to the script project, but it doesn't need to be the project owner.

**Avoid losing access to code or settings if the owner of the project leaves your organization.**

To prevent losing access to code, use shared drives when you collaborate. Placing your script file in a shared drive ensures that no single account is the sole owner.

Add collaborators to the script project's Google Cloud (GCP). This ensures that your team can always access the add-on's Cloud settings.

**Warning:** If you don't add collaborators, transfer ownership of the script project before the owner's account is shut down or removed. Otherwise, you might lose access to the add-on code and settings.

## Code the add-on

After you create a script project, write code to define the add-on appearance and behavior. Use the Apps Script HtmlService to construct the user interface—dialogs and sidebars—using conventional HTML and CSS. Editor add-ons can define custom menu items.

As you code, refer to the Editor add-on style guide to create a seamless user experience that extends the editor in a natural way. When building interfaces, use the add-ons CSS package and refer to the style guide for recommendations on text, menus, controls, branding, and accessibility. Also, understand and program for the different authorization lifecycle states your add-on might encounter.

## Test the add-on

Test Editor add-ons before you publish them to ensure they behave as expected. Testing requires a test configuration and a testing document, spreadsheet, form, or presentation.

See Test an Editor add-on.

## Publish the add-on

Publishing makes your add-on available to others—either publicly to all users, or privately to users in a specific domain. Before you publish, review the publication overview.

Editor add-ons are published to the Google Workspace Marketplace. Publicly available add-ons require app review before they are published.

See Publishing an Editor add-on.
