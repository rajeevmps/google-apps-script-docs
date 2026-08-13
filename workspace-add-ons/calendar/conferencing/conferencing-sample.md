# Add a web conferencing service to Google Calendar

Important: This quickstart is only for web conference providers.

The following Google Workspace add-on quickstart extends Google Calendar to sync with a fictional web conferencing service called My Web Conferencing. When editing Calendar events, the add-on lets users see My Web Conferencing as a conferencing option.

The quickstart shows conference creation and event syncing, but isn't operational until you connect it to your conferencing solution API.

## Objectives

- Set up your environment.
- Set up the script.
- Run the script.

## Prerequisites

- A web browser with access to the internet.
- A Google Workspace account (You might need administrator approval).
- A Google Cloud project.

## Set up your environment

### Open your Cloud project in the Google Cloud console

If it's not open already, open the Cloud project that you intend to use for this sample:

1. In the Google Cloud console, go to the Select a project page.

   Select a Cloud project

2. Select the Google Cloud project you want to use. Or, click Create project and follow the on-screen instructions. If you create a Google Cloud project, you might need to turn on billing for the project.

### Turn on the Calendar API

This quickstart uses the Calendar advanced service, which accesses the Calendar API.

Before using Google APIs, you need to turn them on in a Google Cloud project. You can turn on one or more APIs in a single Google Cloud project.

In your Google Cloud project, turn on the Calendar API.

Turn on the API

### Configure the OAuth consent screen

Google Workspace add-ons require a consent screen configuration. Configuring your Google Workspace add-on's OAuth consent screen defines what Google displays to users.

1. In the Google API Console, go to Menu menu > Google Auth platform > Branding.

   Go to Branding

2. If you have already configured the Google Auth platform, you can configure the following OAuth Consent Screen settings in Branding, Audience, and Data Access. If you see a message that says Google Auth platform not configured yet, click Get Started:
   1. Under App Information, in App name, enter a name for the app.
   2. In User support email, choose a support email address where users can contact you if they have questions about their consent.
   3. Click Next.
   4. Under Audience, select Internal.
   5. Click Next.
   6. Under Contact Information, enter an Email address where you can be notified about any changes to your project.
   7. Click Next.
   8. Under Finish, review the Google API Services User Data Policy and if you agree, select I agree to the Google API Services: User Data Policy.
   9. Click Continue.
   10. Click Create.
3. For now, you can skip adding scopes. In the future, when you create an app for use outside of your Google Workspace organization, you must change the User type to External. Then add the authorization scopes that your app requires. To learn more, see the full Configure OAuth consent guide.

## Set up the script

### Create the Apps Script project

1. To create a new Apps Script project, go to script.new.
2. Click Untitled project.
3. Rename the Apps Script project Conference add-on and click Rename.
4. Next to the Code.gs file, click More more_vert > Rename. Name the file CreateConf.
5. Click Add a file add > Script.
6. Name the file Syncing.

Replace the contents of each file with the following corresponding code:

**CreateConf.gs**

