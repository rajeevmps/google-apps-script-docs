# Collaborate using a Meet add-on

## Overview

Participants in a meeting can work collaboratively on a Google Meet add-on activity. When a collaborative activity starts, all participants in the meeting receive a notification that the activity is ongoing.

This notification is adapted to the availability and installation status of the add-on:

- **If the participant has the add-on installed**: They can join the activity.
- **If the participant doesn't have the add-on installed**: They're directed to install the add-on.
- **If the add-on isn't available for the participant's platform**: They're informed that they can't join the activity using their current device.

When a user joins the activity they will load their own iframes with your add-on content. You can customize whether new joiners should open the collaborative activity in the main stage or side panel.

## Start the activity

An activity is started by calling the `startActivity()` method, which uses the `ActivityStartingState` interface.

### Step 1 (Optional): The add-on sets the activity starting state

The `ActivityStartingState` contains information about the initial state of the add-on that's used when the participant accepts the invitation to join the activity.

The add-on can set or update the `ActivityStartingState` by calling the `setActivityStartingState()` method anytime before or during the activity. Calls to `setActivityStartingState()` can be omitted if the `ActivityStartingState` is exclusively set in the call to `startActivity()`.

### Step 2: The add-on starts the activity

The activity begins when the add-on calls the `startActivity()` method on the `MeetSidePanelClient`. The `startActivity()` method takes an `ActivityStartingState` object as a parameter, so `startActivity()` can be called instead of calling `setActivityStartingState()`.

Once the user completes the content selection and is ready to start an activity, call the `startActivity()` method in your add-on as follows:

```
sidePanelClient.startActivity({
        mainStageUrl: "https://app.example.com/mainstage",
        additionalData: JSON.stringify({
            // State to send to participants.
        })
    });
```

When `startActivity()` method is invoked, Meet performs the following actions:

- **For other participants**: Meet shows a notification that the activity is ongoing.
- **For the initiator**: If a main stage URL was specified in the `ActivityStartingState`, Meet opens the main stage using the URL from the `ActivityStartingState`.

### Step 3: Get the activity starting state

When a user joins the activity, they load your add-on into the main stage or side panel depending on the `ActivityStartingState`.

With the `additionalData` property, you can share initial data (also referred to as state) with users joining the activity. After initializing a `MainStageClient` or `SidePanelClient`, you can call the `getActivityStartingState()` method to retrieve the `additionalData` property.

```
const startingState = client.getActivityStartingState();
    const additionalData = JSON.parse(startingState.additionalData);
```

### Step 4 (Optional): Share add-on state in an activity

You may also share state between users while the activity is ongoing. You can share state in two ways:

- Handle it yourself by authoring your own synchronization backend.
- Use the Co-Doing API, which is a convenient and fast way to share arbitrary data between users.

## Example: Animation add-on on GitHub

The "Animation" sample add-on on GitHub includes collaboration in an add-on. Step 1 from this guide is not included in the sample. Instead, when the add-on initiator clicks the "Start the Animation" button in the side panel, the `startActivity()` method is called (Step 2) by populating the starting state with the user's selected color. After the activity starts, the main stage retrieves the starting state by calling the `getActivityStartingState()` method (Step 3). Step 4 is omitted, as state (the selected color) is not shared between participants during the activity in this sample add-on. Individual users can, however, change their own state by selecting a color, which is sent from the side panel frame to the main stage frame using frame-to-frame messaging.

## Constraints

- The URLs specified in the `ActivityStartingState` must belong to the same origin as the origins specified in the add-on manifest. For more information, see Add-on security.
- The `sidePanelUrl` property, `mainStageUrl` property, and `additionalData` property character lengths must conform to their respective size limits as published in the SDK reference docs.

## Related topics

- Use the activity starting state
- Use a Meet add-on
- Implement the Co-Doing API
- Add-on security
