# CalendarEventSeries

Represents a series of events (a recurring event).

Represents a series of events (a recurring event). The CalendarEventSeries object enables management of recurring calendar events through Google Apps Script, providing capabilities to modify event properties, manage guest lists, configure reminders, and handle event recurrence settings.

## Methods

### addEmailReminder(minutesBefore)
**Return type:** `CalendarEventSeries`

Adds a new email reminder to the event. The reminder must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

```javascript
const event = CalendarApp.getEventById('abc123456');
event.addEmailReminder(15);
```

### addGuest(email)
**Parameters:** `email` (String)
**Return type:** `CalendarEventSeries`

Adds a guest to the event.

```javascript
const attendeeEmail = 'user@example.com';
const event = calendar.getEventById(eventId);
event.addGuest(attendeeEmail);
```

### addPopupReminder(minutesBefore)
**Parameters:** `minutesBefore` (Integer)
**Return type:** `CalendarEventSeries`

Adds a new pop-up notification to the event. The notification must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

```javascript
const event = CalendarApp.getEventById('abc123456');
event.addPopupReminder(15);
```

### addSmsReminder(minutesBefore)
**Parameters:** `minutesBefore` (Integer)
**Return type:** `CalendarEventSeries`

Adds a new SMS reminder to the event. The reminder must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

### anyoneCanAddSelf()
**Return type:** `Boolean`

Determines whether people can add themselves as guests to a Calendar event.

```javascript
const event = CalendarApp.getEventById('abc123456');
console.log(event.anyoneCanAddSelf());
```

### deleteEventSeries()
**Return type:** `void`

Deletes the event series.

### deleteTag(key)
**Parameters:** `key` (String)
**Return type:** `CalendarEventSeries`

Deletes a key/value tag from the event.

### getAllTagKeys()
**Return type:** `String[]`

Gets all keys for tags that have been set on the event.

### getColor()
**Return type:** `String`

Returns the color of the calendar event.

```javascript
const event = CalendarApp.getEventById('abc123456');
const eventColor = event.getColor();
console.log(eventColor);
```

### getCreators()
**Return type:** `String[]`

Gets the creators of an event.

```javascript
const event = CalendarApp.getEventById('abc123456');
console.log(event.getCreators());
```

### getDateCreated()
**Return type:** `Date`

Gets the date the event was created. You must have access to the calendar.

```javascript
const event = calendar.getEvents(
    new Date('Feb 01, 2023 08:10:00'),
    new Date('Feb 01, 2023 16:25:00'),
)[0];
const eventCreated = event.getDateCreated();
console.log(eventCreated);
```

### getDescription()
**Return type:** `String`

Gets the description of the event. You must have edit access to the calendar.

```javascript
const event = calendar.getEvents(
    new Date('Feb 04, 2023 16:00:00'),
    new Date('Feb 04, 2023 17:00:00'),
)[0];
event.setDescription('Important meeting');
const description = event.getDescription();
console.log(description);
```

### getEmailReminders()
**Return type:** `Integer[]`

Gets the minute values for all email reminders for the event. You must have edit access to the calendar.

```javascript
const event = calendar.getEvents(
    new Date('Feb 04, 2023 15:00:00'),
    new Date('Feb 04, 2023 18:00:00'),
)[0];
event.addEmailReminder(4);
event.addEmailReminder(7);
const emailReminder = event.getEmailReminders();
console.log(emailReminder);
```

### getEventType()
**Return type:** `EventType`

Gets the EventType of this event.

```javascript
const calendar = CalendarApp.getDefaultCalendar();
const events = calendar.getEventsForDay(new Date());
console.log(events.filter(e => e.getEventType() === CalendarApp.EventType.OUT_OF_OFFICE));
```

### getGuestByEmail(email)
**Parameters:** `email` (String)
**Return type:** `EventGuest`

Gets a guest by email address.

```javascript
const event = calendar.getEvents(
    new Date('Feb 25,2023 17:00:00'),
    new Date('Feb 25,2023 17:25:00'),
)[0];
const guestEmailId = event.getGuestByEmail('alex@example.com');
if (guestEmailId) {
  console.log(guestEmailId.getEmail());
}
```

### getGuestList()
**Return type:** `EventGuest[]`

Gets the guests for the event, not including the event owner.

### getGuestList(includeOwner)
**Parameters:** `includeOwner` (Boolean)
**Return type:** `EventGuest[]`

