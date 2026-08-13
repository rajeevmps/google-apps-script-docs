# Manifest structure

## Page Summary

- An Apps Script project's manifest file defines its function or purpose.
- The manifest uses a JSON data structure with various fields for configuration.
- Fields in the manifest can configure the project as a Google Workspace add-on, Google Chat app, or web app.
- The manifest includes configurations for dependencies, exception logging, authorization scopes, runtime version, and time zone.
- A URL allowlist can be used in the manifest to restrict fetched URL endpoints.

## Overview

This page describes the top-level of the Google Apps Script manifest file JSON data structure. The manifest defines the Apps Script project function or purpose.

## JSON Representation

```json
{
  "addOns": {
    object (AddOns)
  },
  "chat": {},
  "dependencies": {
    object (Dependencies)
  },
  "exceptionLogging": string,
  "executionApi": {
    object (ExecutionApi)
  },
  "oauthScopes": [
    string
  ],
  "runtimeVersion": string,
  "sheets": {
    object (Sheets)
  },
  "timeZone": string,
  "urlFetchWhitelist": [
    string
  ],
  "webapp": {
    object (Webapp)
  }
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `addOns` | object (AddOns) | The project resource configuration if deployed as a Google Workspace add-on. |
| `chat` | object | The project configuration if deployed as a Google Chat app. For new Chat apps, use the `addOns.chat` field instead. If you maintain an existing Chat app that uses the `chat` field, it should be an empty object. To configure Chat app details, you must enable the Google Chat API. Apps Script handles authorization at the script level. A Chat app that requires authorization cannot perform actions until the user authorizes it. To post a message before authorization, add an `addToSpaceFallbackMessage` object to the manifest. |
| `dependencies` | object (Dependencies) | The configuration of advanced services and libraries enabled for use by the script project. |
| `exceptionLogging` | string | The location where exceptions are logged. Valid settings: `NONE` (exceptions not logged) or `STACKDRIVER` (logged in Stackdriver). |
| `executionApi` | object (ExecutionApi) | The script project API executable configuration. Only used if deployed for API execution. |
| `oauthScopes[]` | string | The definition of authorization scopes used by the script project. |
| `runtimeVersion` | string | The runtime version the script is using. Valid options: `STABLE` (default, Rhino), `V8`, or `DEPRECATED_ES5` (Rhino). |
| `sheets` | object (Sheets) | The resource configuration defining Sheets macros. |
| `timeZone` | string | The script time zone in a ZoneId value such as "America/Denver". |
| `urlFetchWhitelist[]` | string | A list of HTTPS URL prefixes. If present, any URL endpoint fetched must match a prefix in this list. Optional for test deployments but required for deployments. |
| `webapp` | object (Webapp) | The script project web app configuration, used if deployed as a web app. |

Source: https://developers.google.com/apps-script/manifest
