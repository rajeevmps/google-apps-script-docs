# Admin SDK Directory Service

Source: https://developers.google.com/apps-script/advanced/admin-sdk-directory

## Overview

The Admin SDK Directory service enables administrators of Google Workspace domains to manage devices, groups, users, and other entities programmatically through Apps Script.

## Key Features

As described in the documentation, this service provides "the ability to manage devices, groups, users, and other entities in their domains." It functions as an advanced service requiring specific enablement steps.

## Prerequisites

Before using this service, you must:

1. **Enable the advanced service** in your Apps Script project
2. **Enable Admin SDK** on your Google Workspace domain (see [prerequisites documentation](https://developers.google.com/admin-sdk/directory/v1/guides/prerequisites))

## Reference Documentation

The service mirrors the public [Admin SDK Directory API](https://developers.google.com/admin-sdk/directory/v1/reference), using identical objects, methods, and parameters. For detailed API information, consult the official reference guide. (External REST reference — not scraped.)

## Common Operations (Code Examples)

The documentation provides sample implementations for:

- **List users**: Retrieve all domain users sorted by first name with pagination
- **Get user**: Retrieve specific user data by email address
- **Add user**: Create new user accounts with required fields
- **Create alias**: Generate email nicknames for existing users
- **List groups**: Display all domain groups
- **Add group member**: Assign users to existing groups

## Support

For issues and additional assistance, see the [Admin SDK Directory support guide](https://developers.google.com/admin-sdk/directory/support). (External link — not scraped.)
</content>
