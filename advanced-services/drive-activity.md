# Google Drive Activity Service

Source: https://developers.google.com/apps-script/advanced/drive-activity

## Overview

The Google Drive Activity service provides programmatic access to retrieve information about Google Drive activity using the Google Drive Activity API within Apps Script.

**Key characteristics:**
- It's an advanced service requiring enablement before use
- Uses the same objects, methods, and parameters as the public API
- Mirrors the Google Drive Activity API v2 reference documentation

## Core Functionality

According to the documentation, this service "lets users retrieve information about their Google Drive activity" through Apps Script integration.

## Sample Implementation

```javascript
function listDriveActivity() {
  const request = {
    pageSize: 10,
  };
  try {
    const response = DriveActivity.Activity.query(request);
    const activities = response.activities;
    if (!activities || activities.length === 0) {
      console.log("No activity.");
      return;
    }
    console.log("Recent activity:");
    for (const activity of activities) {
      const time = getTimeInfo(activity);
      const action = getActionInfo(activity.primaryActionDetail);
      const actors = activity.actors.map(getActorInfo);
      const targets = activity.targets.map(getTargetInfo);
      console.log("%s: %s, %s, %s", time, actors, action, targets);
    }
  } catch (err) {
    console.log("Failed with an error %s", err.message);
  }
}
```

## Reference Resources

- [Google Drive Activity API v2 Reference](https://developers.google.com/drive/activity/v2/reference/rest) (external — not scraped)
- [Support Guide](https://developers.google.com/drive/activity/v2/support) (external — not scraped)
</content>
