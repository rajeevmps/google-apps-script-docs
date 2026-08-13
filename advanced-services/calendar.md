# Advanced Calendar Service

Source: https://developers.google.com/apps-script/advanced/calendar

## Overview

The Advanced Calendar Service provides access to the public Google Calendar API within Apps Script. As stated in the documentation, "this advanced service provides a few extra features, including setting the background color for individual events."

## Key Features

**Enhanced Capabilities:**
- Access to Google Calendar API v3
- Setting individual event background colors (not available in the built-in CalendarApp service)
- Support for HTTP request headers like `If-Match` and `If-None-Match`
- Conditional operations on calendar events

## Enabling the Service

This is an advanced service requiring explicit enablement before use, through the Apps Script editor's Services menu (or the manifest's `enabledAdvancedServices`).

## Primary Use Cases

The service supports:
- Creating calendar events with detailed properties
- Listing calendars and upcoming events
- Conditional updates using ETags
- Efficient event synchronization using sync tokens
- Attendee management and color customization

## Code Sample

```javascript
// Creating an event example structure
let event = {
  summary: "Lunch Meeting",
  location: "The Deli",
  start: { dateTime: start.toISOString() },
  end: { dateTime: end.toISOString() },
  colorId: 11  // Red background
};
Calendar.Events.insert(event, calendarId);
```

## Reference Documentation

The service uses the same objects and methods as the [public Google Calendar API reference](https://developers.google.com/calendar/api/v3/reference). For detailed specifications and additional functionality, consult the official Calendar API documentation. (External — not scraped.)
</content>
