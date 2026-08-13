# CalendarEventActionResponse

A response that modifies the calendar event a user is currently editing.

Represents a response that makes changes to the calendar event that the user is currently editing in reaction to an action taken in the UI, such as a button click.

```javascript
const calendarEventActionResponse =
    CardService.newCalendarEventActionResponseBuilder()
        .addAttendees(['user1@example.com', 'user2@example.com'])
        .build();
```

## Methods

### printJson(): String

Prints the JSON representation of this object. This is for debugging only.
