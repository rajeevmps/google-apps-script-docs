# ClockTriggerBuilder

A builder for clock triggers.

A builder for clock triggers.

## Methods

### after(durationMilliseconds: Integer) → ClockTriggerBuilder

Specifies the minimum duration (in milliseconds) after the current time that the trigger runs. The actual duration might vary, but won't be less than your specified minimum.

**Parameters:**
- `durationMilliseconds` (`Integer`): The minimum duration (in milliseconds) after the current time when the trigger should run.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().after(10 * 60 * 1000).create();
```

### at(date: Date) → ClockTriggerBuilder

Specifies when the trigger runs.

**Parameters:**
- `date` (`Date`): A Date object representing when the trigger should run.

```javascript
const triggerDay = new Date(2012, 11, 1);
ScriptApp.newTrigger('myFunction').timeBased().at(triggerDay).create();
```

### atDate(year: Integer, month: Integer, day: Integer) → ClockTriggerBuilder

Specifies that the trigger fires on the given date, by default near midnight (+/- 15 minutes).

**Parameters:**
- `year` (`Integer`): The calendar year to schedule the trigger.
- `month` (`Integer`): The calendar month to schedule the trigger (should be a number between 1 and 12, inclusive).
- `day` (`Integer`): The calendar day to schedule the trigger (should be a number between 1 and 31, inclusive).

```javascript
ScriptApp.newTrigger('myFunction').timeBased().atDate(2013, 1, 1).create();
```

### atHour(hour: Integer) → ClockTriggerBuilder

Specifies the hour the trigger at which the trigger runs.

**Parameters:**
- `hour` (`Integer`): The hour at which to fire.

```javascript
ScriptApp.newTrigger('myFunction')
    .timeBased()
    .atHour(5)
    .everyDays(1)
    .create();
```

### create() → Trigger

Creates the trigger.

**Return:** `Trigger` — The newly created, scheduled trigger.

### everyDays(n: Integer) → ClockTriggerBuilder

Specifies to run the trigger every `n` days.

**Parameters:**
- `n` (`Integer`): The number of days between executions.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().everyDays(3).create();
```

### everyHours(n: Integer) → ClockTriggerBuilder

Specifies to run the trigger every `n` hours.

**Parameters:**
- `n` (`Integer`): The number of hours between executions.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().everyHours(12).create();
```

### everyMinutes(n: Integer) → ClockTriggerBuilder

Specifies to run the trigger every `n` minutes. `n` must be 1, 5, 10, 15 or 30.

**Parameters:**
- `n` (`Integer`): The number of minutes between executions.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().everyMinutes(10).create();
```

### everyWeeks(n: Integer) → ClockTriggerBuilder

Specifies to run the trigger every `n` weeks.

**Parameters:**
- `n` (`Integer`): The number of weeks between executions.

```javascript
ScriptApp.newTrigger('myFunction')
    .timeBased()
    .everyWeeks(2)
    .onWeekDay(ScriptApp.WeekDay.FRIDAY)
    .create();
```

### inTimezone(timezone: String) → ClockTriggerBuilder

Specifies the timezone for the specified dates/time when the trigger runs. By default, the timezone is that of the script. The list of valid timezone strings corresponds with the valid timezone strings listed by Joda.org. An invalid timezone string causes the script to throw an error.

**Parameters:**
- `timezone` (`String`): The timezone with which to treat time information in the event.

```javascript
ScriptApp.newTrigger('myFunction')
    .timeBased()
    .atHour(12)
    .everyDays(1)
    .inTimezone('America/Los_Angeles')
    .create();
```

### nearMinute(minute: Integer) → ClockTriggerBuilder

Specifies the minute at which the trigger runs (plus or minus 15 minutes). If `nearMinute()` is not called, a random minute value is used.

**Parameters:**
- `minute` (`Integer`): The minute at which to fire.

```javascript
ScriptApp.newTrigger('myFunction')
    .timeBased()
    .atHour(5)
    .nearMinute(30)
    .everyDays(1)
    .create();
```

### onMonthDay(day: Integer) → ClockTriggerBuilder

Specifies the date in the month that the trigger runs.

**Parameters:**
- `day` (`Integer`): The day of the month the trigger should be scheduled for.

```javascript
ScriptApp.newTrigger('myFunction').timeBased().onMonthDay(1).create();
```

### onWeekDay(day: Weekday) → ClockTriggerBuilder

Specifies the day of the week that the trigger runs.

**Parameters:**
- `day` (`Weekday`): The day of the week to fire.

```javascript
ScriptApp.newTrigger('myFunction')
    .timeBased()
    .onWeekDay(ScriptApp.WeekDay.FRIDAY)
    .create();
```
