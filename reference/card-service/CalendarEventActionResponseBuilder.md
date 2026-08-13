# CalendarEventActionResponseBuilder

A builder for CalendarEventActionResponse objects.

CalendarEventActionResponseBuilder is a builder for `CalendarEventActionResponse` objects. Methods like addAttachments, addAttendees, and setConferenceData specify actions to take on a Calendar event when a UI action is triggered. The build method validates and creates the CalendarEventActionResponse object.

## Methods

### addAttachments(attachments: Attachment[]): CalendarEventActionResponseBuilder

Specifies that the response should add the attachments to the Calendar event when the associated UI action is taken.

Parameters:
- `attachments` (Attachment[]): An array of Attachments to add.

Returns: This object, for chaining.

### addAttendees(emails: String[]): CalendarEventActionResponseBuilder

Specifies that the response should add the indicated attendees to the Calendar event when the associated UI action is taken.

Parameters:
- `emails` (String[]): An array of email addresses to add to the event.

Returns: This object, for chaining.

Throws: Error if too many attendees have been added.

### build(): CalendarEventActionResponse

Builds the current Calendar event action response and validates it.

Returns: A validated CalendarEventActionResponse.

Throws: Error if the constructed Calendar event action response isn't valid.

### setConferenceData(conferenceData: ConferenceData): CalendarEventActionResponseBuilder

Specifies that the response should set the indicated conference data to the Calendar event when the associated UI action is taken.

Parameters:
- `conferenceData` (ConferenceData): Conference data to set to the event, created by an add-on.

Returns: This object, for chaining.
