# DataSourceRefreshScheduleFrequency

Access a refresh schedule's frequency.

Access a refresh schedule's frequency, which specifies how often and when to refresh. This class is used exclusively with database-connected data in Google Sheets. It provides access to the configuration details of how often and when a data source refresh occurs.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getDaysOfTheMonth()` | `Integer[]` | Gets the days of the month as numbers (1-28) on which to refresh the data source. Only applies if frequency type is monthly. |
| `getDaysOfTheWeek()` | `Weekday[]` | Gets the days of the week on which to refresh the data source. Only applies if the frequency type is weekly. |
| `getFrequencyType()` | `FrequencyType` | Gets the frequency type. |
| `getStartHour()` | `Integer` | Gets the start hour (as a number 0-23) of the time interval during which the refresh schedule runs. For example, if the start hour is 13 and the time interval's duration is 4 hours, then the data source is refreshed between 1 p.m. and 5 p.m. The hour is in the timezone of the spreadsheet. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
