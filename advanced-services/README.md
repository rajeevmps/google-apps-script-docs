# Advanced Google Services (Apps Script)

Source: https://developers.google.com/apps-script/guides/services/advanced

## What are Advanced Google Services?

Advanced Google services are thin wrappers around certain public Google APIs, exposed inside the Apps Script editor. They work much like Apps Script's built-in services (e.g. `SpreadsheetApp`, `GmailApp`) — offering autocomplete in the editor and handling OAuth authorization automatically — but unlike built-in services, **they are not enabled by default** and must be explicitly turned on before use.

**Enabling an advanced service is a two-step process:**

1. **Activate the service in the Apps Script project** — either via the editor's Services menu, or by editing the project manifest (`appsscript.json`) to add an entry under `enabledAdvancedServices`.
2. **Enable the corresponding API in the Google Cloud console** — required only for projects using a *standard* Google Cloud project. Apps Script projects using the default, auto-created Cloud project have this handled automatically.

**How advanced services differ from built-in services:**

| | Built-in services | Advanced services |
|---|---|---|
| Enablement | Available by default | Must be explicitly enabled |
| Coverage | Apps Script-specific, simplified API surface | Mirrors the full public REST API (same objects/methods/parameters) |
| Editor support | Autocomplete | Autocomplete (once enabled) |
| Authorization | Automatic | Automatic (mostly — some services like Chat require manually adding OAuth scopes to the manifest) |
| Typical use case | Common, everyday tasks | Access to API surface area not exposed by the built-in service (e.g. Drive file revisions, Calendar event color, Sheets pivot tables, batch operations) |

Each advanced service page under `https://developers.google.com/apps-script/advanced/<slug>` documents how to enable and call a specific advanced service from Apps Script, and links out to that API's full public REST reference (not mirrored here — see the "External reference" links in each file).

## Index of fetched services

| File | Service | One-line description |
|---|---|---|
| [admin-sdk-directory.md](admin-sdk-directory.md) | Admin SDK Directory | Manage Workspace domain users, groups, and devices programmatically. |
| [admin-sdk-license-manager.md](admin-sdk-license-manager.md) | Admin SDK License Manager | Assign, update, retrieve, and delete Workspace user licenses. |
| [admin-sdk-groups-migration.md](admin-sdk-groups-migration.md) | Admin SDK Groups Migration | Migrate emails from public folders/distribution lists into Google Groups archives. |
| [admin-sdk-groups-settings.md](admin-sdk-groups-settings.md) | Admin SDK Groups Settings | Read and update settings for Workspace Groups. |
| [admin-sdk-reseller.md](admin-sdk-reseller.md) | Admin SDK Reseller | Place customer orders and manage Workspace post-pay subscriptions (reseller admins). |
| [calendar.md](calendar.md) | Calendar (Advanced) | Full Calendar API v3 access, including event background color and conditional (ETag) requests. |
| [chat.md](chat.md) | Chat (Advanced) | Manage Google Chat spaces, memberships, and messages; requires manual OAuth scopes and a Chat app config. |
| [docs.md](docs.md) | Docs (Advanced) | Read/edit/format Google Docs via the Docs API, incl. batchUpdate for text and style changes. |
| [drive.md](drive.md) | Drive (Advanced) | Drive API v3 access: custom file properties, revisions, permissions, folder management. |
| [drive-activity.md](drive-activity.md) | Drive Activity | Query the activity history (who did what) on Drive files/folders. |
| [drive-labels.md](drive-labels.md) | Drive Labels | Create, read, and apply/remove Drive Labels on files and folders. |
| [gmail.md](gmail.md) | Gmail (Advanced) | Gmail API v1 access to threads, messages, and labels beyond the built-in GmailApp. |
| [sheets.md](sheets.md) | Sheets (Advanced) | Sheets API v4: range read/write, batchUpdate, new sheets, pivot tables. |
| [slides.md](slides.md) | Slides (Advanced) | Slides API: create presentations/slides, add/format text boxes, batchUpdate. |
| [classroom.md](classroom.md) | Classroom | Manage Google Classroom courses and rosters. |
| [people.md](people.md) | People | Read/write the logged-in user's contacts and read Google user profile data. |
| [tasks.md](tasks.md) | Tasks | Manage Google Tasks task lists and tasks (as used in Gmail). |
| [analyticsdata.md](analyticsdata.md) | Analytics Data (GA4) | Query Google Analytics 4 report data via the Analytics Data API v1. Note: the `analytics` slug now redirects/canonicalizes to this same page — the legacy Universal Analytics "Analytics" advanced service page no longer exists separately. |
| [vertex-ai.md](vertex-ai.md) | Vertex AI | Call Gemini/generative models via the Vertex AI (Agent Platform) API; requires a billed Cloud project. |
| [youtube.md](youtube.md) | YouTube | YouTube Data API v3 and Live Streaming API: search, manage videos/playlists/channels, subscriptions. |
| [youtube-analytics.md](youtube-analytics.md) | YouTube Analytics | Retrieve viewing stats, popularity metrics, and demographics for videos/channels. |
| [youtubecontentid.md](youtubecontentid.md) | YouTube Content ID | Manage assets, claims, and campaigns for YouTube content partners (rights management). Live page is actually at slug `youtube-content-id`. |
| [adsense.md](adsense.md) | AdSense | Access AdSense account/report data. |
| [dv360.md](dv360.md) | Display & Video 360 | Manage DV360 programmatic advertising campaigns. |
| [dbm.md](dbm.md) | DoubleClick Bid Manager | Query and manage Bid Manager reports/campaigns. Live page is actually at slug `doubleclick-bidmanager`. |
| [dfareporting.md](dfareporting.md) | DCM/DFA Reporting & Trafficking | Reporting and trafficking for Campaign Manager (DCM/DFA). Live page is actually at slug `doubleclick-campaigns`. |
| [content.md](content.md) | Content API for Shopping | Manage Merchant Center product data and orders. Live page is actually at slug `shopping-content`. |
| [tag-manager.md](tag-manager.md) | Tag Manager | Manage Google Tag Manager containers, tags, triggers, and variables. |
| [bigquery.md](bigquery.md) | BigQuery | Run queries and manage datasets/tables/jobs in BigQuery. |

29 of 32 requested slugs were fetched successfully (one page, `analyticsdata`, covers both the `analytics` and `analyticsdata` slugs since the former now redirects to the latter).

## Not found (404)

- `admin-sdk-reports` was requested as **admin-reports** — this slug returned HTTP 404. No working alternate slug was found for the Admin SDK Reports service under `/apps-script/advanced/`.
- `cloud-identity-groups` — returned HTTP 404. Alternate slugs `cloudidentity` and `cloud-identity` were also tried and 404'd. No Cloud Identity Groups advanced-service page currently exists at `developers.google.com/apps-script/advanced/`.

## Slugs that resolved under a different name than requested

Google has renamed some advanced-service URL slugs since these were last indexed. The content was still recovered and saved under the originally-requested filename in this directory:

| Requested slug | Actual live slug |
|---|---|
| `youtubecontentid` | `youtube-content-id` |
| `dbm` | `doubleclick-bidmanager` |
| `dfareporting` | `doubleclick-campaigns` |
| `content` | `shopping-content` |
</content>
