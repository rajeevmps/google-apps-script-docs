# REST Resource: projects.versions

Source: https://developers.google.com/apps-script/api/reference/rest/v1/projects.versions

## Resource Description

A Version represents a snapshot of a script project, functioning as a read-only branched release. Versions are required when creating deployments.

## JSON Representation

```json
{
  "scriptId": string,
  "versionNumber": integer,
  "description": string,
  "createTime": string
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `scriptId` | string | The script project's Drive ID. |
| `versionNumber` | integer | System-assigned incremental ID created when a version is created; immutable once established. |
| `description` | string | Description for this version. |
| `createTime` | string (Timestamp format) | When the version was created in RFC3339 UTC "Zulu" format with nanosecond resolution and up to nine fractional digits (e.g., "2014-10-02T15:01:23Z"). |

## Methods

### create
Creates a new immutable version using the current code, with a unique version number.

### get
Retrieves a specific version of a script project.

### list
Lists all versions of a script project.
</content>
