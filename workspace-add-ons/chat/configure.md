# Configure a Google Chat app

This guide explains how to set up a Google Chat app as a Google Workspace add-on using either Apps Script or an HTTP service.

You'll need a Google Workspace account, a Google Cloud project, and necessary API configurations to get started.

The setup involves choosing a display name, avatar, and description for your app, and configuring its interactive features in the Google Cloud console.

For existing Google Workspace add-ons, specific considerations apply when integrating Chat app functionalities.

This feature is part of the Google Workspace Developer Preview Program, granting early access before public release.

## Prerequisites

- A Business or Enterprise Google Workspace account with access to Google Chat
- A Google Cloud project
- Configured OAuth consent screen
- Enabled Google Chat API

## Key Configuration Steps

### Chat App Display Information

Choose these details before configuration:

| Field | Description | Format |
|-------|-------------|--------|
| App name | The display name for the Chat app | Up to 25 alphanumeric characters |
| Avatar URL | Image displaying as the Chat app's avatar | HTTPS URL (PNG/JPEG, 256x256+ pixels recommended) |
| Description | Brief purpose description | Up to 40 alphanumeric characters |

### Configuration Process in Google Cloud Console

1. Navigate to the Chat API Configuration page
2. Fill out Application info fields (name, avatar URL, description)
3. Enable interactive features and select functionality
4. Choose connection settings: HTTP endpoint, Apps Script deployment ID, Dialogflow, or Cloud Pub/Sub
5. Optionally configure triggers for Chat events
6. Add quick commands, slash commands, or link previews
7. Set visibility for testing (up to five individuals or Google Groups)
8. Optionally enable Google Cloud Logging
9. Save configuration

## Important Considerations for Existing Add-ons

- Chat apps require different configuration than add-ons extending other Google Workspace applications
- Chat apps use separate name and logo settings from other applications
- Published add-ons cannot save drafts of Chat API changes—updates immediately affect all users
- Apps Script add-ons must use the same deployment ID across all configurations
- HTTP service deployments specified in the Marketplace SDK apply only to other Google Workspace applications
