# CalendarEventActionResponse

Represents a response that makes changes to the calendar event that the user is currently editing.

Represents a response that makes changes to the calendar event that the user is currently editing in reaction to an action taken in the UI, such as a button click.

## Methods

### printJson()

`printJson(): String`

Prints the JSON representation of this object. This is for debugging only.

## Code Sample

```javascript
const calendarEventActionResponse =
    AddOnsResponseService.newCalendarEventActionResponseBuilder()
        .addAttendees(['user1@example.com', 'user2@example.com'])
        .build();
```

This example demonstrates creating a CalendarEventActionResponse that adds two attendees to a calendar event.
