# Provide attachment icons

Google Calendar Google Workspace add-ons let developers add custom attachments to Calendar events through the use of the EventAttachmentTrigger. These custom attachments can optionally specify an image URL which is displayed as the attachment's icon inside of the Calendar event. Since these images are used within Calendar directly, you must host them on Google's infrastructure. Specifically, use the same icon that you use for the add-ons Google Workspace Marketplace store listing.

To obtain an image URL that can be used as the `attachment.iconUrl`:

1. Open the Google Cloud console.
2. If necessary, switch to the project hosting your Google Workspace add-on.
3. At the top-left, click Menu menu > APIs & Services.
4. In the list at the bottom, click Google Workspace Marketplace SDK.
5. Select the Store Listing tab.
6. In the Graphics Assets section, upload the intended attachment icon image as an Application Icon 32x32.
7. Copy the resulting image URL and use it as the `attachment.iconUrl`.
