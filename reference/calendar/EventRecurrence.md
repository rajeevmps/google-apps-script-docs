# EventRecurrence

Represents the recurrence settings for an event series.

Represents the recurrence settings for an event series. You can add rules to specify daily, weekly, monthly, or yearly recurrences or exclusions for events. Specific dates can be added for event recurrences or excluded from an event series. The time zone for the recurrence can be set, affecting when events recur.

## Methods

### addDailyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a daily basis.

```javascript
// Example: weekly rule with daily exclusion applied 30 times.
```

### addDailyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a daily basis.

```javascript
// Example: Creates recurring daily event for ten days.
```

### addDate(date)
**Parameters:** `date` (Date)
**Return type:** `EventRecurrence`

Adds a rule that causes the event to recur on a specific date.

### addDateExclusion(date)
**Parameters:** `date` (Date)
**Return type:** `EventRecurrence`

Adds a rule that excludes an occurrence for a specific date.

### addMonthlyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a monthly basis. Applies to same day of month as first event by default, alterable via `onlyOnMonthDay()` or `onlyOnMonthDays()`.

### addMonthlyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a monthly basis. Defaults to same day as first event; adjustable via `onlyOnMonthDay()` or `onlyOnMonthDays()`.

### addWeeklyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a weekly basis. Applies to same weekday as first event by default, adjustable via `onlyOnWeekday()` or `onlyOnWeekdays()`.

```javascript
// Example: Daily rule excluding first four Wednesdays.
```

### addWeeklyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a weekly basis. Defaults to same weekday; adjustable via `onlyOnWeekday()` or `onlyOnWeekdays()`.

```javascript
// Example: Weekly recurrence for ten weeks.
```

### addYearlyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a yearly basis. Applies to same day of year as first event by default, modifiable via `onlyOnYearDay()` or `onlyOnYearDays()`.

### addYearlyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a yearly basis. Defaults to same day of year; adjustable via `onlyOnYearDay()` or `onlyOnYearDays()`.

### setTimeZone(timeZone)
**Parameters:** `timeZone` (String) — the time zone, specified in "long" format
**Return type:** `EventRecurrence`

Sets the time zone for this recurrence. This affects the date and time that events recur on, and whether the event shifts with daylight savings time. Defaults to calendar's time zone.
