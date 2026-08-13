# Web apps and API executables manifest resource

## Overview

This documentation describes the resource configurations for web apps and API executables in Google Apps Script projects.

## Webapp

The web app configuration applies when a project is deployed as a web app.

**JSON representation:**
```json
{
  "access": string,
  "executeAs": string
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `access` | string | Web app execution permission levels: `MYSELF` (deploying user only), `DOMAIN` (same domain users), `ANYONE` (logged-in users), `ANYONE_ANONYMOUS` (all users) |
| `executeAs` | string | Execution identity: `USER_ACCESSING` (runs as accessing user) or `USER_DEPLOYING` (runs as deploying user) |

## ExecutionApi

The API executable configuration applies when a project is deployed for API execution.

**JSON representation:**
```json
{
  "access": string
}
```

**Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `access` | string | API execution permissions: `MYSELF`, `DOMAIN`, `ANYONE`, or `ANYONE_ANONYMOUS` |

Both configurations use the `access` field to control "who has permission to run the script," while only the web app includes an additional `executeAs` field determining execution identity.

Source: https://developers.google.com/apps-script/manifest/web-app-api-executable
