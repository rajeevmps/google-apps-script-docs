# Calendar

A calendar that the user owns or is subscribed to.

The Calendar class represents a calendar owned or subscribed to by the user and provides methods for managing events. Key capabilities include creating all-day events, standard events, and recurring event series with various options; retrieving events by ID, time range, or day with filtering options; managing calendar properties such as color, description, name, and time zone; checking calendar visibility, ownership, and selection status; and deleting or unsubscribing from calendars.

## Methods

### createAllDayEvent(title, date)
**Return type:** `CalendarEvent`

Creates a new all-day event for a single date.

```javascript
const event = CalendarApp.getDefaultCalendar().createAllDayEvent(
    'Apollo 11 Landing',
    new Date('July 20, 1969'),
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createAllDayEvent(title, startDate, endDate)
**Return type:** `CalendarEvent`

Creates an all-day event spanning multiple days.

### createAllDayEvent(title, startDate, endDate, options)
**Return type:** `CalendarEvent`

Creates multi-day all-day event with advanced parameters (description, location, guests, sendInvites).

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

Creates single-day all-day event with advanced options.

### createAllDayEventSeries(title, startDate, recurrence)
**Return type:** `CalendarEventSeries`

Creates recurring all-day event series.

### createAllDayEventSeries(title, startDate, recurrence, options)
**Return type:** `CalendarEventSeries`

Creates recurring all-day series with advanced parameters.

### createEvent(title, startTime, endTime)
**Return type:** `CalendarEvent`

Creates standard timed event.

### createEvent(title, startTime, endTime, options)
**Return type:** `CalendarEvent`

Creates timed event with advanced options.

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

Creates event from free-form text description using Quick Add format.

```javascript
const event = CalendarApp.getDefaultCalendar().createEventFromDescription(
    'Lunch with Mary, Friday at 1PM',
);
Logger.log(`Event ID: ${event.getId()}`);
```

### createEventSeries(title, startTime, endTime, recurrence)
**Return type:** `CalendarEventSeries`

Creates recurring timed event series.

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

Creates recurring timed series with advanced parameters.

### deleteCalendar()
**Return type:** `void`

Permanently removes calendar (owner only). Throws an Error for imported calendars.

```javascript
const calendar = CalendarApp.createCalendar('Test');
calendar.deleteCalendar();
```

### getColor()
**Return type:** `String`

Returns hexadecimal color string ("#rrggbb").

```javascript
const calendar = CalendarApp.getCalendarById('222larabrown@gmail.com');
const calendarColor = calendar.getColor();
console.log(calendarColor);
```

### getDescription()
**Return type:** `String`

Returns calendar description text.

### getEventById(iCalId)
**Return type:** `CalendarEvent`

Retrieves specific event by ID.

### getEventSeriesById(iCalId)
**Return type:** `CalendarEventSeries`

Retrieves specific event series by ID.

### getEvents(startTime, endTime)
**Return type:** `CalendarEvent[]`

Retrieves all events within time range.

### getEvents(startTime, endTime, options)
**Return type:** `CalendarEvent[]`

Retrieves events within time range meeting specified criteria.

### getEventsForDay(date)
**Return type:** `CalendarEvent[]`

Retrieves all events occurring on specific date.

### getEventsForDay(date, options)
**Return type:** `CalendarEvent[]`

Retrieves events for date meeting specified criteria.

### getId()
**Return type:** `String`

Returns calendar identifier.

### getName()
**Return type:** `String`

Returns calendar name.

### getTimeZone()
**Return type:** `String`

Returns calendar time zone setting.

### isHidden()
**Return type:** `Boolean`

Determines visibility in user interface.

### isMyPrimaryCalendar()
**Return type:** `Boolean`

Checks if this is user's primary calendar.

### isOwnedByMe()
**Return type:** `Boolean`

Determines calendar ownership.

### isSelected()
**Return type:** `Boolean`

Determines if events display in interface.

### setColor(color)
**Return type:** `Calendar`

Sets calendar color; returns modified calendar object.

### setDescription(description)
**Return type:** `Calendar`

Sets calendar description; returns modified calendar object.

### setHidden(hidden)
**Return type:** `Calendar`

Sets calendar visibility; returns modified calendar.

### setName(name)
**Return type:** `Calendar`

Sets calendar name; returns modified calendar object.

### setSelected(selected)
**Return type:** `Calendar`

Sets event display status; returns modified calendar.

### setTimeZone(timeZone)
**Return type:** `Calendar`

Sets calendar time zone; returns modified calendar object.

### unsubscribeFromCalendar()
**Return type:** `void`

Unsubscribes user from calendar.
