# REST Resource: projects

Source: https://developers.google.com/apps-script/api/reference/rest/v1/projects

## Resource Description

The Project resource represents a script project in Google Apps Script. It encapsulates metadata about a script project including its unique identifier, title, creation and modification timestamps, and user information for the creator and last modifier.

## Project Resource

### JSON Representation

```json
{
  "scriptId": string,
  "title": string,
  "parentId": string,
  "createTime": string,
  "updateTime": string,
  "creator": {
    object (User)
  },
  "lastModifyUser": {
    object (User)
  }
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `scriptId` | string | The script project's Drive ID |
| `title` | string | The title for the project |
| `parentId` | string | The parent's Drive ID that the script will be attached to (usually a Google Document or Sheet ID); optional for stand-alone scripts |
| `createTime` | string (Timestamp) | When the script was created in RFC3339 UTC format |
| `updateTime` | string (Timestamp) | When the script was last updated in RFC3339 UTC format |
| `creator` | object (User) | User who originally created the script |
| `lastModifyUser` | object (User) | User who last modified the script |

## User Resource

### JSON Representation

```json
{
  "domain": string,
  "email": string,
  "name": string,
  "photoUrl": string
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `domain` | string | The user's domain |
| `email` | string | The user's identifying email address |
| `name` | string | The user's display name |
| `photoUrl` | string | The user's photo |

## Methods

### create
POST `/v1/projects` — Creates a new, empty script project with no script files and a base manifest file.

### get
GET `/v1/projects/{scriptId}` — Gets a script project's metadata.

### getContent
GET `/v1/projects/{scriptId}/content` — Gets the content of the script project, including the code source and metadata for each script file.

### getMetrics
GET `/v1/projects/{scriptId}/metrics` — Retrieves metrics data for scripts, such as number of executions and active users.

### updateContent
PUT `/v1/projects/{scriptId}/content` — Updates the content of the specified script project.
</content>
