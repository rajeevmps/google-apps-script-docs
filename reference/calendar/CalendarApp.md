# CalendarApp

Allows a script to read and update the user's Google Calendar.

Allows a script to read and update the user's Google Calendar. This class provides direct access to the user's default calendar, as well as the ability to retrieve additional calendars that the user owns or is subscribed to.

All methods require authorization with one or more of these scopes:
- `https://www.googleapis.com/auth/calendar`
- `https://www.google.com/calendar/feeds`

## Properties

| Property | Type | Description |
|----------|------|-------------|
| `Color` | `Color` | An enum representing the named colors available in the Calendar service. |
| `EventColor` | `EventColor` | An enum representing the named event colors available in the Calendar service. |
| `EventTransparency` | `EventTransparency` | The EventTransparency enumeration. |
| `EventType` | `EventType` | The EventType enumeration. |
| `GuestStatus` | `GuestStatus` | An enum representing the statuses a guest can have for an event. |
| `Month` | `Month` | An enum representing the months of the year. |
| `Visibility` | `Visibility` | An enum representing the visibility of an event. |
| `Weekday` | `Weekday` | An enum representing the days of the week. |

## Methods

### createAllDayEvent(title, date)
**Return type:** `CalendarEvent`

Creates a new all-day event.

```javascript
const event = CalendarApp.getDefaultCalendar().createAllDayEvent(
    'Apollo 11 Landing',
    new Date('July 20, 1969'),
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createAllDayEvent(title, startDate, endDate)
**Return type:** `CalendarEvent`

Creates a new all-day event that can span multiple days.

```javascript
const event = CalendarApp.getDefaultCalendar().createAllDayEvent(
    'Woodstock Festival',
    new Date('August 15, 1969'),
    new Date('August 18, 1969'),
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createAllDayEvent(title, startDate, endDate, options)
**Return type:** `CalendarEvent`

Creates a new all-day event that can span multiple days, with advanced parameters (description, location, guests, sendInvites).

```javascript
const event = CalendarApp.getDefaultCalendar().createAllDayEvent(
    'Woodstock Festival',
    new Date('August 15, 1969'),
    new Date('August 18, 1969'),
    {location: 'Bethel, White Lake, New York, U.S.', sendInvites: true},
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createAllDayEvent(title, date, options)
**Return type:** `CalendarEvent`

Creates a new all-day event with advanced parameters.

```javascript
const event = CalendarApp.getDefaultCalendar().createAllDayEvent(
    'Apollo 11 Landing',
    new Date('July 20, 1969'),
    {location: 'The Moon'},
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createAllDayEventSeries(title, startDate, recurrence)
**Return type:** `CalendarEventSeries`

Creates a new all-day event series.

```javascript
const eventSeries = CalendarApp.getDefaultCalendar().createAllDayEventSeries(
    'No Meetings',
    new Date('January 2, 2013 03:00:00 PM EST'),
    CalendarApp.newRecurrence()
        .addWeeklyRule()
        .onlyOnWeekday(CalendarApp.Weekday.WEDNESDAY)
        .until(new Date('January 1, 2014')),
);
Logger.log(`Event Series ID: ${eventSeries.getId()}`);
```

### createAllDayEventSeries(title, startDate, recurrence, options)
**Return type:** `CalendarEventSeries`

Creates a new all-day event series with advanced parameters (description, location, guests, sendInvites).

```javascript
const eventSeries = CalendarApp.getDefaultCalendar().createAllDayEventSeries(
    'No Meetings',
    new Date('January 2, 2013 03:00:00 PM EST'),
    CalendarApp.newRecurrence()
        .addWeeklyRule()
        .onlyOnWeekday(CalendarApp.Weekday.WEDNESDAY)
        .until(new Date('January 1, 2014')),
    {guests: 'everyone@example.com'},
);
Logger.log(`Event Series ID: ${eventSeries.getId()}`);
```

### createCalendar(name)
**Return type:** `Calendar`

Creates a new calendar, owned by the user.

```javascript
const calendar = CalendarApp.createCalendar('Travel Plans');
Logger.log(
    'Created the calendar "%s", with the ID "%s".',
    calendar.getName(),
    calendar.getId(),
);
```

### createCalendar(name, options)
**Return type:** `Calendar`

Creates a new calendar with advanced parameters (location, description, timeZone, color, hidden, selected).

```javascript
const calendar = CalendarApp.createCalendar('Travel Plans', {
  description: 'A calendar to plan my travel schedule.',
  color: CalendarApp.Color.BLUE,
});
Logger.log(
    'Created the calendar "%s", with the ID "%s".',
    calendar.getName(),
    calendar.getId(),
);
```

### createEvent(title, startTime, endTime)
**Return type:** `CalendarEvent`

Creates a new event. If no time zone is specified, the time values are interpreted in the context of the script's time zone, which may be different than the calendar's time zone.

```javascript
const event = CalendarApp.getDefaultCalendar().createEvent(
    'Apollo 11 Landing',
    new Date('July 20, 1969 20:00:00 UTC'),
    new Date('July 21, 1969 21:00:00 UTC'),
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createEvent(title, startTime, endTime, options)
**Return type:** `CalendarEvent`

Creates a new event with advanced parameters (description, location, guests, sendInvites).

```javascript
const event = CalendarApp.getDefaultCalendar().createEvent(
    'Apollo 11 Landing',
    new Date('July 20, 1969 20:00:00 UTC'),
    new Date('July 20, 1969 21:00:00 UTC'),
    {location: 'The Moon'},
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createEventFromDescription(description)
**Return type:** `CalendarEvent`

Creates an event from a free-form description using the same format as the UI's "Quick Add" feature.

```javascript
const event = CalendarApp.getDefaultCalendar().createEventFromDescription(
    'Lunch with Mary, Friday at 1PM',
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createEventSeries(title, startTime, endTime, recurrence)
**Return type:** `CalendarEventSeries`

Creates a new event series.

```javascript
const eventSeries = CalendarApp.getDefaultCalendar().createEventSeries(
    'Team Meeting',
    new Date('January 1, 2013 03:00:00 PM EST'),
    new Date('January 1, 2013 04:00:00 PM EST'),
    CalendarApp.newRecurrence()
        .addWeeklyRule()
        .onlyOnWeekdays([CalendarApp.Weekday.TUESDAY, CalendarApp.Weekday.THURSDAY])
        .until(new Date('January 1, 2014')),
);
Logger.log(`Event Series ID: ${eventSeries.getId()}`);
```

### createEventSeries(title, startTime, endTime, recurrence, options)
**Return type:** `CalendarEventSeries`

Creates a new event series with advanced parameters.

### getAllCalendars()
**Return type:** `Calendar[]`

Gets all calendars that the user owns or is subscribed to.

### getAllOwnedCalendars()
**Return type:** `Calendar[]`

Gets all calendars that the user owns.

### getCalendarById(id)
**Return type:** `Calendar|null`

Gets the calendar with the given ID.

### getCalendarsByName(name)
**Return type:** `Calendar[]`

Gets all calendars with a given name that the user owns or is subscribed to.

### getColor()
**Return type:** `String`

Gets the color of the calendar.

### getDefaultCalendar()
**Return type:** `Calendar`

Gets the user's default calendar.

### getDescription()
**Return type:** `String`

Gets the description of the calendar.

### getEventById(iCalId)
**Return type:** `CalendarEvent`

Gets the event with the given ID.

### getEventSeriesById(iCalId)
**Return type:** `CalendarEventSeries`

Gets the event series with the given ID.

### getEvents(startTime, endTime)
**Return type:** `CalendarEvent[]`

Gets all events that occur within a given time range.

### getEvents(startTime, endTime, options)
**Return type:** `CalendarEvent[]`

Gets all events that occur within a given time range and meet the specified criteria.

### getEventsForDay(date)
**Return type:** `CalendarEvent[]`

Gets all events that occur on a given day.

### getEventsForDay(date, options)
**Return type:** `CalendarEvent[]`

Gets all events that occur on a given day and meet specified criteria.

### getId()
**Return type:** `String`

Gets the ID of the calendar.

### getName()
**Return type:** `String`

Gets the name of the calendar.

### getOwnedCalendarById(id)
**Return type:** `Calendar|null`

Gets the calendar with the given ID, if the user owns it.

### getOwnedCalendarsByName(name)
**Return type:** `Calendar[]`

Gets all calendars with a given name that the user owns.

### getTimeZone()
**Return type:** `String`

Gets the time zone of the calendar.

### isHidden()
**Return type:** `Boolean`

Determines whether the calendar is hidden in the user interface.

### isMyPrimaryCalendar()
**Return type:** `Boolean`

Determines whether the calendar is the primary calendar for the effective user.

### isOwnedByMe()
**Return type:** `Boolean`

Determines whether the calendar is owned by you.

### isSelected()
**Return type:** `Boolean`

Determines whether the calendar's events are displayed in the user interface.

### newRecurrence()
**Return type:** `EventRecurrence`

Creates a new recurrence object, which can be used to create rules for event recurrence.

### setColor(color)
**Return type:** `Calendar`

Sets the color of the calendar.

### setDescription(description)
**Return type:** `Calendar`

Sets the description of a calendar.

### setHidden(hidden)
**Return type:** `Calendar`

Sets whether the calendar is visible in the user interface.

### setName(name)
**Return type:** `Calendar`

Sets the name of the calendar.

### setSelected(selected)
**Return type:** `Calendar`

Sets whether the calendar's events are displayed in the user interface.

### setTimeZone(timeZone)
**Return type:** `Calendar`

Sets the time zone of the calendar.

### subscribeToCalendar(id)
**Return type:** `Calendar`

Subscribes the user to the calendar with the given ID, if the user is allowed to subscribe.

### subscribeToCalendar(id, options)
**Return type:** `Calendar`

Subscribes the user to the calendar with the given ID with options (color, hidden, selected).
