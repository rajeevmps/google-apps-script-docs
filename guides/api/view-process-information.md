# View process information

## Page Summary

- "The Apps Script API provides methods to list your script processes."
- "The `processes.list` method returns metadata for processes you have run."
- "The `processes.listScriptProcesses` method returns metadata for processes run from a specific script project."
- "Both methods can be filtered to narrow down the results."

## API method overview

### List your processes

**processes.list**

**Results**: Returns an array of `Process` objects, each containing the metadata for a process you have run. This information includes the process type, status, start time, and duration.

**Options**: You can define and provide a `ListUserProcessFilter` object to filter the process list. Only processes that match **all** of the filter conditions are returned.

### List a project's processes

**processes.listScriptProcesses**

**Results**: Returns an array of `Process` objects, each containing the metadata for a process run from a specified script project. This information includes the process type, status, start time, and duration.

**Options**: You can define and provide a `ListScriptProcessesFilter` object to filter the process list. Only processes that match **all** of the filter conditions are returned.

Source: https://developers.google.com/apps-script/api/how-tos/view-processes
