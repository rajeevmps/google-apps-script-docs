# File

Source: https://developers.google.com/apps-script/api/reference/rest/v1/File

## Overview

The File resource represents an individual file within an Apps Script project. According to the documentation, "A file is a third-party source code created by one or more developers. It can be a server-side JS code, HTML, or a configuration file."

## File Properties

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | The filename without extension |
| `type` | FileType enum | Categorizes the file format |
| `source` | string | The file content |
| `lastModifyUser` | User object | Profile of the most recent editor |
| `createTime` | Timestamp | Creation date in RFC3339 format |
| `updateTime` | Timestamp | Last modification date in RFC3339 format |
| `functionSet` | FunctionSet object | Collection of defined functions |

## File Types (FileType enum)

- `SERVER_JS` — Server-side Apps Script code
- `HTML` — Client-side HTML content
- `JSON` — Project manifest configuration file

## FunctionSet Structure

A FunctionSet contains a `values` array of Function objects, with no duplicates permitted.

## Function Structure

Each Function object contains:

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | The function identifier |
| `parameters` | string array | Ordered parameter names |
</content>
