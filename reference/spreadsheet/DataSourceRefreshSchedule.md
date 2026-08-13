# DataSourceRefreshSchedule

Access and modify an existing refresh schedule.

Access and modify an existing refresh schedule. To get all refresh schedules, see `Spreadsheet.getDataSourceRefreshSchedules()`. Only use this class with data that's connected to a database.

## Methods

| Method | Return Type | Description |
|---|---|---|
| `getFrequency()` | `DataSourceRefreshScheduleFrequency` | Gets the refresh schedule frequency, which specifies how often and when to refresh. |
| `getScope()` | `DataSourceRefreshScope` | Gets the scope of this refresh schedule. |
| `getTimeIntervalOfNextRun()` | `TimeInterval` | Gets the time window of the next run of this refresh schedule. Only applies if this refresh schedule is enabled. |
| `isEnabled()` | `Boolean` | Determines whether this refresh schedule is enabled. |

## Authorization

All methods require one or more of these scopes:
- `https://www.googleapis.com/auth/spreadsheets.currentonly`
- `https://www.googleapis.com/auth/spreadsheets`