```javascript
/**
 *  Creates a conference, then builds and returns a ConferenceData object
 *  with the corresponding conference information. This method is called
 *  when a user selects a conference solution defined by the add-on that
 *  uses this function as its 'onCreateFunction' in the add-on manifest.
 *
 *  @param {Object} arg The default argument passed to a 'onCreateFunction';
 *      it carries information about the Google Calendar event.
 *  @return {ConferenceData}
 */
function createConference(arg) {
  const eventData = arg.eventData;
  const calendarId = eventData.calendarId;
  const eventId = eventData.eventId;

  // Retrieve the Calendar event information using the Calendar
  // Advanced service.
  var calendarEvent;
  try {
    calendarEvent = Calendar.Events.get(calendarId, eventId);
  } catch (err) {
    // The calendar event does not exist just yet; just proceed with the
    // given event ID and allow the event details to sync later.
    console.log(err);
    calendarEvent = {
      id: eventId,
    };
  }

  // Create a conference on the third-party service and return the
  // conference data or errors in a custom JSON object.
  var conferenceInfo = create3rdPartyConference(calendarEvent);

  // Build and return a ConferenceData object, either with conference or
  // error information.
  var dataBuilder = ConferenceDataService.newConferenceDataBuilder();

  if (!conferenceInfo.error) {
    // No error, so build the ConferenceData object from the
    // returned conference info.

    var phoneEntryPoint = ConferenceDataService.newEntryPoint()
        .setEntryPointType(ConferenceDataService.EntryPointType.PHONE)
        .setUri('tel:+' + conferenceInfo.phoneNumber)
        .setPin(conferenceInfo.phonePin);

    var adminEmailParameter = ConferenceDataService.newConferenceParameter()
        .setKey('adminEmail')
        .setValue(conferenceInfo.adminEmail);

    dataBuilder.setConferenceId(conferenceInfo.id)
        .addEntryPoint(phoneEntryPoint)
        .addConferenceParameter(adminEmailParameter)
        .setNotes(conferenceInfo.conferenceLegalNotice);

    if (conferenceInfo.videoUri) {
      var videoEntryPoint = ConferenceDataService.newEntryPoint()
          .setEntryPointType(ConferenceDataService.EntryPointType.VIDEO)
          .setUri(conferenceInfo.videoUri)
          .setPasscode(conferenceInfo.videoPasscode);
      dataBuilder.addEntryPoint(videoEntryPoint);
    }

    // Since the conference creation request succeeded, make sure that
    // syncing has been enabled.
    initializeSyncing(calendarId, eventId, conferenceInfo.id);

  } else if (conferenceInfo.error === 'AUTH') {
    // Authenentication error. Implement a function to build the correct
    // authenication URL for the third-party conferencing system.
    var authenticationUrl = getAuthenticationUrl();
    var error = ConferenceDataService.newConferenceError()
        .setConferenceErrorType(
            ConferenceDataService.ConferenceErrorType.AUTHENTICATION)
        .setAuthenticationUrl(authenticationUrl);
    dataBuilder.setError(error);

  } else {
    // Other error type;
    var error = ConferenceDataService.newConferenceError()
        .setConferenceErrorType(
            ConferenceDataService.ConferenceErrorType.TEMPORARY);
    dataBuilder.setError(error);
  }

  // Don't forget to build the ConferenceData object.
  return dataBuilder.build();
}


/**
 *  Contact the third-party conferencing system to create a conference there,
 *  using the provided calendar event information. Collects and retuns the
 *  conference data returned by the third-party system in a custom JSON object
 *  with the following fields:
 *
 *    data.adminEmail - the conference administrator's email
 *    data.conferenceLegalNotice - the conference legal notice text
 *    data.error - Only present if there was an error during
 *         conference creation. Equal to 'AUTH' if the add-on user needs to
 *         authorize on the third-party system.
 *    data.id - the conference ID
 *    data.phoneNumber - the conference phone entry point phone number
 *    data.phonePin - the conference phone entry point PIN
 *    data.videoPasscode - the conference video entry point passcode
 *    data.videoUri - the conference video entry point URI
 *
 *  The above fields are specific to this example; which conference information
 *  your add-on needs is dependent on the third-party conferencing system
 *  requirements.
 *
 * @param {Object} calendarEvent A Calendar Event resource object returned by
 *     the Google Calendar API.
 * @return {Object}
 */
function create3rdPartyConference(calendarEvent) {
  var data = {};

  // Implementation details dependent on the third-party system API.
  // Typically one or more API calls are made to create the conference and
  // acquire its relevant data, which is then put in to the returned JSON
  // object.

  return data;
}

/**
 *  Return the URL used to authenticate the user with the third-party
 *  conferencing system.
 *
 *  @return {String}
 */
function getAuthenticationUrl() {
  var url;
  // Implementation details dependent on the third-party system.

  return url;
}
```

**Syncing.gs**