Gets the guests for the event, potentially including the event owners.

### getId()
**Return type:** `String`

Gets the unique iCalUID of the event.

### getLastUpdated()
**Return type:** `Date`

Gets the date the event was last updated.

### getLocation()
**Return type:** `String`

Gets the location of the event.

### getMyStatus()
**Return type:** `GuestStatus`

Gets the event status (such as attending or invited) of the effective user.

### getOriginalCalendarId()
**Return type:** `String`

Get the ID of the calendar where this event was originally created.

### getPopupReminders()
**Return type:** `Integer[]`

Gets the minute values for all pop-up reminders for the event.

### getSmsReminders()
**Return type:** `Integer[]`

Gets the minute values for all SMS reminders for the event.

### getTag(key)
**Parameters:** `key` (String)
**Return type:** `String`

Gets a tag value of the event.

### getTitle()
**Return type:** `String`

Gets the title of the event.

### getTransparency()
**Return type:** `EventTransparency`

Gets the transparency of the event.

### getVisibility()
**Return type:** `Visibility`

Gets the visibility of the event.

### guestsCanInviteOthers()
**Return type:** `Boolean`

Determines whether guests can invite other guests.

### guestsCanModify()
**Return type:** `Boolean`

Determines whether guests can modify the event.

### guestsCanSeeGuests()
**Return type:** `Boolean`

Determines whether guests can see other guests.

### isOwnedByMe()
**Return type:** `Boolean`

Determines whether you're the owner of the event.

### removeAllReminders()
**Return type:** `CalendarEventSeries`

Removes all reminders from the event.

### removeGuest(email)
**Parameters:** `email` (String)
**Return type:** `CalendarEventSeries`

Removes a guest from the event.

### resetRemindersToDefault()
**Return type:** `CalendarEventSeries`

Resets the reminders using the calendar's default settings.

### setAnyoneCanAddSelf(anyoneCanAddSelf)
**Parameters:** `anyoneCanAddSelf` (Boolean)
**Return type:** `CalendarEventSeries`

Sets whether non-guests can add themselves to the event.

### setColor(color)
**Parameters:** `color` (String)
**Return type:** `CalendarEventSeries`

Sets the color of the calendar event.

### setDescription(description)
**Parameters:** `description` (String)
**Return type:** `CalendarEventSeries`

Sets the description of the event.

### setGuestsCanInviteOthers(guestsCanInviteOthers)
**Parameters:** `guestsCanInviteOthers` (Boolean)
**Return type:** `CalendarEventSeries`

Sets whether guests can invite other guests.

### setGuestsCanModify(guestsCanModify)
**Parameters:** `guestsCanModify` (Boolean)
**Return type:** `CalendarEventSeries`

Sets whether guests can modify the event.

### setGuestsCanSeeGuests(guestsCanSeeGuests)
**Parameters:** `guestsCanSeeGuests` (Boolean)
**Return type:** `CalendarEventSeries`

Sets whether guests can see other guests.

### setLocation(location)
**Parameters:** `location` (String)
**Return type:** `CalendarEventSeries`

Sets the location of the event.

### setMyStatus(status)
**Parameters:** `status` (GuestStatus)
**Return type:** `CalendarEventSeries`

Sets the event status (such as attending or invited) of the effective user.

### setRecurrence(recurrence, startDate)
**Parameters:** `recurrence` (EventRecurrence), `startDate` (Date)
**Return type:** `CalendarEventSeries`

Sets the recurrence rules for an all-day event series.

### setRecurrence(recurrence, startTime, endTime)
**Parameters:** `recurrence` (EventRecurrence), `startTime` (Date), `endTime` (Date)
**Return type:** `CalendarEventSeries`

Sets the recurrence rules for this event series.

### setTag(key, value)
**Parameters:** `key` (String), `value` (String)
**Return type:** `CalendarEventSeries`

Sets a key/value tag on the event, for storing custom metadata.

### setTitle(title)
**Parameters:** `title` (String)
**Return type:** `CalendarEventSeries`

Sets the title of the event.

### setTransparency(transparency)
**Parameters:** `transparency` (EventTransparency)
**Return type:** `CalendarEventSeries`

Sets the transparency of the event.

### setVisibility(visibility)
**Parameters:** `visibility` (Visibility)
**Return type:** `CalendarEventSeries`

Sets the visibility of the event.
