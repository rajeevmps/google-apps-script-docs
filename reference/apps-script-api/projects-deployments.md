# REST Resource: projects.deployments

Source: https://developers.google.com/apps-script/api/reference/rest/v1/projects.deployments

## Resource Overview

The `projects.deployments` resource manages single script deployments, including deployment ID, configuration, update time, and entry points.

## Resource: Deployment

Representation of a single script deployment.

| Field | Type | Description |
|-------|------|-------------|
| `deploymentId` | string | The deployment ID for this deployment |
| `deploymentConfig` | DeploymentConfig object | The deployment configuration |
| `updateTime` | string (Timestamp) | Last modified date time stamp in RFC3339 UTC format |
| `entryPoints[]` | EntryPoint object array | The deployment's entry points |

## DeploymentConfig

Metadata defining deployment configuration.

| Field | Type | Description |
|-------|------|-------------|
| `scriptId` | string | The script project's Drive ID |
| `versionNumber` | integer | The version number on which this deployment is based |
| `manifestFileName` | string | The manifest file name for this deployment |
| `description` | string | The description for this deployment |

## EntryPoint

Configuration defining how a deployment is accessed externally.

| Field | Type | Description |
|-------|------|-------------|
| `entryPointType` | EntryPointType enum | The type of the entry point |
| `webApp` | WebAppEntryPoint object | Entry point specification for web apps (union field) |
| `executionApi` | ExecutionApiEntryPoint object | Entry point specification for Apps Script API execution (union field) |
| `addOn` | AddOnEntryPoint object | Add-on properties (union field) |

## EntryPointType Enum

- `ENTRY_POINT_TYPE_UNSPECIFIED` - An unspecified entry point
- `WEB_APP` - A web application entry point
- `EXECUTION_API` - An API executable entry point
- `ADD_ON` - An Add-On entry point

## WebAppEntryPoint

A web application entry point.

| Field | Type | Description |
|-------|------|-------------|
| `url` | string | The URL for the web application |
| `entryPointConfig` | WebAppConfig object | The entry point's configuration |

## WebAppConfig

Web app entry point configuration.

| Field | Type | Description |
|-------|------|-------------|
| `access` | Access enum | Who has permission to run the web app |
| `executeAs` | ExecuteAs enum | Who to execute the web app as |

## Access Enum

- `UNKNOWN_ACCESS` - Default value, should not be used
- `MYSELF` - Only the deploying user can access
- `DOMAIN` - Only users in the same domain can access
- `ANYONE` - Any logged-in user can access
- `ANYONE_ANONYMOUS` - Any user, logged in or not, can access

## ExecuteAs Enum

- `UNKNOWN_EXECUTE_AS` - Default value, should not be used
- `USER_ACCESSING` - The script runs as the accessing user
- `USER_DEPLOYING` - The script runs as the deploying user

## ExecutionApiEntryPoint

An API executable entry point.

| Field | Type | Description |
|-------|------|-------------|
| `entryPointConfig` | ExecutionApiConfig object | The entry point's configuration |

## ExecutionApiConfig

API executable entry point configuration.

| Field | Type | Description |
|-------|------|-------------|
| `access` | Access enum | Who has permission to run the API executable |

## AddOnEntryPoint

An add-on entry point.

| Field | Type | Description |
|-------|------|-------------|
| `addOnType` | AddOnType enum | The add-on's required list of supported container types |
| `title` | string | The add-on's required title |
| `description` | string | The add-on's optional description |
| `helpUrl` | string | The add-on's optional help URL |
| `reportIssueUrl` | string | The add-on's optional report issue URL |
| `postInstallTipUrl` | string | The add-on's required post install tip URL |

## AddOnType Enum

- `UNKNOWN_ADDON_TYPE` - Default value, unknown add-on type
- `GMAIL` - Add-on type for Gmail
- `DATA_STUDIO` - Add-on type for Data Studio

## Methods

| Method | Description |
|--------|-------------|
| `create` | Creates a deployment of an Apps Script project |
| `delete` | Deletes a deployment of an Apps Script project |
| `get` | Gets a deployment of an Apps Script project |
| `list` | Lists the deployments of an Apps Script project |
| `update` | Updates a deployment of an Apps Script project |
</content>
