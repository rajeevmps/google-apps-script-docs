# CalendarEvent

Represents a single calendar event.

Represents a single calendar event. The `CalendarEvent` class in Google Apps Script manages properties, guests, and reminders of individual calendar events. Key capabilities include managing reminders (adding, removing, retrieving), handling guests (adding, removing, getting lists, setting permissions), retrieving event information (dates, times, titles, locations), modifying event properties via setter methods, deleting events, and managing custom tags. Most methods require authorization with either read-write (`https://www.googleapis.com/auth/calendar`) or read-only (`https://www.googleapis.com/auth/calendar.readonly`) scopes.

## Methods

### addEmailReminder(minutesBefore)
**Parameters:** `minutesBefore` (Integer)
**Return type:** `CalendarEvent`

Adds a new email reminder to the event. The reminder must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

### addGuest(email)
**Parameters:** `email` (String)
**Return type:** `CalendarEvent`

Adds a guest to the event.

### addPopupReminder(minutesBefore)
**Parameters:** `minutesBefore` (Integer)
**Return type:** `CalendarEvent`

Adds a new pop-up notification to the event. The notification must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

### addSmsReminder(minutesBefore)
**Parameters:** `minutesBefore` (Integer)
**Return type:** `CalendarEvent`

Adds a new SMS reminder to the event. The reminder must be at least 5 minutes, and at most 4 weeks (40320 minutes), before the event.

### anyoneCanAddSelf()
**Return type:** `Boolean`

Determines whether people can add themselves as guests to a Calendar event.

### deleteEvent()
**Return type:** `void`

Deletes a Calendar event.

### deleteTag(key)
**Parameters:** `key` (String)
**Return type:** `CalendarEvent`

Deletes a key/value tag from the event.

### getAllDayEndDate()
**Return type:** `Date`

Gets the date on which this all-day calendar event ends. (If this is not an all-day event, then this method throws an exception.) The returned `Date` represents midnight at the beginning of the day after the event ends in the script's time zone. To use the calendar's time zone instead, call `getEndTime()`.

### getAllDayStartDate()
**Return type:** `Date`

Gets the date on which this all-day calendar event begins. (If this is not an all-day event, then this method throws an exception.) The returned `Date` represents midnight at the beginning of the day on which the event starts in the script's time zone. To use the calendar's time zone instead, call `getStartTime()`.

### getAllTagKeys()
**Return type:** `String[]`

Gets all keys for tags that have been set on the event.

### getColor()
**Return type:** `String`

Returns the color of the calendar event. Returns the string representation of the event color, as an index (1-11) of values from `CalendarApp.EventColor`.

### getCreators()
**Return type:** `String[]`

Gets the creators of an event. Returns the email addresses of the event's creators.

### getDateCreated()
**Return type:** `Date`

Gets the date the event was created. You must have access to the calendar. Returns the date of creation.

### getDescription()
**Return type:** `String`

Gets the description of the event. You must have edit access to the calendar. Returns the description.

### getEmailReminders()
**Return type:** `Integer[]`

Gets the minute values for all email reminders for the event.

### getEndTime()
**Return type:** `Date`

Gets the date and time at which this calendar event ends.

### getEventSeries()
**Return type:** `CalendarEventSeries`

Gets the series of recurring events that this event belongs to.

### getEventType()
**Return type:** `EventType`

Gets the `EventType` of this event.

### getGuestByEmail(email)
**Parameters:** `email` (String)
**Return type:** `EventGuest`

Gets a guest by email address.

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

### getStartTime()
**Return type:** `Date`

Gets the date and time at which this calendar event begins.

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

### isAllDayEvent()
**Return type:** `Boolean`

Determines whether this is an all-day event.

### isOwnedByMe()
**Return type:** `Boolean`

Determines whether you're the owner of the event.

### isRecurringEvent()
**Return type:** `Boolean`

Determines whether the event is part of an event series.

### removeAllReminders()
**Return type:** `CalendarEvent`

Removes all reminders from the event.

### removeGuest(email)
**Parameters:** `email` (String)
**Return type:** `CalendarEvent`

Removes a guest from the event.

### resetRemindersToDefault()
**Return type:** `CalendarEvent`

Resets the reminders using the calendar's default settings.

### setAllDayDate(date)
**Parameters:** `date` (Date)
**Return type:** `CalendarEvent`

Sets the date of the event.

### setAllDayDates(startDate, endDate)
**Parameters:** `startDate` (Date), `endDate` (Date)
**Return type:** `CalendarEvent`

Sets the dates of the event.

### setAnyoneCanAddSelf(anyoneCanAddSelf)
**Parameters:** `anyoneCanAddSelf` (Boolean)
**Return type:** `CalendarEvent`

Sets whether non-guests can add themselves to the event.

### setColor(color)
**Parameters:** `color` (String)
**Return type:** `CalendarEvent`

Sets the color of the calendar event.

### setDescription(description)
**Parameters:** `description` (String)
**Return type:** `CalendarEvent`

Sets the description of the event.

### setGuestsCanInviteOthers(guestsCanInviteOthers)
**Parameters:** `guestsCanInviteOthers` (Boolean)
**Return type:** `CalendarEvent`

Sets whether guests can invite other guests.

### setGuestsCanModify(guestsCanModify)
**Parameters:** `guestsCanModify` (Boolean)
**Return type:** `CalendarEvent`

Sets whether guests can modify the event.

### setGuestsCanSeeGuests(guestsCanSeeGuests)
**Parameters:** `guestsCanSeeGuests` (Boolean)
**Return type:** `CalendarEvent`

Sets whether guests can see other guests.

### setLocation(location)
**Parameters:** `location` (String)
**Return type:** `CalendarEvent`

Sets the location of the event.

### setMyStatus(status)
**Parameters:** `status` (GuestStatus)
**Return type:** `CalendarEvent`

Sets the event status (such as attending or invited) of the effective user.

### setTag(key, value)
**Parameters:** `key` (String), `value` (String)
**Return type:** `CalendarEvent`

Sets a key/value tag on the event, for storing custom metadata.

### setTime(startTime, endTime)
**Parameters:** `startTime` (Date), `endTime` (Date)
**Return type:** `CalendarEvent`

Sets the dates and times for the start and end of the event.

### setTitle(title)
**Parameters:** `title` (String)
**Return type:** `CalendarEvent`

Sets the title of the event.

### setTransparency(transparency)
**Parameters:** `transparency` (EventTransparency)
**Return type:** `CalendarEvent`

Sets the transparency of the event.

### setVisibility(visibility)
**Parameters:** `visibility` (Visibility)
**Return type:** `CalendarEvent`

Sets the visibility of the event.
