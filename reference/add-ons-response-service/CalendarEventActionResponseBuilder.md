# CalendarEventActionResponseBuilder

A builder for `CalendarEventActionResponse` objects.

A builder for `CalendarEventActionResponse` objects used in Google Apps Script add-ons.

## Methods

### addAttachments(attachments)

`addAttachments(attachments: Attachment[]): CalendarEventActionResponseBuilder`

Specifies that the response should add the attachments to the Calendar event when the associated UI action is taken.

**Parameters**
- `attachments` (Attachment[]) — An array of Attachments to add.

**Returns**
- `CalendarEventActionResponseBuilder` — This object, for chaining.

### addAttendees(emails)

`addAttendees(emails: String[]): CalendarEventActionResponseBuilder`

Specifies that the response should add the indicated attendees to the Calendar event when the associated UI action is taken.

**Parameters**
- `emails` (String[]) — An array of email addresses to add to the event.

**Returns**
- `CalendarEventActionResponseBuilder` — This object, for chaining.

**Throws:** Error if too many attendees have been added.

### build()

`build(): CalendarEventActionResponse`

Builds the current Calendar event action response and validates it.

**Returns**
- `CalendarEventActionResponse` — A validated CalendarEventActionResponse.

**Throws:** Error if the constructed response isn't valid.

### setConferenceData(conferenceData)

`setConferenceData(conferenceData: ConferenceData): CalendarEventActionResponseBuilder`

Specifies that the response should set the indicated conference data to the Calendar event when the associated UI action is taken.

**Parameters**
- `conferenceData` (ConferenceData) — Conference data to set to the event, created by an add on.

**Returns**
- `CalendarEventActionResponseBuilder` — This object, for chaining.
