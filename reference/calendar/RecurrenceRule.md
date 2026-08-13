# RecurrenceRule

Represents a recurrence rule for an event series.

Represents a recurrence rule for an event series. The class enables chaining rule creation together, allowing multiple rules to be combined. Modifiers like `times(times)` and `interval(interval)` are applied to the most recently added rule.

## Methods

### addDailyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a daily basis.

```javascript
const recurrence = CalendarApp.newRecurrence().addDailyRule().times(3).interval(2).addWeeklyExclusion().times(2);
```

### addDailyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a daily basis.

```javascript
const recurrence = CalendarApp.newRecurrence().addDailyRule().times(10);
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

Adds a rule that excludes occurrences on a monthly basis. By default the exclusion is applied on the same day of the month as the first event in the series, but this can be altered by calling `onlyOnMonthDay(day)` or `onlyOnMonthDays(days)`.

```javascript
const recurrence = CalendarApp.newRecurrence().addMonthlyRule().times(4);
```

### addMonthlyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a monthly basis. By default the event recurs on the same day of the month as the first event in the series, but this can be altered by calling `onlyOnMonthDay(day)` or `onlyOnMonthDays(days)`.

### addWeeklyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a weekly basis. By default the exclusion is applied on the same day of the week as the first event in the series, but this can be altered by calling `onlyOnWeekday(day)` or `onlyOnWeekdays(days)`.

```javascript
const recurrence = CalendarApp.newRecurrence()
    .addDailyRule()
    .addWeeklyExclusion()
    .onlyOnWeekday(CalendarApp.Weekday.WEDNESDAY)
    .times(4);
```

### addWeeklyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a weekly basis. By default the event recurs on the same day of the week as the first event in the series, but this can be altered by calling `onlyOnWeekday(day)` or `onlyOnWeekdays(days)`.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().times(10);
```

### addYearlyExclusion()
**Return type:** `RecurrenceRule`

Adds a rule that excludes occurrences on a yearly basis. By default the exclusion is applied on the same day of the year as the first event in the series, but this can be altered by calling `onlyOnYearDay(day)` or `onlyOnYearDays(days)`.

### addYearlyRule()
**Return type:** `RecurrenceRule`

Adds a rule that causes the event to recur on a yearly basis. By default the event recurs on the same day of the year as the first event in the series, but this can be altered by calling `onlyOnYearDay(day)` or `onlyOnYearDays(days)`.

```javascript
const recurrence = CalendarApp.newRecurrence().addYearlyRule().onlyOnYearDay(46);
```

### interval(interval)
**Parameters:** `interval` (Integer)
**Return type:** `RecurrenceRule`

Configures the rule to only apply at this interval of the rule's time unit.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().interval(4);
```

### onlyInMonth(month)
**Parameters:** `month` (Month)
**Return type:** `RecurrenceRule`

Configures the rule to only apply to a specific month.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyInMonth(
    CalendarApp.Month.FEBRUARY);
```

### onlyInMonths(months)
**Parameters:** `months` (Month[])
**Return type:** `RecurrenceRule`

Configures the rule to only apply to specific months.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyInMonths(
    [CalendarApp.Month.FEBRUARY, CalendarApp.Month.MARCH]);
```

### onlyOnMonthDay(day)
**Parameters:** `day` (Integer)
**Return type:** `RecurrenceRule`

Configures the rule to only apply to a specific day of the month.

```javascript
const recurrence = CalendarApp.newRecurrence().addMonthlyRule().onlyOnMonthDay(5);
```

### onlyOnMonthDays(days)
**Parameters:** `days` (Integer[])
**Return type:** `RecurrenceRule`

Configures the rule to only apply to specific days of the month.

```javascript
const recurrence = CalendarApp.newRecurrence().addMonthlyRule().onlyOnMonthDays([1, 15]);
```

### onlyOnWeek(week)
**Parameters:** `week` (Integer)
**Return type:** `RecurrenceRule`

Configures the rule to only apply to a specific week of the year.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyOnWeek(5);
```

### onlyOnWeekday(day)
**Parameters:** `day` (Weekday)
**Return type:** `RecurrenceRule`

Configures the rule to only apply to a specific day of the week.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyOnWeekday(
    CalendarApp.Weekday.WEDNESDAY);
```

### onlyOnWeekdays(days)
**Parameters:** `days` (Weekday[])
**Return type:** `RecurrenceRule`

Configures the rule to only apply to specific days of the week.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyOnWeekdays(
    [CalendarApp.Weekday.TUESDAY, CalendarApp.Weekday.THURSDAY]);
```

### onlyOnWeeks(weeks)
**Parameters:** `weeks` (Integer[])
**Return type:** `RecurrenceRule`

Configures the rule to only apply to specific weeks of the year.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().onlyOnWeeks([5, 10]);
```

### onlyOnYearDay(day)
**Parameters:** `day` (Integer)
**Return type:** `RecurrenceRule`

Configures the rule to only apply to a specific day of the year.

### onlyOnYearDays(days)
**Parameters:** `days` (Integer[])
**Return type:** `RecurrenceRule`

Configures the rule to only apply to specific days of the year.

```javascript
const recurrence = CalendarApp.newRecurrence().addYearlyRule().onlyOnYearDay([20, 46]);
```

### setTimeZone(timeZone)
**Parameters:** `timeZone` (String)
**Return type:** `EventRecurrence`

Sets the time zone for this recurrence. This affects the date and time that events recur on, and whether the event shifts with daylight savings time. Defaults to the calendar's time zone.

### times(times)
**Parameters:** `times` (Integer)
**Return type:** `RecurrenceRule`

Configures the rule to end after a given number of occurrences.

### until(endDate)
**Parameters:** `endDate` (Date)
**Return type:** `RecurrenceRule`

Configures the rule to end on a given date (inclusive).

```javascript
const recurrence = CalendarApp.newRecurrence().addDailyRule().until(
    new Date('December 31, 2013'));
```

### weekStartsOn(day)
**Parameters:** `day` (Weekday)
**Return type:** `RecurrenceRule`

Configures which day a week starts on, for the purposes of applying the rule.

```javascript
const recurrence = CalendarApp.newRecurrence().addWeeklyRule().weekStartsOn(
    CalendarApp.Weekday.MONDAY);
```
