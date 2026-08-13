# Add conferencing add-on settings

Note: This functionality was built for conference providers specifically, and was originally available as Calendar conferencing add-ons.

Google Workspace add-ons that add conferencing solutions often have details that should be controlled by the user from an add-on settings page. For example, it is common to have a button or control that lets a user log out of the third-party conference system.

Add-on setting pages are optional. The following sections describe how to open an add-on's setting page and how to build a setting page.

## Open add-on settings

Settings for conferencing add-ons are accessible from the Calendar settings menu. Open the settings page of an add-on you have installed by doing the following:

1. Open Google Calendar.
2. Click the settings icon and select Settings.
3. In the left navigation panel, select add-ons to jump to the installed add-on list.
4. Click the Settings button that appears to the right of the add-on name to open the settings page for that add-on; this causes Calendar to open the settings page URL.

If an add-on does not define a settings page, the Settings button does not appear.

## Build a settings page

A settings page is built using standard HTML and CSS. When designing your page, follow the add-on style guidelines.

When a user adjusts the add-on settings, the page should send requests to the third-party conferencing system to enact those changes. The page can also store and retrieve information from the add-on project user properties as needed.

### Hosted on an external web server

You can host your add-on setting page externally from the add-on script project, perhaps as part of the third-party conferencing website.

To link an add-on to an external setting page, do the following:

1. Build the page and host it externally. When adding elements to the page, ensure they communicate correctly with the third-party conferencing system and make the appropriate changes for that user.
2. In the add-on script project, implement a function that returns the URL for the external page.
3. Specify the name of this function as the `calendar.createSettingsFunction` field in the add-on project manifest.

### Hosted within Apps Script

You can provide a settings page for your add-on by using an Apps Script web app. As a web app, your add-on script project can build and deploy the page, which is then hosted on the Apps Script servers.

See the HTML Service guide for details on how to build HTML for web apps. Your settings page can communicate with the Google servers as needed. You can also make use of templates in the page to make it more dynamic.

The Calendar conferencing add-on example shows how to construct a web app settings page.

Caution: When deploying a web app page for use, you must provide a script project version. You also provide a project version when deploying the add-on. As you update your script project to new versions, always ensure that the version number for the deployments matches. Otherwise your add-on may exhibit unexpected behavior.
