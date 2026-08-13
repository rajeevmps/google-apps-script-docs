# Admin SDK Groups Settings Service

Source: https://developers.google.com/apps-script/advanced/admin-sdk-groups-settings

## Overview

The Admin SDK Groups Settings service in Apps Script enables Google Workspace administrators to manage group settings through the Admin SDK Groups Settings API. According to the documentation, this service "lets you use the Admin SDK's Groups Settings API in Google Apps Script."

## Key Characteristics

**Service Type:** Advanced service (must be enabled before use)

**API Compatibility:** The service utilizes "the same objects, methods, and parameters as the public API," maintaining consistency with the Admin SDK Groups Settings API v1 reference.

**Primary Function:** Allows administrators to "manage the group settings for groups in their Google Workspace account."

## Enabling the Service

This is an advanced service requiring enablement — see the guide on [enabling advanced services](https://developers.google.com/apps-script/guides/services/advanced). No further slug-specific steps are given on this page.

## Code Examples

### Get Group Settings
```javascript
function getGroupSettings() {
  const groupId = "exampleGroup@example.com";
  try {
    const group = AdminGroupsSettings.Groups.get(groupId);
    console.log(JSON.stringify(group, null, 2));
  } catch (err) {
    console.log("Failed with error %s", err.message);
  }
}
```

### Update Group Settings
```javascript
function updateGroupSettings() {
  const groupId = "exampleGroup@example.com";
  try {
    const group = AdminGroupsSettings.newGroups();
    group.description = "Newly changed group description";
    AdminGroupsSettings.Groups.patch(group, groupId);
  } catch (err) {
    console.log("Failed with error %s", err.message);
  }
}
```

## Resources

- **Reference Documentation:** [Admin SDK Groups Settings API v1](https://developers.google.com/admin-sdk/groups-settings/v1/reference) (external — not scraped)
- **Support Guide:** [Admin SDK Groups Settings support](https://developers.google.com/admin-sdk/groups-settings/support) (external — not scraped)
</content>