```javascript
/**
 *  Initializes syncing of conference data by creating a sync trigger and
 *  sync token if either does not exist yet.
 *
 *  @param {String} calendarId The ID of the Google Calendar.
 */
function initializeSyncing(calendarId) {
  // Create a syncing trigger if it doesn't exist yet.
  createSyncTrigger(calendarId);

  // Perform an event sync to create the initial sync token.
  syncEvents({'calendarId': calendarId});
}

/**
 *  Creates a sync trigger if it does not exist yet.
 *
 *  @param {String} calendarId The ID of the Google Calendar.
 */
function createSyncTrigger(calendarId) {
  // Check to see if the trigger already exists; if does, return.
  var allTriggers = ScriptApp.getProjectTriggers();
  for (var i = 0; i < allTriggers.length; i++) {
    var trigger = allTriggers[i];
    if (trigger.getTriggerSourceId() == calendarId) {
      return;
    }
  }

  // Trigger does not exist, so create it. The trigger calls the
  // 'syncEvents()' trigger function when it fires.
  var trigger = ScriptApp.newTrigger('syncEvents')
      .forUserCalendar(calendarId)
      .onEventUpdated()
      .create();
}

/**
 *  Sync events for the given calendar; this is the syncing trigger
 *  function. If a sync token already exists, this retrieves all events
 *  that have been modified since the last sync, then checks each to see
 *  if an associated conference needs to be updated and makes any required
 *  changes. If the sync token does not exist or is invalid, this
 *  retrieves future events modified in the last 24 hours instead. In
 *  either case, a new sync token is created and stored.
 *
 *  @param {Object} e If called by a event updated trigger, this object
 *      contains the Google Calendar ID, authorization mode, and
 *      calling trigger ID. Only the calendar ID is actually used here,
 *      however.
 */
function syncEvents(e) {
  var calendarId = e.calendarId;
  var properties = PropertiesService.getUserProperties();
  var syncToken = properties.getProperty('syncToken');

  var options;
  if (syncToken) {
    // There's an existing sync token, so configure the following event
    // retrieval request to only get events that have been modified
    // since the last sync.
    options = {
      syncToken: syncToken
    };
  } else {
    // No sync token, so configure to do a 'full' sync instead. In this
    // example only recently updated events are retrieved in a full sync.
    // A larger time window can be examined during a full sync, but this
    // slows down the script execution. Consider the trade-offs while
    // designing your add-on.
    var now = new Date();
    var yesterday = new Date();
    yesterday.setDate(now.getDate() - 1);
    options = {
      timeMin: now.toISOString(),          // Events that start after now...
      updatedMin: yesterday.toISOString(), // ...and were modified recently
      maxResults: 50,   // Max. number of results per page of responses
      orderBy: 'updated'
    }
  }

  // Examine the list of updated events since last sync (or all events
  // modified after yesterday if the sync token is missing or invalid), and
  // update any associated conferences as required.
  var events;
  var pageToken;
  do {
    try {
      options.pageToken = pageToken;
      events = Calendar.Events.list(calendarId, options);
    } catch (err) {
      // Check to see if the sync token was invalidated by the server;
      // if so, perform a full sync instead.
      if (err.message ===
            "Sync token is no longer valid, a full sync is required.") {
        properties.deleteProperty('syncToken');
        syncEvents(e);
        return;
      } else {
        throw new Error(err.message);
      }
    }

    // Read through the list of returned events looking for conferences
    // to update.
    if (events.items && events.items.length > 0) {
      for (var i = 0; i < events.items.length; i++) {
         var calEvent = events.items[i];
         // Check to see if there is a record of this event has a
         // conference that needs updating.
         if (eventHasConference(calEvent)) {
           updateConference(calEvent, calEvent.conferenceData.conferenceId);
         }
      }
    }

    pageToken = events.nextPageToken;
  } while (pageToken);

  // Record the new sync token.
  if (events.nextSyncToken) {
    properties.setProperty('syncToken', events.nextSyncToken);
  }
}

/**
 *  Returns true if the specified event has an associated conference
 *  of the type managed by this add-on; retuns false otherwise.
 *
 *  @param {Object} calEvent The Google Calendar event object, as defined by
 *      the Calendar API.
 *  @return {boolean}
 */
function eventHasConference(calEvent) {
  var name = calEvent.conferenceData.conferenceSolution.name || null;

  // This version checks if the conference data solution name matches the
  // one of the solution names used by the add-on. Alternatively you could
  // check the solution's entry point URIs or other solution-specific
  // information.
  if (name) {
    if (name === "My Web Conference" ||
        name === "My Recorded Web Conference") {
      return true;
    }
  }
  return false;
}

/**
 *  Update a conference based on new Google Calendar event information.
 *  The exact implementation of this function is highly dependant on the
 *  details of the third-party conferencing system, so only a rough outline
 *  is shown here.
 *
 *  @param {Object} calEvent The Google Calendar event object, as defined by
 *      the Calendar API.
 *  @param {String} conferenceId The ID used to identify the conference on
 *      the third-party conferencing system.
 */
function updateConference(calEvent, conferenceId) {
  // Check edge case: the event was cancelled
  if (calEvent.status === 'cancelled' || eventHasConference(calEvent)) {
    // Use the third-party API to delete the conference too.


  } else {
    // Extract any necessary information from the event object, then
    // make the appropriate third-party API requests to update the
    // conference with that information.

  }
}
```

