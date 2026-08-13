# Sync calendar conference changes

Note: This functionality was built for conference providers specifically, and was originally available as Calendar conferencing add-ons.

Users can update or delete their Google Calendar events. If a user updates an event after creating a conference for it, your Google Workspace add-on may need to respond to the change by updating the conference data. If your third-party conferencing system depends on tracking event data, failing to update the conference on an event change can render the conference unusable.

The process of keeping conference data updated with changes to the Calendar event is called syncing. Sync event changes by creating an Google Apps Script installable trigger that fires whenever events change in a given calendar. The trigger doesn't report which events changed and you can't limit it to only events with conferences you created. Request a list of all changes made to a calendar since the last sync, filter through the event list, and make updates accordingly.

The general syncing procedure is as follows:

1. The first time a user creates a conference, the sync process is initialized.
2. Whenever the user creates, updates, or deletes one of their Calendar events, the trigger executes a trigger function in your add-on project.
3. The trigger function examines the set of event changes since the last sync and determines if any require updating an associated third-party conference.
4. Required updates are made to the conferences by making third-party API requests.
5. A new sync token is stored so the next trigger execution only examines the most recent changes to the calendar.

## Initialize syncing

The initialization process ensures that your add-on is ready to respond to calendar changes. Once the add-on has successfully created a conference on a third-party system, it should create an installable trigger that responds to event changes in this calendar, if the trigger does not already exist.

After creating the trigger, initialization should finish by creating the initial sync token. This is done by executing the trigger function directly.

## Create a Calendar trigger

To sync, your add-on needs to detect when a Calendar event that has an attached conference is changed. This is accomplished by creating an `EventUpdated` installable trigger. Your add-on only needs one trigger for each calendar, and can create them programmatically.

A recommended time to create a trigger is when the user creates their first conference, since at that point the user is starting to use the add-on. After creating a conference and verifying there is no error, your add-on should check to see if the trigger exists for this user and if not create it.

Creating triggers requires the add-on to have the `https://www.googleapis.com/auth/calendar.readonly` and `https://www.googleapis.com/auth/script.scriptapp` scopes.

## Implement a sync trigger function

Trigger functions are executed when Apps Script detects a condition that causes a trigger to fire. `EventUpdated` Calendar triggers fire when a user creates, modifies, or deletes any event in a specified calendar.

Implement the trigger function your add-on uses. This trigger function should do the following:

Make a Calendar advanced service `Calendar.Events.list` call using a `syncToken` to retrieve a list of events that have changed since the last sync. By using a sync token, you reduce the number of events your add-on must examine.

When the trigger function executes without a valid sync token, it backs off to a full sync. Full syncs attempt to retrieve all events within a prescribed window of time in order to generate a new, valid sync token.

Caution: Occasionally sync tokens are invalidated by the server, resulting in a `Sync token is no longer valid` error. When this happens, your code should conduct a full sync and replace any stored sync tokens you have.

Each modified event is examined to determine if it has an associated third-party conference.

If an event has a conference, it is examined to see what was changed. Depending on the change, a modification of the associated conference may be necessary. For example, if an event was deleted, the add-on should delete the conference.

Any needed changes to the conference are made by making API calls to the third-party system.

After making all necessary changes, store the `nextSyncToken` returned by the `Calendar.Events.list` method. This sync token is found on the last page of results returned by the `Calendar.Events.list` call.

## Update the Calendar event

In some cases you may want to update the Calendar event when performing a sync. If you choose to do this, make the event update with the appropriate Calendar advanced service request. Be sure to use conditional updating with an `If-Match` header. This prevents your changes from overwriting concurrent changes made by the user in a different client.

## Example

The following example shows how you can set up syncing for calendar events and their associated conferences.

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
