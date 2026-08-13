# Apps Script Guides — Index

Conceptual guides, how-tos, and platform-specific documentation for Google Apps Script (everything that isn't class/method reference — see [`../reference/`](../reference/README.md) for that).

## Getting started & core concepts

- [Overview](Overvieww.md) — what Apps Script is
- [Apps Script Dashboard](AppsScriptDashboard.md)
- [Script Projects](Scriptprojects.md)
- [Standalone Scripts](standalone.md)
- [Bound to Google Workspace Documents](Boundtogoogleworkspacedocuments.md)
- [Manifests (concept)](Manifests.md) · full field reference in [manifest/](#manifest-reference)
- [JSDoc](JSDoc.md)
- [Versions](Versions.md)
- [Deployments](Deployments.md)
- [Libraries](Libraries.md)
- [Collaboration](Colloboration.md)
- [Logging](Logging.md)
- [Troubleshooting](Troubleshoot.md)
- [Quotas and Limits](quotas-and-limits.md)

## Triggers

- [Simple Triggers](triggers/simple-triggers.md)
- [Installable Triggers](triggers/installable-triggers.md)
- [Event Objects](triggers/event-objects.md)

## Services, authorization & scopes

- [Built-in Google Services](BuiltinGoogleservices.md)
- [Advanced Google Services](Advanced%20Googleservices.md) — see also [`../advanced-services/`](../advanced-services/README.md)
- [Authorization](Authorization.md)
- [Scopes](Scopes.md)
- [Authenticate Using Service Accounts](Authenticate%20using%20service%20accounts.md)
- [OAuth Client Verification](Oauth%20client%20verification.md)
- [Connect to Google Cloud Services](ConnectToGoogleCloudServices.md)
- [Google Cloud Projects](GoogleCloud%20projects.md)
- [External APIs](ExternalAPI.md)
- [Admin Management](Adminmanagement.md) — assign GCP permissions, monitor/restrict OAuth scopes, monitor use, view cloud projects

## User interfaces

- [Custom Menus](Menus_dialogs_sidebars.md)
- [User Interfaces / Dialogs & Sidebars](UserInterfaces.md)
- [Create and Serve HTML / Store & Serve Data](storeandservedata.md)
- [Content Service](content-service.md)
- [Gemini Side Panel](gemini-side-panel.md)

### HTML Service subtree

- [Web Apps](html/web-apps.md)
- [Client-to-Server Communication](html/client-server-communication.md)
- [Templated HTML](html/templated-html.md)
- [Restrictions](html/restrictions.md)
- [Best Practices](html/best-practices.md)
- [Migrate to IFRAME Sandbox Mode](html/migrate-to-iframe.md)
- [google.script.run](html/reference-google-script-run.md)
- [google.script.host](html/reference-google-script-host.md)
- [google.script.history](html/reference-google-script-history.md)
- [google.script.url](html/reference-google-script-url.md)

## Runtime & migration

- [V8 Runtime Overview](v8runtimeoverview.md)
- [Migrate to the V8 Runtime](migrate%20to%20the%20v8runtime.md)
- [Bulk Migrate Identical Scripts](BulkMigrateIdenticalScripts.md)

## Command line & REST API

- [Command Line Interface (clasp)](commandlineinterface.md)
- [Use the REST API](UseTheRestAPI.md) — see also full class reference in [`../reference/apps-script-api/`](../reference/apps-script-api/README.md)

### Apps Script API how-tos

- [Concepts](api/concepts.md)
- [Processes Concept](api/processes-concept.md)
- [Enable Script Authorization and Access](api/enable-script-authorization-and-access.md)
- [Manage Script Projects](api/manage-script-projects.md)
- [Manage Script Deployments](api/manage-script-deployments.md)
- [Manage Script Versions](api/manage-script-versions.md)
- [View Process Information](api/view-process-information.md)
- [Execute a Function](api/execute-a-function.md)
- [Troubleshoot Authentication/Authorization](api/troubleshoot-auth.md)

## Manifest reference

- [Overview](manifest/overview.md)
- [Libraries & Advanced Services](manifest/libraries-and-advanced-services.md)
- [Web Apps and API Executables](manifest/web-apps-and-api-executables.md)
- [Sheets Macros](manifest/sheets-macros.md)
- [Allowlist URLs](manifest/allowlist-urls.md)
- [AddOns Resource](manifest/addons-resource.md)
- [Calendar Resource](manifest/calendar-resource.md)
- [Drive Resource](manifest/drive-resource.md)
- [Gmail Resource](manifest/gmail-resource.md)
- [Editors Resource](manifest/editors-resource.md)
- [Meet Resource](manifest/meet-resource.md)
- [HomepageTrigger Resource](manifest/homepage-trigger-resource.md)

## Google Workspace app-specific guides

### Docs
- [Overview](docs/overview.md)
- [Working with Tabs](docs/working-with-tabs.md)

### Sheets
- [Google Sheets Overview](extendgoogleworkspace_GoogleSheets_Overview.md)
- [Custom Functions](sheets/custom-functions.md)
- [Macros](sheets/macros.md)
- [Connected Sheets](sheets/connected-sheets.md)

### Slides
- [Overview](slides/overview.md)
- [Structure of a Presentation](slides/structure-of-a-presentation.md)
- [Size and Position Page Elements](slides/size-and-position-page-elements.md)
- [Select Items](slides/select-items.md)
- [Edit and Style Text](slides/edit-and-style-text.md)
- [Lifecycle of an Update](slides/lifecycle-of-an-update.md)

## VBA Macro Converter

- [Overview / Convert Files](ConvertVBAMAcrostoAppsscript.md)
- [Determine VBA Compatibility](macro-converter/determine-vba-compatibility.md)
- [Fix Conversion Errors](macro-converter/fix-conversion-errors.md)
- [Address Common Issues](macro-converter/address-common-issues.md)
- [Compatible VBA APIs](macro-converter/compatible-vba-apis.md)

## Migration guides

- [Groups Service → Cloud Identity Groups API](migration/groups-to-cloud-identity-groups-api.md)
- [Contacts Service → People API](migration/contacts-to-people-api.md)

## Quickstarts

- [Automation](quickstart/automation.md)
- [Custom Functions](quickstart/custom-functions.md)
- [Chat Bot](quickstart/chat-bot.md)

## Support & meta

- [Service Status Dashboard](support/service-status-dashboard.md)
- [Sunset Schedule](support/sunset-schedule.md)
- [Glossary](support/glossary.md)
- [Release Notes](support/release-notes.md)

---

For Workspace Add-ons (Gmail/Calendar/Drive/Editor/Chat/Meet add-on development, a separate but related doc tree), see [`../workspace-add-ons/`](../workspace-add-ons/README.md).
