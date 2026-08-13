# Build conferencing add-ons

Note: This functionality was built for conference providers specifically, and was originally available as Google Calendar conferencing add-ons.

The procedure to build a Google Workspace add-on that provides Calendar third-party conferencing solutions is the same as the procedure for building add-ons, with a few additional steps (shown in bold below):

1. Choose an add-ons project owner and collaborators.
2. Create an Google Apps Script project.
3. Design your add-on appearance and behavior.
4. **Enable the Calendar advanced service.**
5. Configure the add-on project manifest.
6. **Define conference solutions in the manifest.**
7. Write code to define the add-on's appearance and behavior, using the built-in Apps Script Card service.
8. **Write code to manage conference solutions, using Apps Script's built-in ConferenceData service.**
9. (Optional) **Create and configure an add-on settings page.**
10. Verify your add-on's OAuth scopes.
11. Test the add-on within the host applications it extends.
12. Publish the add-on.

This page provides a general overview of each of the new steps (see Building add-ons for an overview of the other steps).

## Enable the Calendar advanced service

The Calendar advanced service lets you call the Calendar API directly from an Apps Script project. Some standard operations such as Calendar event syncs can only be performed using the advanced service. Before you can use the advanced service, enable it for your add-on project.

You can enable the Calendar advanced service from the Apps Script editor. Be sure to enable the API in both the editor Advanced Google Services dialog and the Google Cloud console.

For consistency and accuracy, use either the Calendar advanced service or the built-in Calendar service, not both. If you enable the Calendar advanced service, use it exclusively throughout your code.

## Define conference solutions in the manifest

The add-on manifest provides the basic information that Calendar needs to display and activate the add-on conference solutions. Your add-on manifest must define (in its calendar section) one or more conference solutions that describe the types of third-party conferences Calendar events can use.

See Manifests for details on how to configure your add-on's manifest.

## Add code to create and sync conferences

After you create a script project, you can add code to define the add-on's conferencing-related behavior. You can use the Calendar advanced service, the ConferenceData service, and other Apps Script services to control this behavior.

As you add conference handling code to your add-on, add code to create conferences, sync calendar changes, and optionally add a settings page.

Refer to the add-on style guide as you code for guidelines on how to design your add-on user experience.

### Create conferences

Your add-on must be able to take information about the Calendar event and use it to create a conference on the third-party conference system. Implement one or more onCreateFunction methods that execute this process, and configure these methods in your add-on manifest.

For more details, see Create third-party conferences.

### Sync calendar changes

After a conference is created and linked to a Calendar event, the conference often needs to be updated to reflect changes in the event. For example, if a user changes the time of the event, the conference data in the third-party conferencing system needs to be updated to reflect this. The process of updating the conference data in response to event changes is called syncing.

For more details, see Sync calendar changes.

### Add settings

You may want to have optional settings that let users configure your add-on. For example, you may want to let users to set conference parameters or notes that are attached to the conference.

Whenever you want to provide users some degree of control over the add-on behavior, you can provide those options in an add-on settings page. This is a web page (either hosted by the add-on script or hosted externally) that is opened when the user accesses the add-on settings within the Calendar UI.

Creating an add-on settings page is optional. For more details, see Add settings.
