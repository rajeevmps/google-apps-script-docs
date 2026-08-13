# Google Apps Script Documentation — Local Offline Copy

A structured, local markdown mirror of the official Google Apps Script documentation (`developers.google.com/apps-script/`) and the related Workspace Add-ons docs (`developers.google.com/workspace/add-ons/`), built for use as coding context in future projects. Content was fetched and converted section by section, so fidelity is generally high, but this is a point-in-time snapshot (fetched August 2026) — for anything version-sensitive or rapidly changing (release notes, quotas, sunset schedules), cross-check the live docs.

## Folders

| Folder | What's in it |
|---|---|
| [`guides/`](guides/README.md) | Conceptual guides: getting started, triggers, authorization/scopes, services, UI, HTML Service, manifest reference, runtime/migration, REST API how-tos, VBA macro converter, quickstarts, support/meta pages |
| [`reference/`](reference/README.md) | Full class/method/enum-level API reference for every built-in service (Spreadsheet, Document, Drive, Gmail, Calendar, Forms, Slides, Card Service, Base, Script, Properties, Cache, Lock, Utilities, HTML/Content/XML Service, Charts, JDBC, Maps, and more), plus the Apps Script REST API |
| [`advanced-services/`](advanced-services/README.md) | How to enable and use "Advanced Google Services" (BigQuery, Admin SDK, YouTube, Analytics, etc.) — thin wrappers around external Google Cloud/Workspace REST APIs, not duplicated here in full |
| [`workspace-add-ons/`](workspace-add-ons/README.md) | Building installable Workspace Add-ons: Gmail, Calendar, Drive, Editor (Docs/Sheets/Slides/Forms), Chat apps, and Meet add-ons, plus publishing |

## Quick orientation

- **Writing a container-bound script for Sheets/Docs/Forms/Slides?** Start with [`guides/README.md`](guides/README.md) (Getting Started, Bound to Google Workspace Documents) and the relevant service in [`reference/`](reference/README.md) (e.g. [`reference/spreadsheet/`](reference/spreadsheet/README.md)).
- **Writing a standalone script or web app?** See [`guides/standalone.md`](guides/standalone.md), [`guides/html/web-apps.md`](guides/html/web-apps.md), and [`reference/html/`](reference/html/README.md) / [`reference/content/`](reference/content/README.md).
- **Building a custom function?** [`guides/sheets/custom-functions.md`](guides/sheets/custom-functions.md) and [`guides/quickstart/custom-functions.md`](guides/quickstart/custom-functions.md).
- **Building a Workspace Add-on (installable, cross-app)?** Start at [`workspace-add-ons/README.md`](workspace-add-ons/README.md); the card UI itself is documented in [`reference/card-service/`](reference/card-service/README.md).
- **Calling Apps Script projects remotely / CI-CD?** [`guides/UseTheRestAPI.md`](guides/UseTheRestAPI.md), [`guides/commandlineinterface.md`](guides/commandlineinterface.md) (clasp), and [`reference/apps-script-api/`](reference/apps-script-api/README.md).
- **Need an API not built into Apps Script (BigQuery, Admin SDK, YouTube, ...)?** [`advanced-services/README.md`](advanced-services/README.md).
- **Triggers, quotas, scopes, manifest fields?** [`guides/triggers/`](guides/triggers/simple-triggers.md), [`guides/quotas-and-limits.md`](guides/quotas-and-limits.md), [`guides/Scopes.md`](guides/Scopes.md), [`guides/manifest/`](guides/manifest/overview.md).

## Known gaps

- The **Sites** service was removed from the current Apps Script reference (its page now redirects to the reference overview) — not covered.
- Two Advanced Google Service enablement pages (`admin-reports`, `cloud-identity-groups`) returned real 404s on the live site at fetch time.
- `advanced-services/` and the linked-out REST APIs for each Advanced Google Service are documented at the "how to enable" level only, not scraped in full — those are generic Google Cloud/Workspace API references maintained elsewhere.
- Release notes in [`guides/support/release-notes.md`](guides/support/release-notes.md) capture entries back to October 2018; older history was not captured.
