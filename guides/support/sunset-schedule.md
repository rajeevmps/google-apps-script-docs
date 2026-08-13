# Apps Script Sunset Schedule

## Page Summary

- Apps Script features are marked as deprecated before they are shut down, allowing time for migration to supported alternatives.
- Deprecated features remain available until their sunset date, after which they cease to function or become unavailable.
- Developers should upgrade existing scripts to use supported features during the deprecation period to avoid disruptions.
- Google provides migration guides and resources to help developers transition away from deprecated features.
- The table above lists deprecated Apps Script features, their deprecation and sunset dates, and the expected behavior after sunset.

Once a sunset date for an Apps Script feature is announced, the feature is considered deprecated, but is available for use until the sunset date. During the deprecation period, upgrade existing scripts to use supported features.

## Deprecated Features Table

| Feature | Deprecated | Sunset | Behavior after sunset date |
|---------|-----------|--------|---------------------------|
| [`setAuthentication(clientId, signingKey)`](https://developers.google.com/apps-script/reference/maps/maps#setAuthentication(String,String)) | March 03, 2026 | June 01, 2026 | This method is unavailable and existing scripts fail when using this method. |
| Area120Tables | July 16, 2024 | Jan 14, 2026 | Service no longer functions. |
| Analytics Reporting API | July 1, 2024 | June 3, 2025 | Service no longer functions. |
| Rhino Runtime | February 20, 2025 | January 31, 2026 | As of February 20, 2025, the Rhino runtime is deprecated. Scripts running on Rhino will continue to function until January 31, 2026, after which they will no longer execute. Please migrate your scripts to the V8 runtime before this date. Refer to [Migrate scripts to the V8 runtime](https://developers.google.com/apps-script/guides/v8-runtime/migration). |
| Contacts service | December 16, 2022 | January 31, 2025 | Service no longer functions. |
| Sites service | September 19, 2023 | September 24, 2024 | Service no longer functions. |
| `getChatThreads()`, `getChatThreads(start, max)` | July 8, 2022 | November 1, 2022 | These methods are unavailable and existing scripts fail when using these methods. |
| Publish Editor add-ons to the Chrome Web Store | October 29, 2018 | December 16, 2019 | You can no longer publish [Editor add-ons](https://developers.google.com/workspace/add-ons/concepts/types#editor_add-ons) to the Chrome Web Store. Now Editor add-ons are published solely to the [Google Workspace Marketplace](https://workspace.google.com/marketplace/). Add-on developers have been notified to [migrate their add-ons](https://developers.google.com/workspace/add-ons/how-tos/cws-migration) to the Google Workspace Marketplace; most add-ons should now be available there. For new add-ons, see [Publishing an Editor add-on](https://developers.google.com/workspace/add-ons/how-tos/publishing-editor-addons) for the new publication flow. |
| Publish web apps to Chrome Web Store | August 19, 2016 | October 28, 2019 | You can no longer publish web apps to the Chrome Web Store. The Chrome Web Store [deprecated Chrome apps in 2016](https://blog.chromium.org/2016/08/from-chrome-apps-to-web.html) and they are now only available for ChromeOS devices. This change includes published Apps Script web apps. Previously published web apps are no longer discoverable in the Chrome Web Store. |
| [Android Add-ons](https://developers.google.com/workspace/add-ons/mobile) | January 30, 2019 | | New Android add-ons can't be reviewed or published. Existing Android add-ons continue to function. |
| [Fusion Tables advanced service](https://developers.google.com/apps-script/advanced/fusion-tables) | December 11, 2018 | December 3, 2019 | Service no longer functions. |
| [JDBC connections](https://developers.google.com/apps-script/guides/jdbc#creating_google_cloud_sql_connections) to Google Cloud SQL databases using `jdbc:google:rdbms` | April 3, 2018 | April 2019 | JDBC connections that use a `jdbc:google:rdbms:subname` URL connectivity path to a Google Cloud SQL database no longer function. `jdbc:google:mysql:subname` URL connectivity paths and connections made using the generic IP method are unaffected. See [Creating Google Cloud SQL connections](https://developers.google.com/apps-script/guides/jdbc#creating_google_cloud_sql_connections) for migration instructions. |
| [SandboxMode.NATIVE](https://developers.google.com/apps-script/reference/html/sandbox-mode#properties) [SandboxMode.EMULATED](https://developers.google.com/apps-script/reference/html/sandbox-mode#properties) | Oct 13, 2015 | Nov 12, 2015 | All **_new_** scripts now default to `IFRAME` sandbox mode unless `NATIVE` mode is explicitly specified. |
| | | Dec 10, 2015 | `EMULATED` mode was shut down. Any scripts that explicitly request `EMULATED` mode now default to `IFRAME` mode. |
| | | Apr 28, 2016 | **_All scripts, including existing ones,_** now default to `IFRAME` sandbox mode unless `NATIVE` mode is explicitly specified. |
| | | Jul 6, 2016 | `NATIVE` mode was shut down. All HTML served from the HTML Service now uses `IFRAME` mode, no matter what mode is specified. |
| OAuthConfig | March 4, 2015 | July 6, 2015 | Class is longer available and existing scripts do not function. |
| DocsList service | [Dec 11, 2014](http://googleappsdeveloper.blogspot.com/2014/12/speeding-up-htmlservice.html) | April 20, 2015 | Service no longer functions. |
| UI service | June 30, 2015 | | Service will no longer appear in autocomplete, although existing scripts should still function. |
| | | July 15, 2019 | Service no longer functions. |
| Domain service | [May 15, 2014](http://googleappsdeveloper.blogspot.com/2014/05/deprecating-scriptdb-and-domain-service.html) | Dec 11, 2014 | Service no longer functions. |
| ScriptDB service | | Dec 18, 2014 | Service no longer functions. |
| Finance service | [Feb 25, 2014](http://googleappsdeveloper.blogspot.com/2014/02/more-apps-script-apis-and-features.html) | Oct 21, 2014 | Service no longer functions. |
| DeckPanel | [Apr 15, 2013](https://developers.google.com/apps-script/release_notes#april_15_2013) | Apr 10, 2014 | Widget no longer functions. |
| DecoratedPopupPanel | | | |
| DockLayoutPanel | | | |
| DockPanel | | | |
| StackLayoutPanel | | | |
| TabLayoutPanel | | | |
| Old XML service | [Jul 9, 2013](http://googleappsdeveloper.blogspot.com/2013/07/xml-changes-in-apps-script.html) | | Service no longer appears in autocomplete, although existing scripts should still function. |
| SOAP service | | | |
| E4X support | | | Feature is no longer supported, although existing scripts should still function. |
| Hyperlink | [Mar 13, 2013](http://googleappsdeveloper.blogspot.com/2013/03/retiring-a-few-apps-script-components.html) | Sep 16, 2013 | Widget no longer functions. |
| Inline Hyperlink | | | |
| LayoutPanel | | | |
| RichTextArea | | | |
| GUI Builder | | Oct 2, 2013 | No access to GUI Builder, though existing components should function. |

Source: https://developers.google.com/apps-script/guides/support/sunset
