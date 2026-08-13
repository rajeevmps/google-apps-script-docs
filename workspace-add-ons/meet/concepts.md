# Meet add-on concepts

## Architecture

Google Meet add-ons integrate into Google Meet through a structured process:

1. **Load add-on panel**: User clicks the meeting tools button to access installed add-ons
2. **Select add-on**: User chooses an add-on from the panel
3. **Load add-on iframe**: Meet loads the side panel iframe URL specified in the manifest
4. **Create AddonSession**: The add-on creates an `AddonSession` object
5. **Add-on initialized**: Ready for use
6. **(Optional) Request token with One Tap**: Uses Google One Tap for authentication
7. **(Optional) Google returns ID token**: Contains user identity information

## Google Workspace Add-ons in the Marketplace

Google Workspace add-ons are customized apps that integrate with Google Workspace applications, such as Gmail, Google Docs, and Google Sheets. The Google Workspace Marketplace provides a central location for finding, installing, and managing published add-ons.

## Types of Add-ons

Two main types exist: Google Workspace add-ons and Editor add-ons. For Meet add-ons SDK development, you must use Google Workspace add-ons. These add-ons can target multiple Google Workspace apps and require declaring a `meet` object within the manifest's `addOns` section.

Add-ons for Meet load in iframes and must reference web pages rather than card-based interfaces.

## Publishing

Once developed, add-ons can be published to make them available for discovery and installation by other users.
