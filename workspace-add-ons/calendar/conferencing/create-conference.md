# Create third-party conferences

Note: This functionality was built for conference providers specifically, and was originally available as Calendar conferencing add-ons.

Each conference solution defined in your script project manifest has an associated `onCreateFunction`. The Google Workspace add-on calls this function to create a conference whenever a user attempts to select that conference solution for an event.

Implement each `onCreateFunction` described in your add-on manifest. These functions must do the following:

1. Retrieve any Google Calendar event information, such as the event ID or list of attendees, that the third-party conferencing system needs to create the conference.
2. Connect to the third-party conferencing service and create a new conference there using the Calendar event information.
3. If the conference creation request fails, use the error information to build and return a `ConferenceData` object containing a `ConferenceError`. Otherwise, complete the next steps.
4. Initialize conference syncing.
5. Use the information returned by the third-party conferencing service to build and return a new `ConferenceData` object.

## Retrieve event information

To create a third-party conference, information about the corresponding Calendar event is needed. The exact event information required varies between different third-party conference systems, but often includes the event start time, end time, summary, attendee list, and ID.

When called, each `onCreateFunction` you define is passed an argument that contains the calendar and event IDs. Use these IDs to retrieve the full event information using the Calendar advanced service.

It's possible for Calendar to add conference details to an event before it exists. In such cases, Calendar passes the `onCreateFunction` a valid `eventId`, but subsequent calls to `Calendar.Events.get` can result in an error saying the event does not exist. In these cases, create the third-party conference using placeholder data; this data is replaced the next time the event syncs.

## Create the third-party conference

After the `onCreateFunction` has retrieved the necessary event data, it must connect to the third-party conferencing system to create the conference. Typically this is accomplished by making API requests supported by the third-party conferencing system. Check the documentation for your third-party conferencing solution to determine what API requests you can use to create conferences.

In Google Apps Script, the easiest way to handle making external API requests is by using the OAuth2 for Apps Script or OAuth1 for Apps Script open-source libraries. You can also connect to external APIs using the UrlFetch service, but this requires you to handle the authorization details explicitly.

After requesting the conference creation, you may need to make additional requests to retrieve the new conference details.

## Initialize conference syncing

Once the add-on has successfully created a conference on a third-party system, it should take a few steps to enable syncing so that changes to the Calendar event are reflected in the conference.

See Syncing Calendar changes for details on setting up syncing after conference creation.

## Build a conference data response

Using the conference information returned by the third-party service, the `onCreateFunction` must then build and return a `ConferenceData` object; the Conference data section describes the content of this object. Calendar uses this information to direct users to the conference once it starts.

When building a `ConferenceData` object, be aware of field lengths, formats of entry point URIs, and allowed combinations of entry points. For example, there can be at most one `VIDEO` entry point in a single `ConferenceData`. These limitations are identical to the limitations described in the Calendar API Event for the corresponding `conferenceData` field, although not all API event fields described there are available in Apps Script.

## Handle errors

Errors can occur during the conference creation process. In some cases the conference creation can't be completed because of an error returned by the third-party conferencing system. In these cases your add-on should handle the error condition by building and returning a `ConferenceData` object containing `ConferenceError` details, so that Calendar can act accordingly.

When constructing a `ConferenceData` object to report an error, you don't need to include any `ConferenceData` components apart from the `ConferenceError` object. `ConferenceError`s can have a `ConferenceErrorType`, an error message, and for authentication issues a URL that allows users to log into the third-party conferencing system.

Your add-on doesn't need to attempt to set up conference syncing if the conference creation attempt failed.

## Example

The following example demonstrates an `onCreateFunction` implementation. The name of the function can be anything; you only need to define it in your add-on project manifest.

The function `create3rdPartyConference` contacts the third-party system to create the conference and the `getAuthenticationUrl` function creates a third-party system authentication URL. These are not fully implemented here.

The function `initializeSyncing` is not shown here; it handles preliminary work required for syncing. See Sync calendar changes for details.

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
