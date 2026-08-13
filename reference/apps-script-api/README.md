# Apps Script API — Overview

Source: https://developers.google.com/apps-script/api/reference/rest

## Service Description

The Apps Script API "manages and executes Google Apps Script projects," providing REST resources for processes, projects, deployments, versions, and scripts.

## Service Endpoint

- **Base URL:** `https://script.googleapis.com`
- **Discovery Document:** `https://script.googleapis.com/$discovery/rest?version=v1`

## Primary REST Resources

### v1.processes
- `list` – GET `/v1/processes` – View process information like type and status
- `listScriptProcesses` – GET `/v1/processes:listScriptProcesses` – Access script execution data

### v1.projects
- `create` – POST `/v1/projects` – Initialize new script project
- `get` – GET `/v1/projects/{scriptId}` – Retrieve project metadata
- `getContent` – GET `/v1/projects/{scriptId}/content` – Fetch code and file details
- `getMetrics` – GET `/v1/projects/{scriptId}/metrics` – Obtain execution statistics
- `updateContent` – PUT `/v1/projects/{scriptId}/content` – Modify project code

### v1.projects.deployments
- `create`, `delete`, `get`, `list`, `update` – Manage deployment instances

### v1.projects.versions
- `create`, `get`, `list` – Handle immutable version snapshots

### v1.scripts
- `run` – POST `/v1/scripts/{scriptId}:run` – Execute functions within projects

## Implementation

The platform recommends "Google-provided client libraries" for calling this service, with options available for JavaScript, Go, Java, .NET, Node.js, PHP, Python, and Ruby.

## See also (in this reference set)

- [processes.md](processes.md)
- [projects.md](projects.md)
- [projects-deployments.md](projects-deployments.md)
- [projects-versions.md](projects-versions.md)
- [scripts-run.md](scripts-run.md)
- [execution-error.md](execution-error.md)
- [execution-response.md](execution-response.md)
- [file.md](file.md)
</content>
