# Google Apps Script release notes

## Page Summary

- Several Apps Script services have been updated, including the Spreadsheet, Forms, Calendar, Docs, Chat, and Google Workspace Add-ons services, adding new features and capabilities.
- The Google Analytics Advanced Service and the Rhino runtime are scheduled for deprecation, requiring migration to the Google Analytics Data API Advanced Service and the V8 runtime respectively.
- The Apps Script IDE has received significant enhancements, such as improved version management, better debugging tools, and a redesigned interface.
- Several services and advanced services have been deprecated or removed, including the Contacts service, classic Google Sites service, Fusion Tables advanced service, and the UI service.
- New services and advanced services have been introduced, such as advanced services for Google Tables, Google Drive API version 3, the Chat API, and Google Workspace Events.

To get the latest product updates delivered to you, add the URL of this page to your [feed reader](https://wikipedia.org/wiki/Comparison_of_feed_aggregators), or add the feed URL directly: `https://developers.google.com/feeds/apps-script-release-notes.xml`.

This page contains release notes for features and updates to Apps Script. We recommend that Apps Script developers periodically check this list for any new announcements.

## August 03, 2026

**Feature**

**Gemini Beta**: You can now use the Gemini side panel in the Apps Script editor to generate, modify, and debug code, and ask questions. Gemini uses context from your active script project and attached container (if available) to provide relevant Apps Script code and explanation.

**Gemini Beta program:** This feature is available only to customers enrolled in the [Gemini Beta program](https://knowledge.workspace.google.com/admin/generative-ai/workspace-with-gemini/turn-access-to-google-workspace-with-gemini-beta-on-or-off).

To learn more, see [Use the Gemini side panel in the Apps Script editor](https://developers.google.com/apps-script/guides/gemini).

## June 22, 2026

**Announcement**

**Generally Available:** Apps Script is generally available as a core service in Google Workspace, giving it the enterprise-grade data protection, robust administrative controls, and standard technical support that safeguard other core services.

## March 12, 2026

**Feature**

**Generally Available:** The [`AddOnsResponseService`](https://developers.google.com/apps-script/reference/add-ons-response-service) and its associated classes in Apps Script are now generally available. This service allows developers to create and manage interactive responses for Google Workspace Add-ons that extend Google Chat.

## March 05, 2026

**Deprecated**

**Deprecated:** The method [`setAuthentication(clientId, signingKey)`](https://developers.google.com/apps-script/reference/maps/maps#setAuthentication(String,String)) has been deprecated and is scheduled for sunset in June 2026. This change is because Maps platform [client IDs were deprecated](https://developers.google.com/maps/premium/migrate-client-id#overview) on May 26, 2025, and can't be used after May 31, 2026. Instead, use [`setAuthenticationByKey(apiKey)`](https://developers.google.com/apps-script/reference/maps/maps#setauthenticationbyapikeyapikey) or [`setAuthenticationByKey(apiKey, signingKey)`](https://developers.google.com/apps-script/reference/maps/maps#setauthenticationbyapikeyapikey,-signingkey). To get an API key, refer to the [Client ID Migration Guide](https://developers.google.com/maps/premium/migrate-client-id).

**Feature**

**Generally Available:** To authenticate to the Maps service, you can now use an API key with the new methods [`setAuthenticationByKey(apiKey)`](https://developers.google.com/apps-script/reference/maps/maps#setauthenticationbyapikeyapikey) and [`setAuthenticationByKey(apiKey, signingKey)`](https://developers.google.com/apps-script/reference/maps/maps#setauthenticationbyapikeyapikey,-signingkey). To reset authentication to the default mode, use [`resetAuthenticationApiKey()`](https://developers.google.com/apps-script/reference/maps/maps#resetauthenticationapikey).

## January 12, 2026

**Feature**

**Generally Available:** Use Apps Script's Vertex AI advanced service to call the Vertex AI API and prompt AI models to generate text, images, and more.

For details, see the [Vertex AI advanced service](https://developers.google.com/apps-script/advanced/vertex-ai) reference documentation.

## January 07, 2026

**Other**

The [Apps Script samples gallery](https://developers.google.com/apps-script/samples) now lets you find samples by use case, products, and sample type. The gallery also features the following new samples:

- [Build a Google Chat app with an ADK AI agent](https://developers.google.com/workspace/add-ons/chat/quickstart-adk-agent)
- [Build a Chat app with an Agent2Agent agent](https://developers.google.com/workspace/add-ons/chat/quickstart-a2a-agent)
- [Analyze and label Gmail messages with Gemini and Vertex AI](https://developers.google.com/workspace/add-ons/samples/gmail-sentiment-analysis-ai)

## June 04, 2025

**Deprecated**

[Google Analytics 4 has replaced Universal Analytics](https://support.google.com/analytics/answer/11583528), which means the Apps Script Advanced Service for Google Analytics Management API and Reporting API is deprecated. Use the [Google Analytics Data API Advanced Service](https://developers.google.com/apps-script/advanced/analyticsdata) instead.

## April 23, 2025

**Fixed**

Between approximately September 2024 and March 2025, for Google Sheets modifications made by time-based Apps Script triggers, a bug caused incorrect OAuth App IDs and App Names to be logged in the Google Admin console.

This logging issue did not impact the functionality of Apps Script or Google Sheets. A fix was deployed on March 27, 2025, preventing future incorrect logging. Historical logs will not be corrected.

To learn more about Apps Script and audit logs, see [Monitor and control Apps Script use in your Google Workspace organization](https://developers.google.com/apps-script/guides/admin/monitor-use).

## April 08, 2025

**Feature**

You can now use the [Forms Service](https://developers.google.com/apps-script/reference/forms) to publish forms, and to have granular control over who can respond to forms.

[Learn about the `setPublished` method to publish forms](https://developers.google.com/apps-script/reference/forms/form#setPublished(Boolean)).

## February 20, 2025

**Announcement**

As of February 20, 2025, the Rhino runtime is deprecated. Scripts running on Rhino will continue to function until January 31, 2026, after which they will no longer execute. Please migrate your scripts to the V8 runtime before this date. Refer to [Migrate scripts to the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime/migration).

## January 08, 2025

**Feature**

**Generally Available**: Granular OAuth permissions are now supported for users executing scripts in the Apps Script IDE. The granular OAuth consent screen lets users specify which individual OAuth scopes they would like to authorize. The granular consent screen will gradually launch to the remaining Apps Script surfaces, such as add-ons and trigger executions, in the future.

For more information, refer to the Workspace Updates blog post: [Granular OAuth consent in Google Apps Script IDE executions](https://workspaceupdates.googleblog.com/2025/01/granular-oauth-consent-in-google-apps-script.html).

**Feature**

**Generally Available**: To complement the release of the granular consent flow in Apps Script IDE executions, the following methods have been added to the `ScriptApp` and `AuthorizationInfo` classes to let Apps Script developers programmatically interact with the scopes granted for a script.

[`ScriptApp` class](https://developers.google.com/apps-script/reference/script/script-app):

- [`requireScopes(authMode, oAuthScopes)`](https://developers.google.com/apps-script/reference/script/script-app#requirescopesauthmode,-oauthscopes)
- [`requireAllScopes(authMode)`](https://developers.google.com/apps-script/reference/script/script-app#requireallscopesauthmode)
- [`getAuthorizationInfo(authMode, oAuthScopes)`](https://developers.google.com/apps-script/reference/script/script-app#getauthorizationinfoauthmode,-oauthscopes)

[`AuthorizationInfo` class](https://developers.google.com/apps-script/reference/script/authorization-info):

- [`getAuthorizedScopes()`](https://developers.google.com/apps-script/reference/script/authorization-info#getauthorizedscopes)

For more information, refer to [Handle granular OAuth permissions](https://developers.google.com/apps-script/concepts/scopes#handle-granular).

## December 09, 2024

**Deprecated**

The `getUrl()` method for the `CellImage`, `CellImageBuilder`, and `OverGridImage` classes of the [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been deprecated. An image's source URL isn't available regardless of how the image is inserted into a spreadsheet.

**Feature**

**Generally available**: The [`getSheetById()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getsheetbyidid) method has been added to the `Spreadsheet` class of the Spreadsheet service. This lets you get a sheet in a spreadsheet using its unique ID.

**Feature**

**Generally available**: You can now get and set the transparency of a calendar event, meaning whether the event shows as "Busy" or "Available" in Google Calendar. For more information, refer to the following documentation:

- [Enum `EventTransparency`](https://developers.google.com/apps-script/reference/calendar/event-transparency)
- [Class `CalendarEvent`](https://developers.google.com/apps-script/reference/calendar/calendar-event)
- [Class `CalendarEventSeries`](https://developers.google.com/apps-script/reference/calendar/calendar-event-series)

## November 27, 2024

**Feature**

The Calendar service now has a `getEventType()` method that lets developers differentiate regular events from other types of events like out-of-office and working location events. For more information, see the following documentation:

- [`getEventType()` for events](https://developers.google.com/apps-script/reference/calendar/calendar-event#getEventType())
- [`getEventType()` for event series](https://developers.google.com/apps-script/reference/calendar/calendar-event-series#getEventType())
- [`EventType` enum](https://developers.google.com/apps-script/reference/calendar/event-type)

## October 02, 2024

**Announcement**

Apps Script has rescheduled the shutdown date of the Contacts service to January 31, 2025. Refer to the [Apps Script sunset schedule](https://developers.google.com/apps-script/guides/support/sunset).

The Apps Script Contacts service was deprecated in December 2022. Instead, use the People API advanced service. Refer to [Migrate from Contacts service to People API advanced service](https://developers.google.com/apps-script/migration/contacts-people).

## September 03, 2024

**Feature**

**Generally available**: You can now use Looker in [Connected Sheets](https://developers.google.com/apps-script/guides/sheets/connected-sheets) from Apps Script. This update lets you create a new or access existing Looker data source connections, connect a sheet to them, create pivot tables, and more.

The following updates have been made to the [`Spreadsheet` service](https://developers.google.com/apps-script/reference/spreadsheet) to support Looker in Connected Sheets from Apps Script.

- The following new data source type has been added:
  - [`LOOKER`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-type)
- The following new classes have been added:
  - [`LookerDataSourceSpec`](https://developers.google.com/apps-script/reference/spreadsheet/looker-data-source-spec)
  - [`LookerDataSourceSpecBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/looker-data-source-spec-builder)
- The following new methods have been added to existing classes:
  - [`DataSourceSpec.asLooker()`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec#aslooker)
  - [`DataSourceSpecBuilder.asLooker()`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec-builder#aslooker)

## August 15, 2024

**Feature**

**Generally Available**: You can now create and organize tabs in Google Docs documents using Apps Script's Document service. For more information, refer to [Work with tabs](https://developers.google.com/apps-script/guides/docs/tabs).

## August 07, 2024

**Change**

Google Workspace administrators can now turn on an allowlist in the admin console to control which external domains users can access through Apps Script's [URL Fetch service](https://developers.google.com/apps-script/reference/url-fetch).

- If you're using a script or add-on that accesses external domains, work with your administrator to add those URLs to the admin allowlist.
- If you've published an add-on on the Google Workspace Marketplace, it might be helpful to list the URLs that admins should add to their allowlist on your Marketplace listing.

For more information, refer to the Google Workspace Admin Help article: [Allow only certain external connections for Apps Script and Sheets](https://knowledge.workspace.google.com/admin/drive/allow-only-certain-external-connections-for-apps-script-and-sheets).

## July 25, 2024

**Feature**

(**Generally Available**): Multiselect menus are now generally available for Add-ons.

For more information refer to the following:

- [`SelectionInput` for Apps Script](https://developers.google.com/apps-script/reference/card-service/selection-input)
- [`SelectionInput` for HTTP runtimes](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectioninput)

**Feature**

(**Generally Available**): Columns are now generally available for Add-ons.

For more information refer to the following:

- [`Columns` for Apps Script](https://developers.google.com/apps-script/reference/card-service/columns)
- [`Columns` for HTTP runtimes](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#columns)

## May 02, 2024

**Feature**

To subscribe to events using Apps Script, you can now use the Advanced Google Workspace Events service. For details, see the [Apps Script reference documentation](https://developers.google.com/apps-script/advanced/events).

## April 30, 2024

**Feature**

The `cancelDataRefresh()` method has been added to the following classes of the Spreadsheet service:

- [`DataSourceChart`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-chart#canceldatarefresh)
- [`DataSourceFormula`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-formula#canceldatarefresh)
- [`DataSourcePivotTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-pivot-table#canceldatarefresh)
- [`DataSourceSheet`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-sheet#canceldatarefresh)
- [`DataSourceTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-table#canceldatarefresh)

The `cancelDataRefresh()` method cancels the data refresh associated with the object it's called on if the refresh is currently running.

The [`cancelAllLinkedDataSourceObjectRefreshes()`](https://developers.google.com/apps-script/reference/spreadsheet/data-source#cancelalllinkeddatasourceobjectrefreshes) method has been added to the `DataSource` class. This method cancels all currently running refreshes of data source objects linked to the data source this method is called on.

## April 22, 2024

**Feature**

**(Generally Available)**: Google Chat apps now support Google Apps Script's Card Service. If you've built your Chat app using Apps Script, you can use Card Service to build user interfaces such as card messages and dialogs. For more information, see the [Card Service reference documentation](https://developers.google.com/apps-script/reference/card-service).

## March 15, 2024

**Change**

The default property for the [`TextButtonStyle` enum](https://developers.google.com/apps-script/reference/card-service/text-button-style) in the Apps Script [Card Service](https://developers.google.com/apps-script/reference/card-service/card-service) has been renamed from `TEXT` to `OUTLINED` to align with the [Google Material 3 design system](https://m3.material.io/components/buttons/guidelines#3742b09f-c224-43e0-a83e-541bd29d0f05). Existing scripts that use the original default, `TEXT`, render the same as the new default, `OUTLINED`.

## March 07, 2024

**Feature**

**(Generally Available)**: You can now delete multiple unused versions at the same time from the Project History page. Refer to [Delete multiple versions](https://developers.google.com/apps-script/guides/versions#bulk-delete).

## March 05, 2024

**Feature**

**(Generally Available)**: The [`LinkPreview`](https://developers.google.com/apps-script/reference/card-service/link-preview) class has been added to the Apps Script Card service. This class lets you control various aspects of link previews, including the smart chip title, the link preview title, and the link preview card.

## February 29, 2024

**Announcement**

The 200 version limit, first announced for new scripts on [December 6, 2023](https://developers.google.com/apps-script/docs/release-notes#December_06_2023), has been extended to all script projects. If your existing script project already has more than 200 versions, after June 1, 2024 you won't be able to add a new version. To delete unused versions, refer to [Delete a version](https://developers.google.com/apps-script/guides/versions#delete-version).

## February 21, 2024

**Feature**

(**Developer Preview**): Multiselect menus are now in Developer Preview for Add-ons.

For more information refer to the following:

- [`SelectionInput` for Apps Script](https://developers.google.com/apps-script/reference/card-service/selection-input)
- [`SelectionInput` for other runtimes](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#selectioninput)

**Feature**

(**Developer Preview**): Columns are now in Developer Preview for Add-ons.

For more information refer to the following:

- [`Columns` for Apps Script](https://developers.google.com/apps-script/reference/card-service/columns)
- [`Columns` for other runtimes](https://developers.google.com/workspace/add-ons/reference/rpc/google.apps.card.v1#columns)

## February 20, 2024

**Feature**

**(Developer Preview)**: Google Chat apps now support Google Apps Script's Card Service. If you've built your Chat app using Apps Script, you can use Card Service to build user interfaces such as card messages and dialogs. For more information, see the [Card Service reference documentation](https://developers.google.com/apps-script/reference/card-service).

## January 24, 2024

**Feature**

(**Generally Available**): Google Workspace Add-ons now support third-party resource creation from the @ menu in Google Docs. This feature is gradually rolling out over the next few weeks. To use this feature, see [Create third-party resources from the @ menu](https://developers.google.com/apps-script/add-ons/editors/gsao/create-insert-resource-smart-chip).

## January 18, 2024

**Feature**

(**Generally available**): Google Workspace Add-ons now support link previews in Google Sheets and Slides. To learn more, see [Preview links with smart chips](https://developers.google.com/apps-script/add-ons/editors/gsao/preview-links).

## December 13, 2023

**Feature**

(**Generally Available**): The [`setPersistValues(persistValues)`](https://developers.google.com/apps-script/reference/card-service/action#setpersistvaluespersistvalues) method has been added to the `Action` class of the [Card service](https://developers.google.com/apps-script/reference/card-service). This means that you can now indicate whether form values are determined by the client's values or the server's values after an action response updates a form's card.

## December 11, 2023

**Feature**

(**Generally Available**): You can now call version 3 of the Google Drive API from Apps Script with the advanced Drive service. To learn more, see [Advanced Drive service](https://developers.google.com/apps-script/advanced/drive).

## December 07, 2023

**Fixed**

To fix a bug that prevented events of `eventType != 'default'` from importing, we updated the code sample in [Populate a team vacation calendar](https://developers.google.com/apps-script/samples/automations/vacation-calendar), the popular Apps Script + Calendar API solution. Review the code change in [GitHub](https://github.com/googleworkspace/apps-script-samples/pull/434/files).

## December 06, 2023

**Feature**

(**Generally available**): You can now delete versions in your Apps Script project from the project history page in the Apps Script IDE.

Script projects created after December 10, 2023 can have up to 200 versions. If your script reaches the versions limit, or you want to clean up your script project, delete undeployed versions that you no longer need.

To learn more, see [Delete a version](https://developers.google.com/apps-script/guides/versions#delete-version).

## November 15, 2023

**Feature**

**([Developer Preview](https://developers.google.com/workspace/preview))**: Google Workspace Add-ons now support third-party resource creation from the @ menu in Google Docs. To use this feature, see [Create third-party resources from the @ menu](https://developers.google.com/apps-script/add-ons/editors/gsao/create-insert-resource-smart-chip).

## November 13, 2023

**Feature**

**(Developer Preview)**: Available as part of the [Google Workspace Developer Preview Program](https://developers.google.com/workspace/preview), which grants early access to certain features.

Google Workspace Add-ons now support link previews in Google Sheets and Slides. To learn more, see [Preview links with smart chips](https://developers.google.com/apps-script/add-ons/editors/gsao/preview-links).

## November 06, 2023

**Feature**

**(Generally available)**: You can now call the Chat API from Apps Script with the Advanced Chat Service. To learn how, see [Advanced Chat Service](https://developers.google.com/apps-script/advanced/chat) in the Apps Script reference documentation.

We've also updated the Apps Script code samples to use the Advanced Chat Service in the following Chat API developer guides:

- [Authenticate as an app](https://developers.google.com/chat/api/guides/auth/service-accounts)
- [Authenticate as a user](https://developers.google.com/chat/api/guides/auth/users)
- [Try it - Respond to Incidents](https://developers.google.com/chat/tutorial-incident-response)

## September 26, 2023

**Change**

The email address that sends notifications about [errors in triggers](https://developers.google.com/apps-script/guides/triggers/installable#errors_in_triggers) has been updated from `apps-scripts-notifications@google.com` to `noreply-apps-scripts-notifications@google.com`.

## September 19, 2023

**Deprecated**

The classic Google Sites service has been deprecated due to the [transition from classic Sites to new Sites](https://support.google.com/a/answer/9958187#zippy=%2Cwhat-are-the-differences-between-classic-sites-and-new-sites%2Cwhat-happens-to-my-classic-site-after-migration). There isn't a way to connect to new Sites with Apps Script.

## August 23, 2023

**Feature**

You can now view previously deployed script versions and compare them to the current script version in the Apps Script IDE. Anyone who has edit permission on an Apps Script project can access the project history page. To learn more, refer to the following:

- **Google Workspace Updates blog**: [View & compare script versions with Apps Script project history](https://workspaceupdates.googleblog.com/2023/08/apps-script-project-history.html)
- **Developer documentation**: [Versions](https://developers.google.com/apps-script/guides/versions)

## June 12, 2023

**Feature**

Third-party smart chips and link previews are now generally available. To build a Google Workspace Add-on that uses this feature, see [Preview links with smart chips](https://developers.google.com/apps-script/add-ons/editors/gsao/preview-links).

## December 16, 2022

**Deprecated**

Apps Script has deprecated the [Contacts service](https://developers.google.com/apps-script/reference/contacts). Instead, use the [People API advanced service](https://developers.google.com/apps-script/advanced/people). Refer to [Migrate from Contacts service to People API advanced service](https://developers.google.com/apps-script/migration/contacts-people).

The Contacts service shutdown has been rescheduled from April 2023 to January 2025. Refer to the [Apps Script sunset schedule](https://developers.google.com/apps-script/guides/support/sunset).

## November 03, 2022

**Feature**

Apps Script added a new method to the [Utilities class](https://developers.google.com/apps-script/reference/utilities/utilities). [`parseDate(date, timeZone, format`)](https://developers.google.com/apps-script/reference/utilities/utilities#parsedatedate,-timezone,-format) parses a provided string date according to the specification described in the [Java Standard Edition SimpleDateFormat class](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html).

## November 01, 2022

**Deprecated**

Apps Script has sunset the following methods:

- [`getChatThreads()`](https://developers.google.com/apps-script/reference/gmail/gmail-app#getChatThreads())
- [`getChatThreads(start, max)`](https://developers.google.com/apps-script/reference/gmail/gmail-app#getChatThreads(Integer,Integer))

There isn't a replacement method to get this data with Apps Script.

[Learn about the switch from Classic Hangouts to Chat](https://support.google.com/chat/answer/9854901).

## September 27, 2022

**Deprecated**

Apps Script has turned down the legacy integrated development environment (IDE) in favor of the redesigned IDE that launched in December 2020.

Learn more about the IDE updates from the following blog posts:

- [Updated Apps Script integrated development environment will replace the legacy experience by Q4 2022](https://workspaceupdates.googleblog.com/2022/09/apps-script-ide-update.html).
- [Additional functionality for the Apps Script Integrated Development Environment (IDE) Script Editor](https://workspaceupdates.googleblog.com/2022/04/apps-script-integrated-development-enviornment-improvements.html).
- [Use the new Apps Script Integrated Development Environment (IDE) Script Editor](https://workspaceupdates.googleblog.com/2020/12/google-apps-script-ide-better-code-editing.html).

## July 19, 2022

**Change**

Apps Script now automatically deletes [default Google Cloud projects](https://developers.google.com/apps-script/guides/cloud-platform-projects#default_google_cloud_projects) (Google Cloud projects that Apps Script creates in the background) when their associated scripts haven't run in 180 days or more. If the script runs after Apps Script deletes the default Google Cloud project, Apps Script creates one for the script.

This update doesn't affect standard Google Cloud projects (Google Cloud projects created by people).

## July 08, 2022

**Deprecated**

Apps Script has deprecated the following methods:

- [`getChatThreads()`](https://developers.google.com/apps-script/reference/gmail/gmail-app#getChatThreads())
- [`getChatThreads(start, max)`](https://developers.google.com/apps-script/reference/gmail/gmail-app#getChatThreads(Integer,Integer))

These methods will become unavailable later this year once Google switches all users from Classic Hangouts to Google Chat. There isn't a replacement method to get this data with Apps Script.

[Learn about the switch from Classic Hangouts to Chat](https://support.google.com/chat/answer/9854901).

## June 06, 2022

**Change**

You can now call functions in separate files before they're parsed. Previously, the V8 runtime required a script file to be parsed before any other file could call the functions it defines.

Now, the order of files in the Apps Script editor doesn't matter. This means that you can call a function in a different file to assign a value to a global variable—the function is always defined before it's called. This behavior reflects that of the legacy Rhino runtime.

## April 13, 2022

**Feature**

You can now perform the following actions in the new Apps Script integrated development environment (IDE):

- [Create test deployments for Editor Add-ons](https://developers.google.com/apps-script/add-ons/how-tos/testing-editor-addons#create_a_test_deployment).
- [Add, edit, and delete script properties from the project settings page](https://developers.google.com/apps-script/guides/properties#manage_script_properties_manually).
- Sort files alphabetically in the editor.
- [Debug Rhino functions without migrating to the V8 runtime](https://developers.google.com/apps-script/guides/support/troubleshooting#use_the_debugger_and_breakpoints). If your code isn't V8 compatible, you might receive errors.
- [Set the time zone for a script project](https://developers.google.com/apps-script/guides/projects#set_the_time_zone_for_a_project).

## March 24, 2022

**Feature**

For Google Workspace Add-ons, an [`Attachment` class](https://developers.google.com/apps-script/reference/card-service/attachment) has been added to the [Card Service](https://developers.google.com/apps-script/reference/card-service/card-service) that lets you add custom attachments to Calendar events. You can also set an event trigger that fires when the user clicks on the add-on attachment provider in the Calendar dropdown menu. For more information, refer to [`EventAttachmentTrigger`](https://developers.google.com/apps-script/manifest/calendar-addons#eventattachmenttrigger).

## March 18, 2022

**Deprecated**

The `get` methods for several color objects in the [Spreadsheet Service](https://developers.google.com/apps-script/reference/spreadsheet) have been deprecated in favor of a new naming convention. The functionality remains the same. For example, the `getFontColor()` method from the Range class has been replaced with `getFontColorObject()`.

The following classes have updated `get` methods for color objects:

- [`Banding`](https://developers.google.com/apps-script/reference/spreadsheet/banding):
  - `getFirstColumnColor()` is now `getFirstColumnColorObject()`.
  - `getFirstRowColor()` is now `getFirstRowColorObject()`.
  - `getFooterColumnColor()` is now `getFooterColumnColor()`.
  - `getFooterRowColor()` is now `getFooterRowColorObject()`.
  - `getHeaderColumnColor()` is now `getHeaderColumnColorObject()`.
  - `getHeaderRowColor()` is now `getHeaderRowColorObject()`.
  - `getSecondColumnColor()` is now `getSecondColumnColorObject()`.
  - `getSecondRowColor()` is now `getSecondRowColorObject()`.
- [`BooleanCondition`](https://developers.google.com/apps-script/reference/spreadsheet/boolean-condition):
  - `getBackground()` is now `getBackgroundObject()`.
  - `getFontColor()` is now `getFontColorObject()`.
- [`GradientCondition`](https://developers.google.com/apps-script/reference/spreadsheet/gradient-condition):
  - `getMaxColor()` is now `getMaxColorObject`.
  - `getMidColor()` is now `getMidColorObject`.
  - `getMinColor()` is now `getMinColorObject`.
- [`Range`](https://developers.google.com/apps-script/reference/spreadsheet/range):
  - `getFontColor()` is now `getFontColorObject()`.
  - `getFontColors()` is now `getFontColorObjects()`.
- [`Sheet`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#methods):
  - `getTabColor()` is now `getTabColorObject`.
- [`Slicer`](https://developers.google.com/apps-script/reference/spreadsheet/slicer):
  - `getBackgroundColor()` is now `getBackgroundColorObject()`.

## February 14, 2022

**Feature**

Owners receive email alerts when someone outside the owner's organization edits a script project in the new integrated development environment (IDE).

- **For container-bound scripts**: If someone outside the container owner's organization creates or edits a container-bound script project, the container owner receives an email notification.
- **For standalone scripts**: If someone outside the script project owner's organization edits a standalone script project, the script project owner receives an email notification.

## January 19, 2022

**Feature**

The following classes have been added to the [Spreadsheet Service](https://developers.google.com/apps-script/reference/spreadsheet) to let you add images to cells:

- [`CellImageBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/cell-image-builder): This builder creates the image value needed to add an image to a cell.
- [`CellImage`](https://developers.google.com/apps-script/reference/spreadsheet/cell-image): Represents an image to add to a cell.

To add an image to a cell, you must create a new image value for the image using [`SpreadsheetApp.newCellImage()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newCellImage()) and [`CellImageBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/cell-image-builder). Then, use [`Range.setValue(value)`](https://developers.google.com/apps-script/reference/spreadsheet/range#setValue(Object)) or [`Range.setValues(values)`](https://developers.google.com/apps-script/reference/spreadsheet/range#setValues(Object)) to add the image value to the cell.

## December 15, 2021

**Deprecated**

Versions 1.0 and 1.1 of the TLS security protocol are disabled. To establish [JDBC](https://developers.google.com/apps-script/guides/jdbc) connections, use TLS 1.2 or higher.

## September 01, 2021

**Feature**

In the HTML Service iframe sandbox, `allow-top-navigation`, which allows the content to navigate its top-level browsing context, is restricted and not set as an attribute in the sandbox. Instead, the `allow-top-navigation-by-user-activation` attribute has been added to the sandbox.

If you need to redirect your script, add a link or a button for the user to take action on.

Learn more about [HMTL Service restrictions](https://developers.google.com/apps-script/guides/html/restrictions).

## August 31, 2021

**Feature**

The [Drive Service](https://developers.google.com/apps-script/reference/drive) has added three new methods to the [file](https://developers.google.com/apps-script/reference/drive/file) and [folder](https://developers.google.com/apps-script/reference/drive/folder) classes to manage the use of resource keys when sharing files and folders.

- `getSecurityUpdateEligible()`: Gets whether a file for folder is eligible to apply the security update that requires a resource key for access when it's shared using a link.
- `getSecurityUpdateEnabled()`: Gets whether a file or folder requires a resource key for access when it's shared using a link.
- `setSecurityUpdateEnabled(enabled)`: Sets whether the file or folder requires a resource key for access when it's shared using a link.

Learn more about the [resource key security update for Drive](https://support.google.com/drive/answer/10729743).

## August 23, 2021

**Feature**

The [Document Service](https://developers.google.com/apps-script/reference/document) has added support for smart chips by adding three new classes:

- [Date](https://developers.google.com/apps-script/reference/document/date) - An element representing a formatted date.
- [Person](https://developers.google.com/apps-script/reference/document/person) - An element representing a link to a person.
- [RichLink](https://developers.google.com/apps-script/reference/document/rich-link) - An element representing a link to a Google resource, such as a Drive file or a YouTube video.

Learn more about [smart chips in Google Docs](https://support.google.com/docs/answer/10710316).

## August 09, 2021

**Change**

The Microsoft SQL Server JDBC driver was updated to version 7.2.1. If you encounter issues, [report them on the issue tracker](https://issuetracker.google.com/issues?q=componentid:191640%2B). If you're an administrator and need live support, [contact Google Workspace support](https://knowledge.workspace.google.com/admin/support/contact-google-workspace-support).

## June 01, 2021

**Feature**

A new divider widget has been added for Google Workspace Add-ons. To add a divider to an add-on card, use the [`newDivider()` method](https://developers.google.com/apps-script/reference/card-service/card-service#newdivider) within the [Card service](https://developers.google.com/apps-script/reference/card-service/card-service).

## May 27, 2021

**Feature**

A new method has been added to the [`Sheet` class](https://developers.google.com/apps-script/reference/spreadsheet/sheet#setrowheightsforcedstartrow,-numrows,-height) of the [`Spreadsheet` service](https://developers.google.com/apps-script/reference/spreadsheet). [`setRowHeightsForced(startRow, numRows, height)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#setrowheightsforcedstartrow,-numrows,-height) lets you manually set the height for a row or a set of rows.

## March 15, 2021

**Change**

The following updates have been made to deployments in the new editor:

- You can now have more than one active deployment.
- You can now change the version associated with an active deployment.

To learn more, see [Create and manage deployments](https://developers.google.com/apps-script/concepts/deployments).

## December 07, 2020

**Announcement**

The Apps Script integrated development environment, or IDE, has been fully redesigned. Along with a completely new interface, the following features have been updated:

- The editor now has a collapsible left sidebar to navigate to the Apps Script project overview, settings, executions, and triggers.
- The editor's resources panel now includes files, advanced services, and libraries.
- Autoformatting has been added to the editor.
- Autocomplete in the editor has been enhanced to be faster, more consistent, and extends its support to user-defined functions and JavaScript language features. You can add JSDoc to your functions for better autocomplete suggestions.
- The editor now supports codeblock and function collapsing.
- Keyboard shortcuts and a Command Palette has been added to the editor. Press F1 to view the Command Palette and available keyboard shortcuts.
- The editor now includes a contextual right-click menu with options such as Go To Symbol, Rename Symbols, and Command Palette.
- Enhancements have been made to the debugger's performance and speed.
- Logs now stream in real-time as you run a script.
- The deployments dialog auto-detects the deployment types from the script project's manifest. You can change or add more types as needed.
- Deployments have been merged with versions. Each time you create a new deployment, a new version is automatically created. clasp users are unaffected by this change.
- A single deployment can be an add-on deployment , web app, library, or API executable. Any deployment can be used as a library.
- Now only one deployment can be active at a time. This change doesn't affect existing active deployments. clasp users are unaffected by this change.
- You can no longer explicitly deactivate published web apps. Instead, delete the deployment that has the web app. To reactivate the web app, deploy it again.
- The debugger is no longer supported in the Rhino runtime. To use the debugger, [migrate your script to the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime/migration).
- Testing Editor Add-ons is not yet supported in this release and will be added in 2021. To test Editor Add-ons, switch back to the legacy IDE.

To switch back to the legacy IDE from within the editor, at the top, click **Use legacy editor**.

## October 23, 2020

**Feature**

An advanced service for [Google Tables](https://tables.area120.google.com/u/0/home) has been added to Apps Script. The [`Tables` service](https://developers.google.com/apps-script/advanced/tables) allows scripts to programmatically read and edit rows within `Tables`.

## September 03, 2020

**Feature**

New classes and methods have been added to support [Connected Sheets](https://gsuiteupdates.googleblog.com/2020/08/connected-sheets-api-apps-script.html).

The following new classes have been added to the [`Spreadsheet` service](https://developers.google.com/apps-script/reference/spreadsheet):

- `DataSourceChart`
- `DataSourceColumn`
- `DataSourceFormula`
- `DataSourcePivotTable`
- `DataSourceRefreshSchedule`
- `DataSourceRefreshScheduleFrequency`
- `DataSourceSheet`
- `DataSourceSheetFilter`
- `DataSourceTableColumn`
- `DataSourceTableFilter`
- `DateTimeGroupingRule`
- `PivotGroupLimit`
- `SortSpec`

New methods to support Connected Sheets have been added to the following classes in the [`Spreadsheet` service](https://developers.google.com/apps-script/reference/spreadsheet):

- `BigQueryDataSourceSpecBuilder`
- `BigQueryDataSourceSpec`
- `DataExecutionStatus`
- `DataSourceTable`
- `DataSource`
- `EmbeddedChart`
- `FilterCriteriaBuilder`
- `PivotFilter`
- `PivotGroup`
- `PivotTable`
- `PivotValue`
- `Range`
- `Sheet`
- `SpreadsheetApp`
- `Spreadsheet`

## August 27, 2020

**Feature**

A new class called [`DecoratedText`](https://developers.google.com/apps-script/reference/card-service/decorated-text) has been added to the [Card Service](https://developers.google.com/apps-script/reference/card-service/card-service). `DecoratedText` adds text with optional decorations and was added to replace the [`KeyValue` class](https://developers.google.com/apps-script/reference/card-service/key-value).

## July 27, 2020

**Deprecated**

The following [`Folder` class methods](https://developers.google.com/apps-script/reference/drive/folder) have been [deprecated](https://developers.google.com/apps-script/reference/drive/folder#expandable-1):

- `addFile(File)`
- `addFolder(Folder)`
- `removeFile(File)`
- `removeFolder(Folder)`

**Announcement**

To help [simplify Google Drive's folder structure and sharing models](https://cloud.google.com/blog/products/g-suite/simplifying-google-drives-folder-structure-and-sharing-models), new methods have been added to the [`Drive` service](https://developers.google.com/apps-script/reference/drive) and some existing methods have been deprecated.

**Feature**

The `DriveApp` now has an `enforceSingleParent(value)` method that enables or disables `enforceSingleParent` behavior.

- The [`File` class](https://developers.google.com/apps-script/reference/drive/file) now has the following methods:

  - `file.getTargetId()`: Gets a shortcut's file ID.
  - `file.getTargetMimeType()`: Returns the mime type of the item a shortcut points to.
  - `file.moveTo(destination)`: Moves a file to a specified destination folder.

The [`Folder` class](https://developers.google.com/apps-script/reference/drive/folder) now has the following methods:

- `folder.createShortcut(targetId)`: Creates a shortcut to the provided Drive item ID, and returns it.
- `folder.moveTo(destination)`: Moves an item to the provided destination folder.

## June 12, 2020

**Feature**

New methods have been added to the [`Spreadsheet` service](https://developers.google.com/apps-script/reference/spreadsheet):

- The [`RichTextValue` class](https://developers.google.com/apps-script/reference/spreadsheet/rich-text-value) now has a `RichTextValue.getLinkUrl()` method that gets the URL of the specified value.
- The [`RichTextValueBuilder` class](https://developers.google.com/apps-script/reference/spreadsheet/rich-text-value-builder) now has a `RichTextValueBuilder.setLinkUrl()` method that sets the link URL for the specified value.
- The [`PivotTable` class](https://developers.google.com/apps-script/reference/spreadsheet/pivot-table) now has a `PivotTable.getSourceDataRange()` method that returns the source data range on which the pivot table is constructed.
- The [`PivotValue` class](https://developers.google.com/apps-script/reference/spreadsheet/pivot-value) now has a `PivotValue.remove()` method that removes the value from the pivot table.

## April 22, 2020

**Feature**

A new simple trigger, [`onSelectionChange(e)`](https://developers.google.com/apps-script/guides/triggers#onselectionchangee), has been added for Google Sheets. The `onSelectionChange(e)` trigger runs automatically when a user changes the selection in a spreadsheet.

## April 02, 2020

**Feature**

The following has been added to the [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet):

- A new [`Drawing` class](https://developers.google.com/apps-script/reference/spreadsheet/drawing) has been added to support drawings.
- You can now get your drawings with the [`Sheet.getDrawings()` method](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getdrawings).

The following has been added to the [Drive service](https://developers.google.com/apps-script/reference/drive):

- There's a new `FILE_ORGANIZER` value in the [`Permission` enum](https://developers.google.com/apps-script/reference/drive/permission). If you have `FILE_ORGANIZER` permission on a shared drive, you can edit, trash, and move content within that drive.

## February 28, 2020

**Feature**

The following methods have been added to the [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) to support the use of theme colors. Many of these methods duplicate the effect of existing color methods, but let you use [`Color` objects](https://developers.google.com/apps-script/reference/spreadsheet/color) instead of strings as parameters and return types:

- The [`Banding` class](https://developers.google.com/apps-script/reference/spreadsheet/banding) now has 16 new methods that manipulate color in the banding columns and rows using `Color` objects.
- The [`BooleanCondition` class](https://developers.google.com/apps-script/reference/spreadsheet/boolean-condition) now has two new methods that retrieve the color of the condition's background and font as `Color` objects.
- The [`ConditionalFormatRuleBuilder` class](https://developers.google.com/apps-script/reference/spreadsheet/conditional-format-rule-builder) now has seven new methods that set color-based format rules using `Color` objects.
- The [`GradientCondition` class](https://developers.google.com/apps-script/reference/spreadsheet/gradient-condition) now has three new methods that retrieve condition colors as `Color` objects.
- The [`Range` class](https://developers.google.com/apps-script/reference/spreadsheet/range) now has eight new methods that get and set font and background colors using `Color` objects.
- The [`Sheet` class](https://developers.google.com/apps-script/reference/spreadsheet/sheet) now has two new methods that get and set tab colors using `Color` objects.
- The [`Slicer` class](https://developers.google.com/apps-script/reference/spreadsheet/slicer) now has two new methods that get and set the background color of the slicer using `Color` objects.
- The [`TextStyleBuilder` class](https://developers.google.com/apps-script/reference/spreadsheet/text-style-builder) now has a [`TextStyleBuilder.setForegroundColorObject(color)` method](https://developers.google.com/apps-script/reference/spreadsheet/text-style-builder#setForegroundColorObject(Color)) that updates the foreground color of the style builder using a `Color` object.
- The [`TextStyle` class](https://developers.google.com/apps-script/reference/spreadsheet/text-style) now has a [`TextStyle.getForegroundColorObject()` method](https://developers.google.com/apps-script/reference/spreadsheet/text-style#getForegroundColorObject()) that gets the foreground color of the style as a `Color` object.

## February 05, 2020

**Announcement**

Apps Script now supports the [V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime). This enables modern JavaScript features and syntax in Apps Script. You can [migrate existing scripts](https://developers.google.com/apps-script/guides/v8-runtime/migration) to use V8 and its features.

## January 21, 2020

**Feature**

To support the launch of [G Suite Add-ons](https://developers.google.com/gsuite/add-ons/concepts/types#g_suite_add-ons), the following manifest changes, service, classes, and methods have been added to Add-ons:

- The add-ons [manifest structure](https://developers.google.com/apps-script/manifest) has been updated to provide configuration controls for G Suite Add-ons. All add-on manifest settings are specified in the [`AddOns` object](https://developers.google.com/apps-script/manifest/addons) in the manifest. Manifest fields that previously supported Gmail add-ons still exist, but are now deprecated. See [Upgrading your published add-ons](https://developers.google.com/gsuite/add-ons/how-tos/upgrade-addons) for instructions on how to upgrade a Gmail add-on into a G Suite add-on.
- The [Card service](https://developers.google.com/apps-script/reference/card-service) has been extended with the following classes and methods that provide new widgets and event responses:

  - [`CalendarEventActionResponse`](https://developers.google.com/apps-script/reference/card-service/calendar-event-action-response)
  - [`CalendarEventActionResponseBuilder`](https://developers.google.com/apps-script/reference/card-service/calendar-event-action-response-builder)
  - [`DatePicker`](https://developers.google.com/apps-script/reference/card-service/date-picker)
  - [`DateTimePicker`](https://developers.google.com/apps-script/reference/card-service/date-time-picker)
  - [`DisplayStyle`](https://developers.google.com/apps-script/reference/card-service/display-style)
  - [`DriveItemsSelectedActionResponse`](https://developers.google.com/apps-script/reference/card-service/drive-items-selected-action-response)
  - [`DriveItemsSelectedActionResponseBuilder`](https://developers.google.com/apps-script/reference/card-service/drive-items-selected-action-response-builder)
  - [`FixedFooter`](https://developers.google.com/apps-script/reference/card-service/fixed-footer)
  - [`SwitchControlType`](https://developers.google.com/apps-script/reference/card-service/switch-control-type)
  - [`TimePicker`](https://developers.google.com/apps-script/reference/card-service/time-picker)
  - [`CardBuilder.setDisplayStyle(displayStyle)`](https://developers.google.com/apps-script/reference/card-service/card-builder#setDisplayStyle(DisplayStyle))
  - [`CardBuilder.setFixedFooter(fixedFooter)`](https://developers.google.com/apps-script/reference/card-service/card-builder#setfixedfooterfixedfooter)
  - [`CardBuilder.setPeekCardHeader(peekCardHeader)`](https://developers.google.com/apps-script/reference/card-service/card-builder#setpeekcardheaderpeekcardheader)
  - [`CardService.newCalendarEventActionResponseBuilder()`](https://developers.google.com/apps-script/reference/card-service/card-service#newcalendareventactionresponsebuilder)
  - [`CardService.newDatePicker()`](https://developers.google.com/apps-script/reference/card-service/card-service#newdatepicker)
  - [`CardService.newDateTimePicker()`](https://developers.google.com/apps-script/reference/card-service/card-service#newdatetimepicker)
  - [`CardService.newDriveItemsSelectedActionResponseBuilder()`](https://developers.google.com/apps-script/reference/card-service/card-service#newdriveitemsselectedactionresponsebuilder)
  - [`CardService.newFixedFooter()`](https://developers.google.com/apps-script/reference/card-service/card-service#newfixedfooter)
  - [`CardService.newTimePicker()`](https://developers.google.com/apps-script/reference/card-service/card-service#newtimepicker)
  - [`Switch.setControlType(controlType)`](https://developers.google.com/apps-script/reference/card-service/switch#setcontroltypecontroltype)

The [Conference Data service](https://developers.google.com/apps-script/reference/conference-data) has been added to Apps Script. The service helps G Suite Add-ons that extend Google Calendar to stay in sync with third-party conferencing applications. This service is only useful to developers who manage a conferencing application and want to make it available in Google Calendar.

## December 18, 2019

**Feature**

The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following class and new methods to support using color building and theme colors:

- [`Color`](https://developers.google.com/apps-script/reference/spreadsheet/color)
- [`ColorBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/color-builder)
- [`SpreadsheetTheme`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-theme)
- [`ThemeColor`](https://developers.google.com/apps-script/reference/spreadsheet/theme-color)
- [`ThemeColorType`](https://developers.google.com/apps-script/reference/spreadsheet/theme-color-type)
- [`SpreadsheetApp.newColor()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newcolor)
- [`Spreadsheet.getPredefinedSpreadsheetThemes()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getpredefinedspreadsheetthemes)
- [`Spreadsheet.getSpreadsheetTheme()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getspreadsheettheme)
- [`Spreadsheet.resetSpreadsheetTheme()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#resetspreadsheettheme)
- [`Spreadsheet.setSpreadsheetTheme(theme)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#setspreadsheetthemetheme)

## December 11, 2019

**Feature**

The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been extended with the following class and new methods to support different response types and dynamic statuses:

- [`GetDataResponse`](https://developers.google.com/apps-script/reference/data-studio/get-data-response)
- [`GetSchemaResponse`](https://developers.google.com/apps-script/reference/data-studio/get-schema-response)
- [`SetCredentialsResponse`](https://developers.google.com/apps-script/reference/data-studio/set-credentials-response)
- [`Checkbox.setIsDynamic(isDynamic)`](https://developers.google.com/apps-script/reference/data-studio/checkbox#setisdynamicisdynamic)
- [`CommunityConnector.newGetDataResponse()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newgetdataresponse)
- [`CommunityConnector.newGetSchemaResponse()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newgetschemaresponse)
- [`CommunityConnector.newSetCredentialsResponse()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newsetcredentialsresponse)
- [`Config.setIsSteppedConfig(isSteppedConfig)`](https://developers.google.com/apps-script/reference/data-studio/config#setissteppedconfigissteppedconfig)
- [`SelectMultiple.setIsDynamic(isDynamic)`](https://developers.google.com/apps-script/reference/data-studio/select-multiple#setisdynamicisdynamic)
- [`SelectSingle.setIsDynamic(isDynamic)`](https://developers.google.com/apps-script/reference/data-studio/select-single#setisdynamicisdynamic)
- [`TextArea.setIsDynamic(isDynamic)`](https://developers.google.com/apps-script/reference/data-studio/text-area#setisdynamicisdynamic)
- [`TextInput.setIsDynamic(isDynamic)`](https://developers.google.com/apps-script/reference/data-studio/text-input#setisdynamicisdynamic)

## November 06, 2019

**Feature**

The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following class and new methods to support using slicers to filter ranges, charts, and pivot tables:

- [`Slicer`](https://developers.google.com/apps-script/reference/spreadsheet/slicer)
- [`Sheet.getSlicers()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getslicers)
- [`Sheet.insertSlicer(range, anchorRowPos, anchorColPos)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#insertslicerrange,-anchorrowpos,-anchorcolpos)
- [`Sheet.insertSlicer(range, anchorRowPos, anchorColPos, offsetX, offsetY)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#insertslicerrange,-anchorrowpos,-anchorcolpos,-offsetx,-offsety)

The [Script service](https://developers.google.com/apps-script/reference/script) has been extended with the [`ScriptApp.getIdentityToken()` method](https://developers.google.com/apps-script/reference/script/script-app#getidentitytoken), which returns an identity token for the effective user.

## October 28, 2019

**Deprecated**

You can no longer publish web apps to the Chrome Web Store. The Chrome Web Store [deprecated Chrome apps in 2016](https://blog.chromium.org/2016/08/from-chrome-apps-to-web.html) and they are now only available for ChromeOS devices. This change includes published Apps Script web apps. Previously published web apps are no longer discoverable in the Chrome Web Store. [Editor Add-ons](https://developers.google.com/gsuite/add-ons/concepts/types#editor_add-ons) aren't affected; you can still [publish Editor Add-ons](https://developers.google.com/gsuite/add-ons/how-tos/publishing-editor-addons) to the Chrome Web Store.

## October 23, 2019

**Deprecated**

Several classes and methods relating to the now shutdown [UiApp service](https://developers.google.com/apps-script/guides/support/sunset) have been removed. Most of these methods involved interactions between the [Charts service](https://developers.google.com/apps-script/reference/charts) and `UiApp` that were very seldom used. The following is a full list of the removed classes and methods:

- [Charts service](https://developers.google.com/apps-script/reference/charts)
  - `CategoryFilterBuilder`
  - `Control`
  - `DashboardPanel`
  - `DashboardPanelBuilder`
  - `Chart.getId()`
  - `Chart.getType()`
  - `Charts.newCategoryFilter()`
  - `Charts.newDashboardPanel()`
  - `Charts.newNumberRangeFilter()`
  - `Charts.newStringFilter()`
  - `NumberRangeFilterBuilder.build()`
  - `NumberRangeFilterBuilder.setDataTable(tableBuilder)`
  - `NumberRangeFilterBuilder.setDataTable(table)`
  - `NumberRangeFilterBuilder.setFilterColumnIndex(columnIndex)`
  - `NumberRangeFilterBuilder.setFilterColumnLabel(columnLabel)`
  - `NumberRangeFilterBuilder.setLabel(label)`
  - `NumberRangeFilterBuilder.setLabelSeparator(labelSeparator)`
  - `NumberRangeFilterBuilder.setLabelStacking(orientation)`
  - `StringFilterBuilder.build()`
  - `StringFilterBuilder.setDataTable(tableBuilder)`
  - `StringFilterBuilder.setDataTable(table)`
  - `StringFilterBuilder.setFilterColumnIndex(columnIndex)`
  - `StringFilterBuilder.setFilterColumnLabel(columnLabel)`
  - `StringFilterBuilder.setLabel(label)`
  - `StringFilterBuilder.setLabelSeparator(labelSeparator)`
  - `StringFilterBuilder.setLabelStacking(orientation)`
- [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet)
  - `EmbeddedChart.getId()`
  - `EmbeddedChart.getType()`
  - `EmbeddedChart.setId(id)`

**Change**

The [Slides service](https://developers.google.com/apps-script/reference/slides) class `RgbColor` and the enumeration `ColorType` have been moved from the Slides service to the [Base script service](https://developers.google.com/apps-script/reference/base). The functionality of these classes has not changed. Moving these classes to the Base script service enables other services to make use of them in the future. You can now find the documentation for these classes at [`RgbColor`](https://developers.google.com/apps-script/reference/base/rgb-color) and [`ColorType`](https://developers.google.com/apps-script/reference/base/color-type).

## September 09, 2019

**Change**

The [Card service](https://developers.google.com/apps-script/reference/card-service) methods [`CardHeader.setUrl(url)`](https://developers.google.com/apps-script/reference/card-service/card-header#setimageurlimageurl) and [`Image.setUrl(url)`](https://developers.google.com/apps-script/reference/card-service/image#setimageurlurl) have been updated to accept an encoded image data string as an input parameter. As before, you can alternatively use a publicly-available image URL as the input parameter.

## August 07, 2019

**Deprecated**

Documentation for the UI service has been removed. This service was deprecated in December 2014 and officially [shut down on July 15, 2019](https://developers.google.com/apps-script/guides/support/sunset#ui-service). To build interfaces for web apps and Editor Add-ons, use the [HTML service](https://developers.google.com/apps-script/reference/html).

## July 26, 2019

**Feature**

- The [Group service](https://developers.google.com/apps-script/reference/groups) has been updated with the [`Groups.getRoles(user)` method](https://developers.google.com/apps-script/reference/groups/group#getrolesusers) that can determine the list of roles a specific user in a group has.
- The [Slides service](https://developers.google.com/apps-script/reference/slides) has been extended with the following new methods to support concrete color schemes:
  - [`ColorScheme.setConcreteColor(type, color)`](https://developers.google.com/apps-script/reference/slides/color-scheme#setconcretecolortype-color)
  - [`ColorScheme.setConcreteColor(type, red, green, blue)`](https://developers.google.com/apps-script/reference/slides/color-scheme#setconcretecolortype-red-green-blue)
  - [`ColorScheme.setConcreteColor(type, hexColor)`](https://developers.google.com/apps-script/reference/slides/color-scheme#setconcretecolortype-hexcolor)
- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new methods to support trimming whitespace and removing duplicate values:
  - [`RangeList.trimWhitespace()`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#trimwhitespace)
  - [`Range.removeDuplicates()`](https://developers.google.com/apps-script/reference/spreadsheet/range#removeduplicates)
  - [`Range.removeDuplicates(columnsToCompare)`](https://developers.google.com/apps-script/reference/spreadsheet/range#removeduplicatescolumnstocompare)
  - [`Range.trimWhitespace()`](https://developers.google.com/apps-script/reference/spreadsheet/range#trimwhitespace)

## May 20, 2019

**Feature**

- The [Gmail service](https://developers.google.com/apps-script/reference/gmail) has been updated with the [`GmailMessage.getHeader(name)` method](https://developers.google.com/apps-script/reference/gmail/gmail-message#getheadername) that can retrieve a RFC 2822 header from a message.
- The [Optimization service](https://developers.google.com/apps-script/reference/optimization) has been updated with the following batch methods:
  - [`LinearOptimizationEngine.addContraints(lowerBounds, upperBounds, variableNames, coefficients)`](https://developers.google.com/apps-script/reference/optimization/linear-optimization-engine#addconstraintslowerbounds-upperbounds-variablenames-coefficients)
  - [`LinearOptimizationEngine.addVariables(names, lowerBounds, upperBounds, types, objectiveCoeffients)`](https://developers.google.com/apps-script/reference/optimization/linear-optimization-engine#addvariablesnames-lowerbounds-upperbounds-types-objectivecoefficients)

## May 03, 2019

**Feature**

The [Document service](https://developers.google.com/apps-script/reference/document) has been updated to add methods to get and set the language of a document:

- [`Document.getLanguage()`](https://developers.google.com/apps-script/reference/document/document#getlanguage)
- [`Document.getSupportedLanguageCodes()`](https://developers.google.com/apps-script/reference/document/document#getsupportedlanguagecodes)
- [`Document.setLanguage(languageCode)`](https://developers.google.com/apps-script/reference/document/document#setlanguagelanguagecode)

## April 19, 2019

**Feature**

The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been updated to add a few values to [`FieldType` enum](https://developers.google.com/apps-script/reference/data-studio/field-type):

- `HYPERLINK`
- `IMAGE`
- `IMAGE_LINK`

## April 08, 2019

**Change**

The behavior of the [Google Cloud (GCP) projects](https://developers.google.com/apps-script/guides/cloud-platform-projects) used by scripts has been altered. Now, the [default GCP projects](https://developers.google.com/apps-script/guides/cloud-platform-projects#default_cloud_platform_projects) that Apps Script creates for new scripts are hidden and script owners can't access them directly. Admins and domain users with the `resourcemanager.projects.list` permission on the parenting GCP folder can still access default GCP projects.

If you need access to a script's GCP project (because you wish to publish it or take a similar action), it's best to switch your script to use a [standard GCP project](https://developers.google.com/apps-script/guides/cloud-platform-projects#standard_cloud_platform_projects).

## April 05, 2019

**Feature**

- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new classes and methods to support text finding, checkboxes, and other features:
  - [`TextFinder`](https://developers.google.com/apps-script/reference/spreadsheet/text-finder)
  - [`RecalculationInterval`](https://developers.google.com/apps-script/reference/spreadsheet/recalculation-interval)
  - [`SheetType`](https://developers.google.com/apps-script/reference/spreadsheet/sheet-type)
  - [`DataValidationBuilder.requireCheckbox()`](https://developers.google.com/apps-script/reference/spreadsheet/data-validation-builder#requirecheckbox)
  - [`DataValidationBuilder.requireCheckbox(checkedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/data-validation-builder#requirecheckboxcheckedvalue)
  - [`DataValidationBuilder.requireCheckbox(checkedValue, uncheckedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/data-validation-builder#requirecheckboxcheckedvalue-uncheckedvalue)
  - A `clearRanges()` method has been added to the all the embedded chart type builder classes, such as [`EmbeddedAreaChartBuilder.clearRanges()`](https://developers.google.com/apps-script/reference/spreadsheet/embedded-area-chart-builder#clearranges)
  - [`EmbeddedChart.getChartId()`](https://developers.google.com/apps-script/reference/spreadsheet/embedded-chart#getchartid)
  - [`RangeList.check()`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#check)
  - [`RangeList.insertCheckboxes()`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#insertcheckboxes)
  - [`RangeList.insertCheckboxes(checkedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#insertcheckboxescheckedvalue)
  - [`RangeList.insertCheckboxes(checkedValue, uncheckedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#insertcheckboxescheckedvalue-uncheckedvalue)
  - [`RangeList.removeCheckboxes()`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#removecheckboxes)
  - [`RangeList.uncheck()`](https://developers.google.com/apps-script/reference/spreadsheet/range-list#uncheck)
  - [`Range.check()`](https://developers.google.com/apps-script/reference/spreadsheet/range#check)
  - [`Range.createTextFinder(findText)`](https://developers.google.com/apps-script/reference/spreadsheet/range#createtextfinderfindtext)
  - [`Range.getDataRegion()`](https://developers.google.com/apps-script/reference/spreadsheet/range#getdataregion)
  - [`Range.getDataRegion(dimension)`](https://developers.google.com/apps-script/reference/spreadsheet/range#getdataregiondimension)
  - [`Range.insertCheckboxes()`](https://developers.google.com/apps-script/reference/spreadsheet/range#insertcheckboxes)
  - [`Range.insertCheckboxes(checkedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/range#insertcheckboxescheckedvalue)
  - [`Range.insertCheckboxes(checkedValue, uncheckedValue)`](https://developers.google.com/apps-script/reference/spreadsheet/range#insertcheckboxescheckedvalue-uncheckedvalue)
  - [`Range.removeCheckboxes()`](https://developers.google.com/apps-script/reference/spreadsheet/range#removecheckboxes)
  - [`Range.uncheck()`](https://developers.google.com/apps-script/reference/spreadsheet/range#uncheck)
  - [`Sheet.createTextFinder(findText)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#createtextfinderfindtext)
  - [`Sheet.getType()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#gettype)
  - [`Spreadsheet.createTextFinder(findText)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#createtextfinderfindtext)
  - [`Spreadsheet.getIterativeCalculationConvergenceThreshold()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getiterativecalculationconvergencethreshold)
  - [`Spreadsheet.getMaxIterativeCalculationCycles()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getmaxiterativecalculationcycles)
  - [`Spreadsheet.getRecalculationInterval()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getrecalculationinterval)
  - [`Spreadsheet.isIterativeCalculationEnabled()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#isiterativecalculationenabled)
  - [`Spreadsheet.moveChartToObjectSheet(chart)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#movecharttoobjectsheetchart)
  - [`Spreadsheet.setIterativeCalculationConvergenceThreshold(minThreshold)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#setiterativecalculationconvergencethresholdminthreshold)
  - [`Spreadsheet.setIterativeCalculationEnabled(isEnabled)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#setiterativecalculationenabledisenabled)
  - [`Spreadsheet.setMaxIterativeCalculationCycles(maxIterations)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#setmaxiterativecalculationcyclesmaxiterations)
  - [`Spreadsheet.setRecalculationInterval(recalculationInterval)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#setrecalculationintervalrecalculationinterval)
- The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been extended with the following new classes and methods that support configuring BigQuery connectors:
  - [`BigQueryConfig`](https://developers.google.com/apps-script/reference/data-studio/big-query-config)
  - [`BigQueryParameterType`](https://developers.google.com/apps-script/reference/data-studio/big-query-parameter-type)
  - [`CommunityConnector.newBigQueryConfig()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newBigQueryConfig())
- The [`Notification` objects](https://developers.google.com/apps-script/reference/card-service/notification) in the [Card service](https://developers.google.com/apps-script/reference/card-service) no longer have a type that you must set. Calls to the now removed `Notification.setType(type)` method result in a no-op.

## February 26, 2019

**Feature**

- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new classes and methods to support [BigQuery data connectors in Sheets](https://cloud.google.com/blog/products/g-suite/connecting-bigquery-and-google-sheets-to-help-with-hefty-data-analysis):

  - [`BigQueryDataSourceSpec`](https://developers.google.com/apps-script/reference/spreadsheet/big-query-data-source-spec)
  - [`BigQueryDataSourceSpecBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/big-query-data-source-spec-builder)
  - [`DataExecutionErrorCode`](https://developers.google.com/apps-script/reference/spreadsheet/data-execution-error-code)
  - [`DataExecutionState`](https://developers.google.com/apps-script/reference/spreadsheet/data-execution-state)
  - [`DataExecutionStatus`](https://developers.google.com/apps-script/reference/spreadsheet/data-execution-status)
  - [`DataSourceParameterType`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-parameter-type)
  - [`DataSourceParameter`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-parameter)
  - [`DataSourceSpecBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec-builder)
  - [`DataSourceSpec`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-spec)
  - [`DataSourceTable`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-table)
  - [`DataSourceType`](https://developers.google.com/apps-script/reference/spreadsheet/data-source-type)
  - [`DataSource`](https://developers.google.com/apps-script/reference/spreadsheet/data-source)
  - [`Range.getDataSourceTables()`](https://developers.google.com/apps-script/reference/spreadsheet/range#getdatasourcetables)
  - [`Sheet.getDataSourceTables()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getdatasourcetables)
  - [`SpreadsheetApp.enableAllDataSourcesExecution()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#enablealldatasourcesexecution)
  - [`SpreadsheetApp.enableBigQueryExecution()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#enablebigqueryexecution)
  - [`SpreadsheetApp.newDataSourceSpec()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newdatasourcespec)
  - [`Spreadsheet.getDataSourceTables()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getdatasourcetables)
  - [`Spreadsheet.insertSheetWithDataSourceTable(spec)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#insertsheetwithdatasourcetablespec)
- The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been extended with the following new methods involving reaggregation settings:

  - [`Field.getIsReaggregatable()`](https://developers.google.com/apps-script/reference/data-studio/field#getisreaggregatable)
  - [`Field.setIsReaggregatable(isReaggregatable)`](https://developers.google.com/apps-script/reference/data-studio/field#setisreaggregatableisreaggregatable)

## January 22, 2019

**Deprecated**

The deprecated [UiApp service](https://developers.google.com/apps-script/reference/ui) will be officially shutdown on July 15th, 2019. After this date, the service will no longer function for any script project.

**Feature**

- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new classes and methods to support text styles and Rich Text cell formatting:
  - [`RichTextValue`](https://developers.google.com/apps-script/reference/spreadsheet/rich-text-value)
  - [`RichTextValueBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/rich-text-value-builder)
  - [`TextStyle`](https://developers.google.com/apps-script/reference/spreadsheet/text-style)
  - [`TextStyleBuilder`](https://developers.google.com/apps-script/reference/spreadsheet/text-style-builder)
  - [`Range.getRichTextValue()`](https://developers.google.com/apps-script/reference/spreadsheet/range#getrichtextvalue)
  - [`Range.getRichTextValues()`](https://developers.google.com/apps-script/reference/spreadsheet/range#getrichtextvalues)
  - [`Range.getTextStyle()`](https://developers.google.com/apps-script/reference/spreadsheet/range#gettextstyle)
  - [`Range.getTextStyles()`](https://developers.google.com/apps-script/reference/spreadsheet/range#gettextstyles)
  - [`Range.setRichTextValue(value)`](https://developers.google.com/apps-script/reference/spreadsheet/range#setrichtextvaluevalue)
  - [`Range.setRichTextValues(values)`](https://developers.google.com/apps-script/reference/spreadsheet/range#setrichtextvaluesvalues)
  - [`Range.setTextStyle(style)`](https://developers.google.com/apps-script/reference/spreadsheet/range#settextstylestyle)
  - [`Range.setTextStyles(styles)`](https://developers.google.com/apps-script/reference/spreadsheet/range#settextstylesstyles)
  - [`SpreadsheetApp.newRichTextValue()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newrichtextvalue)
  - [`SpreadsheetApp.newTextStyle()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app#newtextstyle)
- The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been extended with the following new classes and methods that define and support authentication types for community connectors:
  - [`GetAuthTypeResponse`](https://developers.google.com/apps-script/reference/data-studio/get-auth-type-response)
  - [`AuthType`](https://developers.google.com/apps-script/reference/data-studio/auth-type)
  - [`CommunityConnector.newAuthTypeResponse()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newauthtyperesponse)

## January 04, 2019

**Feature**

- The [Slides service](https://developers.google.com/apps-script/reference/slides) has been extended with the following new classes and methods that support slide linking and text box insertion:
  - [`SlideLinkingMode`](https://developers.google.com/apps-script/reference/slides/slide-linking-mode)
  - [`Layout.insertTextBox(text)`](https://developers.google.com/apps-script/reference/slides/layout#inserttextboxtext)
  - [`Layout.insertTextBox(text, left, top, width, height)`](https://developers.google.com/apps-script/reference/slides/layout#inserttextboxtext-left-top-width-height)
  - [`Master.insertTextBox(text)`](https://developers.google.com/apps-script/reference/slides/master#inserttextboxtext)
  - [`Master.insertTextBox(text, left, top, width, height)`](https://developers.google.com/apps-script/reference/slides/master#inserttextboxtext-left-top-width-height)
  - [`Page.insertTextBox(text)`](https://developers.google.com/apps-script/reference/slides/page#inserttextboxtext)
  - [`Page.insertTextBox(text, left, top, width, height)`](https://developers.google.com/apps-script/reference/slides/page#inserttextboxtext-left-top-width-height)
  - [`Presentation.appendSlide(slide, linkingMode)`](https://developers.google.com/apps-script/reference/slides/presentation#appendslideslide-linkingmode)
  - [`Presentation.insertSlide(insertionIndex, slide, linkingMode)`](https://developers.google.com/apps-script/reference/slides/presentation#insertslideinsertionindex-slide-linkingmode)
  - [`Slide.getSlideLinkingMode()`](https://developers.google.com/apps-script/reference/slides/slide#getslidelinkingmode)
  - [`Slide.getSourcePresentationId()`](https://developers.google.com/apps-script/reference/slides/slide#getsourcepresentationid)
  - [`Slide.getSourceSlideObjectId()`](https://developers.google.com/apps-script/reference/slides/slide#getsourceslideobjectid)
  - [`Slide.insertTextBox(text)`](https://developers.google.com/apps-script/reference/slides/slide#inserttextboxtext)
  - [`Slide.insertTextBox(text, left, top, width, height)`](https://developers.google.com/apps-script/reference/slides/slide#inserttextboxtext-left-top-width-height)
  - [`Slide.refreshSlide()`](https://developers.google.com/apps-script/reference/slides/slide#refreshslide)
  - [`Slide.unlink()`](https://developers.google.com/apps-script/reference/slides/slide#unlink)
- The [Data Studio service](https://developers.google.com/apps-script/reference/data-studio) has been extended with the following new classes and methods that error displays:
  - [`DebugError`](https://developers.google.com/apps-script/reference/data-studio/debug-error)
  - [`UserError`](https://developers.google.com/apps-script/reference/data-studio/user-error)
  - [`CommunityConnector.newDebugError()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newdebugerror)
  - [`CommunityConnector.newUserError()`](https://developers.google.com/apps-script/reference/data-studio/community-connector#newusererror)

## December 13, 2018

**Deprecated**

The [Fusion Tables advanced service](https://developers.google.com/apps-script/advanced/fusion-tables) has been deprecated and will shutdown fully on December 3rd, 2019.

**Feature**

The [Slides service](https://developers.google.com/apps-script/reference/slides) has been extended with the following new classes and methods that support connector lines:

- [`ConnnectionSite`](https://developers.google.com/apps-script/reference/slides/connection-site)
- [`Group.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/group#getconnectionsites)
- [`Image.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/image#getconnectionsites)
- [`Line.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/line#getconnectionsites)
- [`Line.getEndConnection()`](https://developers.google.com/apps-script/reference/slides/line#getendconnection)
- [`Line.getLineCategory()`](https://developers.google.com/apps-script/reference/slides/line#getlinecategory)
- [`Line.getStartConnection()`](https://developers.google.com/apps-script/reference/slides/line#getstartconnection)
- [`Line.isConnector()`](https://developers.google.com/apps-script/reference/slides/line#isconnector)
- [`Line.setEndConnection(connectionSite)`](https://developers.google.com/apps-script/reference/slides/line#setendconnectionconnectionsite)
- [`Line.setLineCategory(lineCategory)`](https://developers.google.com/apps-script/reference/slides/line#setlinecategorylinecategory)
- [`Line.setStartConnection(connectionSite)`](https://developers.google.com/apps-script/reference/slides/line#setstartconnectionconnectionsite)
- [`LineCategory.UNSUPPORTED`](https://developers.google.com/apps-script/reference/slides/line-category)
- [`PageElement.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/page-element#getconnectionsites)
- [`Shape.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/shape#getconnectionsites)
- [`SheetsChart.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/sheets-chart#getconnectionsites)
- [`Table.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/table#getconnectionsites)
- [`Video.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/video#getconnectionsites)
- [`WordArt.getConnectionSites()`](https://developers.google.com/apps-script/reference/slides/word-art#getconnectionsites)

## November 14, 2018

**Feature**

- The [Card service](https://developers.google.com/apps-script/reference/card-service) has been extended with the following new classes and methods that let you to customize the background of text button widgets:
  - [`TextButtonStyle`](https://developers.google.com/apps-script/reference/card-service/text-button-style)
  - [`TextButton.setBackgroundColor(backgroundColor)`](https://developers.google.com/apps-script/reference/card-service/text-button#setbackgroundcolorbackgroundcolor)
  - [`TextButton.setDisabled(disabled)`](https://developers.google.com/apps-script/reference/card-service/text-button#setdisableddisabled)
  - [`TextButton.setTextButtonStyle(textButtonStyle)`](https://developers.google.com/apps-script/reference/card-service/text-button#settextbuttonstyletextbuttonstyle)
- The [Slides service](https://developers.google.com/apps-script/reference/slides) has been extended with the following new methods that let you control the Z-positioning of page elements in Slides. Other new methods let you add alt titles and alt descriptions to page elements. The following methods have been added to the [`Group`](https://developers.google.com/apps-script/reference/slides/group), [`Image`](https://developers.google.com/apps-script/reference/slides/image), [`Line`](https://developers.google.com/apps-script/reference/slides/line), [`PageElement`](https://developers.google.com/apps-script/reference/slides/page-element), [`Shape`](https://developers.google.com/apps-script/reference/slides/shape), [`SheetsChart`](https://developers.google.com/apps-script/reference/slides/sheets-chart), [`Table`](https://developers.google.com/apps-script/reference/slides/table), [`Video`](https://developers.google.com/apps-script/reference/slides/video), and [`WordArt`](https://developers.google.com/apps-script/reference/slides/word-art) classes:
  - `bringForward()`
  - `bringToFront()`
  - `sendBackward()`
  - `sendToBack()`
  - `setDescription(description)`
  - `setTitle(title)`
- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new classes and methods that let you add and search for metadata strings attached to rows, columns, sheets, or spreadsheets:
  - [`DeveloperMetadata`](https://developers.google.com/apps-script/reference/spreadsheet/developer-metadata)
  - [`DeveloperMetadataFinder`](https://developers.google.com/apps-script/reference/spreadsheet/developer-metadata-finder)
  - [`DeveloperMetadataLocation`](https://developers.google.com/apps-script/reference/spreadsheet/developer-metadata-location)
  - [`DeveloperMetadataLocationType`](https://developers.google.com/apps-script/reference/spreadsheet/developer-metadata-location-type)
  - [`DeveloperMetadataVisibility`](https://developers.google.com/apps-script/reference/spreadsheet/developer-metadata-visibility)
  - [`Range.addDeveloperMetadata(key)`](https://developers.google.com/apps-script/reference/spreadsheet/range#adddevelopermetadatakey)
  - [`Range.addDeveloperMetadata(key, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/range#adddevelopermetadatakey-visibility)
  - [`Range.addDeveloperMetadata(key, value)`](https://developers.google.com/apps-script/reference/spreadsheet/range#adddevelopermetadatakey-value)
  - [`Range.addDeveloperMetadata(key, value, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/range#adddevelopermetadatakey-value-visibility)
  - [`Range.createDeveloperMetadataFinder()`](https://developers.google.com/apps-script/reference/spreadsheet/range#createdevelopermetadatafinder)
  - [`Range.getDeveloperMetadata()`](https://developers.google.com/apps-script/reference/spreadsheet/range#getdevelopermetadata)
  - [`Sheet.addDeveloperMetadata(key)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#adddevelopermetadatakey)
  - [`Sheet.addDeveloperMetadata(key, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#adddevelopermetadatakey-visibility)
  - [`Sheet.addDeveloperMetadata(key, value)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#adddevelopermetadatakey-value)
  - [`Sheet.addDeveloperMetadata(key, value, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#adddevelopermetadatakey-value-visibility)
  - [`Sheet.createDeveloperMetadataFinder()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#createdevelopermetadatafinder)
  - [`Sheet.getDeveloperMetadata()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getdevelopermetadata)
  - [`Spreadsheet.addDeveloperMetadata(key)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#adddevelopermetadatakey)
  - [`Spreadsheet.addDeveloperMetadata(key, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#adddevelopermetadatakey-visibility)
  - [`Spreadsheet.addDeveloperMetadata(key, value)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#adddevelopermetadatakey-value)
  - [`Spreadsheet.addDeveloperMetadata(key, value, visibility)`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#adddevelopermetadatakey-value-visibility)
  - [`Spreadsheet.createDeveloperMetadataFinder()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#createdevelopermetadatafinder)
  - [`Spreadsheet.getDeveloperMetadata()`](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet#getdevelopermetadata)

## October 30, 2018

**Feature**

- The [Spreadsheet service](https://developers.google.com/apps-script/reference/spreadsheet) has been extended with the following new classes and methods:

  - [`OverGridImage`](https://developers.google.com/apps-script/reference/spreadsheet/over-grid-image)
  - [`Sheet.getImages()`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#getimages)
  - [`Sheet.isColumnHiddenByUser(columnPosition)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#iscolumnhiddenbyusercolumnposition)
  - [`Sheet.isRowHiddenByFilter(rowPosition)`](https://developers.google.com/apps-script/reference/spreadsheet/sheet#isrowhiddenbyfilterrowposition)

**Note:** This page shows release notes back to October 30, 2018 as captured. The live page may contain additional older entries not included in this extraction pass.

Source: https://developers.google.com/apps-script/release-notes
