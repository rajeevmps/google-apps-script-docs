# Convert an interactive Google Chat app to a Google Workspace add-on

## Overview

This guide enables developers to transform existing Google Chat apps using Chat API interaction events into Google Workspace add-ons. The conversion opens up new possibilities for integration and features within Google Chat and across Google Workspace, including distribution through Google Workspace Marketplace alongside Gmail, Calendar, and Docs extensions.

## Key Conversion Steps

The process involves five main phases:

1. **Code Duplication**: Create a backup copy of your existing Chat app before modifications
2. **Code Modifications**: Update request/response structures from Chat API `Event` format to Google Workspace add-on `EventObject` format
3. **Test Configuration**: Enable add-on settings for test users in Google Cloud console
4. **Testing**: Verify functionality with configured test accounts
5. **Full Deployment**: Complete irreversible conversion for all users

## Critical Limitations

Before conversion, review limitations of Google Workspace add-ons that extend Google Chat to ensure your app's functionality remains intact. Notably, Google Chat app homepages aren't supported by add-ons that extend Google Chat, so `APP_HOME` events aren't supported.

## Request/Response Mapping

The conversion requires translating between two distinct payload structures. For example, an "App added to space" event transforms from `{"type": "ADDED_TO_SPACE", "space": {...}}` to a nested structure: `{"chat": {"addedToSpacePayload": {"space": {...}}}}`

For HTTP deployments, request verification updates are essential: Google Workspace add-ons use per-project service accounts instead of `chat@system.gserviceaccount.com`.
