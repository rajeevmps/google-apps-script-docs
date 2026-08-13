# Meet add-ons SDK for Web overview

The Google Meet add-ons SDK lets you embed your app into Google Meet as an add-on where users can discover, share, and collaborate in the app without leaving Meet.

Developers can register their app in the Google Workspace Marketplace, through which users and administrators can search for, discover, and install add-ons. Users can also discover and install apps directly from the Meet UI.

For more information about add-ons and the Marketplace, see Concepts.

**Note:** Third-party cookies in the Chrome browser are **no longer being deprecated**. Development of Google Meet add-ons shouldn't be impacted for the near future. However, Chrome intends to further elevate user choice around third-party cookies so third-party cookie access might become more limited in the future than it is today.

## Key Terminology

- **Add-ons:** Customized apps that integrate with Google Workspace apps.
- **Available add-ons:** Add-on that's available in the Marketplace but not installed by users.
- **Google Workspace Marketplace:** The Marketplace offers users and administrators a way to find and install third-party enterprise apps that are integrated with Google Workspace. It's the central place for managing published Google Workspace add-ons.
- **Installable add-ons:** An add-on that users can install through the side panel or through the Marketplace.
- **Installed add-ons:** Add-ons that are installed and ready for use. These are listed in a user's add-ons side panel. User's cannot uninstall admin-installed apps.
- **Main stage:** The central focus area where the meeting is held. An add-on can open on the main stage to display content that needs more space than what's available in the side panel. The main stage is rendered by its own page in your add-on (for example, `https://example.com/mainStage.html`), which must call `createAddonSession` in JavaScript.
- **Origin:** A URL with a scheme (protocol), host (domain), and port. Two URLs have the same origin when they share the same scheme, host, and port. For example, `https://example.com/` and `http://example.com/` don't share the same origin (because they use different schemes).
- **Region Capture screen sharing:** Allows Meet to crop the video track and remove some content from it before sharing it remotely.
- **Screen sharing:** The act of showing a screen, window, or browser tab to others in a call or the contents of screen sharing.
- **Side panel:** The vertical panel on the right side of the meeting space. This initially displays the installed add-ons for selection. Once an add-on is selected, the side panel displays the entry point page for your add-on app.

## Related Topics

- To learn how to create an add-on, follow the example in Deploy a Meet add-on.
- To learn how to use the Meet add-ons SDK, follow the example in Use the Meet add-ons SDK.
- To learn how to collaborate in an add-on, follow the example in Collaborate using a Meet add-on.
- To implement either the Co-Doing API or Co-Watching API, see Implement the Co-Doing API and Implement the Co-Watching API.
- To learn about deploying and sharing your Meet add-on with others, see Publish your Meet add-on.
- To learn about developing with Google Workspace APIs, refer to Get started as a Google Workspace developer.