7. Click Project Settings.
8. Check the Show "appsscript.json" manifest file in editor box.
9. Click Editor code.
10. Open the appsscript.json file and replace the contents with the following code, then click Save.

**appsscript.json**

```json
{
  "addOns": {
    "calendar": {
      "conferenceSolution": [{
        "id": 1,
        "name": "My Web Conference",
        "logoUrl": "https://lh3.googleusercontent.com/...",
        "onCreateFunction": "createConference"
      }],
      "currentEventAccess": "READ_WRITE"
    },
    "common": {
      "homepageTrigger": {
        "enabled": false
      },
      "logoUrl": "https://lh3.googleusercontent.com/...",
      "name": "My Web Conferencing"
    }
  },
  "timeZone": "America/New_York",
  "dependencies": {
    "enabledAdvancedServices": [
    {
      "userSymbol": "Calendar",
      "serviceId": "calendar",
      "version": "v3"
    }
    ]
  },
  "webapp": {
    "access": "ANYONE",
    "executeAs": "USER_ACCESSING"
  },
  "exceptionLogging": "STACKDRIVER",
  "oauthScopes": [
    "https://www.googleapis.com/auth/calendar.addons.execute",
    "https://www.googleapis.com/auth/calendar.events.readonly",
    "https://www.googleapis.com/auth/calendar.addons.current.event.read",
    "https://www.googleapis.com/auth/calendar.addons.current.event.write",
    "https://www.googleapis.com/auth/script.external_request",
    "https://www.googleapis.com/auth/script.scriptapp"
  ]
}
```

### Copy the Cloud project number

1. In the Google API Console, go to Menu menu > IAM & Admin > Settings.

   Go to IAM & Admin Settings

2. In the Project number field, copy the value.

### Set the Apps Script project's Cloud project

1. In your Apps Script project, click Project Settings.
2. Under Google Cloud Platform (GCP) Project, click Change project.
3. In GCP project number, paste the Google Cloud project number.
4. Click Set project.

### Install a test deployment

1. In your Apps Script project, click Editor code.
2. Open the CreateConf.gs file and click Run. When prompted, authorize the script.
3. Click Deploy > Test deployments.
4. Click Install > Done.

## Run the script

1. Go to calendar.google.com.
2. Create a new event or open an existing one.
3. Next to Add Google Meet video conferencing, click the Down arrow arrow_drop_down > My Web Conference. The Failed to create conference error displays since the add-on isn't connected to a real third-party conferencing solution.

## Next steps

- Extend Google Workspace with add-ons
- Build Google Workspace add-ons
- Publish an app
