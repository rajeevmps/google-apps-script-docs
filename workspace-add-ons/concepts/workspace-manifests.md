# Manifests for Google Workspace add-ons

An add-on uses a *manifest* file to configure certain details about the app and its operation.

This documentation covers the details of configuring a manifest for a Google Workspace Add-on.

## Manifest structure for Google Workspace add-ons

Google Workspace add-ons use the manifest file to define several aspects of appearance and behavior.

Manifest properties for Google Workspace add-ons are organized under the `addOns` section.

- For information about Google Apps Script manifest files, refer to [Manifest structure](/apps-script/manifest).
- For information about manifest files for add-ons built with HTTP endpoints, refer to [`projects.deployments`](/workspace/add-ons/reference/rest/v1/projects.deployments).

### Manifests for Google Chat

If your Google Workspace add-on extends Google Chat, [configure a Google Chat app](/workspace/add-ons/chat/configure) by enabling and configuring the Google Chat API in the Google Cloud console.

Common manifest configuration settings (including `addons.common`) are ignored in Chat. Use the Chat API to configure the following Chat settings:

- The name, logo, and description of the Chat app for the Chat UI.
- [Chat app triggers](/workspace/add-ons/chat/build#triggers).

If you built the add-on in Apps Script, add or update the following objects in your manifest:

- [`addons.chat`](/apps-script/manifest/addons#AddOns.FIELDS.chat) (Required)
- [`oauthScopes`](/apps-script/manifest#Manifest.FIELDS.oauthScopes) (Required if your Google Chat app uses OAuth)

To configure Chat settings for an add-on, see [Configure a Google Chat app](/workspace/add-ons/chat/configure).

### Sample Google Workspace add-on manifest configuration

The following samples show the portion of a manifest that defines a Google Workspace add-on, including these aspects:

- `addOns.common` defines the name, logo, colors, and other general settings for the add-on.
- The manifest defines a common homepage, but also defines Google Calendar, Google Drive, Google Docs, Google Sheets, and Google Slides-specific homepages. Gmail uses the default homepage.
- The sample manifest settings enable the following:
  - Calendar `eventOpen` and `eventUpdated` triggers.
  - (Apps Script only) Two Calendar [conference solutions](/workspace/add-ons/calendar/conferencing/overview).
  - Two universal actions.
  - A Drive `onItemsSelectedTrigger`.
  - A Gmail compose action and contextual trigger.
  - A Docs `linkPreviewTriggers` object. See [Preview links with smart chips](/workspace/add-ons/editors/gsao/preview-links).
  - A Docs `createActionTriggers` object. See [Create third-party resources from the @ menu](/workspace/add-ons/guides/create-insert-resource-smart-chip).
  - File-specific interfaces for Docs, Sheets, and Slides.
  - A Google Meet `sidePanelUri` and `addOnOrigins` option.
  - (HTTP only) Two [`HttpOptions`](/workspace/add-ons/reference/rest/v1/projects.deployments#httpoptions) for sending an authorization header and supporting granular consent.

- The `oauthScopes` field sets project's authorization scopes.
- (Apps Script only) The `urlFetchWhitelist` ensures fetched endpoints match specified HTTPS URL prefixes. See Allowlist URLs.

The links in the samples redirect to field descriptions in the manifest reference for [Apps Script](/apps-script/manifest/addons) and [HTTP](/workspace/add-ons/reference/rest/v1/projects.deployments) Google Workspace add-ons.

Manifests include other components. Fields under `addOns` relate directly to Google Workspace add-ons. This example shows only a portion of a full manifest file and isn't functional on its own.

### Apps Script

```
{
  "addOns": {
    "calendar": {
      "createSettingsUrlFunction": "getConferenceSettingsPageUrl",
      "conferenceSolution": [{
        "id": "my-video-conf",
        "logoUrl": "https://lh3.googleusercontent.com/...",
        "name": "My Video Conference",
        "onCreateFunction": "onCreateMyVideoConference"
      }, {
        "id": "my-streamed-conf",
        "logoUrl": "https://lh3.googleusercontent.com/...",
        "name": "My Streamed Conference",
        "onCreateFunction": "onCreateMyStreamedConference"
      }],
      "currentEventAccess": "READ_WRITE",
      "eventOpenTrigger": {
        "runFunction": "onCalendarEventOpen"
      },
      "eventUpdateTrigger": {
        "runFunction": "onCalendarEventUpdate"
      },
      "eventAttachmentTrigger": {
        "label": "My Event Attachment",
        "runFunction": "onCalendarEventAddAttachment"
      },
      "homepageTrigger": {
        "runFunction": "onCalendarHomePageOpen",
        "enabled": true
      }
    },
    "common": {
      "homepageTrigger": {
        "runFunction": "onDefaultHomePageOpen",
        "enabled": true
      },
      "layoutProperties": {
        "primaryColor": "#ff392b",
        "secondaryColor": "#d68617"
      },
      "logoUrl": "https://ssl.gstatic.com/docs/script/images/logo/script-64.png",
      "name": "Demo Google Workspace add-on",
      "openLinkUrlPrefixes": [
        "https://mail.google.com/",
        "https://script.google.com/a/google.com/d/",
        "https://drive.google.com/a/google.com/file/d/",
        "https://www.example.com/"
      ],
      "universalActions": [{
        "label": "Open settings",
        "runFunction": "getSettingsCard"
      }, {
        "label": "Open Help URL",
        "openLink": "https://www.example.com/help"
      }],
      "useLocaleFromApp": true
    },
    "drive": {
      "homepageTrigger": {
        "runFunction": "onDriveHomePageOpen",
        "enabled": true
      },
      "onItemsSelectedTrigger": {
        "runFunction": "onDriveItemsSelected"
      }
    },
    "gmail": {
      "composeTrigger": {
        "selectActions": [
          {
            "text": "Add images to email",
            "runFunction": "getInsertImageComposeCards"
          }
        ],
        "draftAccess": "METADATA"
      },
      "contextualTriggers": [
        {
          "unconditional": {},
          "onTriggerFunction": "onGmailMessageOpen"
        }
      ]
    },
    "docs": {
      "homepageTrigger": {
        "runFunction": "onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "onFileScopeGrantedEditors"
      },
      "linkPreviewTriggers": [
        {
        "runFunction": "onLinkPreview",
        "patterns": [
            {
              "hostPattern": "example.com",
              "pathPrefix": "example-path"
            }
        ],
        "labelText": "Link preview",
        "localizedLabelText": {
          "es": "Link preview localized in Spanish"
        },
        "logoUrl": "https://www.example.com/images/smart-chip-icon.png"
        }
      ],
      "createActionTriggers": [
        {
          "id": "exampleId",
          "labelText": "Example label text",
          "localizedLabelText": {
            "es": "Label text localized in Spanish"
          },
          "runFunction": "exampleFunction",
          "logoUrl": "https://www.example.com/images/case.png"
        }
      ]
    },
    "sheets": {
      "homepageTrigger": {
        "runFunction": "onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "onFileScopeGrantedEditors"
      }
    },
    "slides": {
      "homepageTrigger": {
        "runFunction": "onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "onFileScopeGrantedEditors"
      }
    },
    "meet": {
      "homepageTrigger",
      "Web": [
        {
          "sidePanelUrl": "https://myownpersonaldomain.com/sidePanelUrl",
          "supportsScreenSharing": true,
          "addOnOrigins": [
            "https://www.myownpersonaldomain.com",
            "https://www.myownpersonaldomain.com:443"
          ],
          "logoUrl": "https://myownpersonaldomain.com/logoUrl",
          "darkModeLogoUrl": "https://myownpersonaldomain.com/darkModeLogoUrl"
        }
    },
  },
  "oauthScopes": [
    "https://www.googleapis.com/auth/calendar.addons.execute",
    "https://www.googleapis.com/auth/calendar.addons.current.event.read",
    "https://www.googleapis.com/auth/calendar.addons.current.event.write",
    "https://www.googleapis.com/auth/drive.addons.metadata.readonly",
    "https://www.googleapis.com/auth/gmail.addons.current.action.compose",
    "https://www.googleapis.com/auth/gmail.addons.current.message.metadata",
    "https://www.googleapis.com/auth/userinfo.email",
    "https://www.googleapis.com/auth/script.external_request",
    "https://www.googleapis.com/auth/script.locale",
    "https://www.googleapis.com/auth/script.scriptapp",
    "https://www.googleapis.com/auth/drive.file",
    "https://www.googleapis.com/auth/documents.currentonly",
    "https://www.googleapis.com/auth/spreadsheets.currentonly",
    "https://www.googleapis.com/auth/presentations.currentonly",
    "https://www.googleapis.com/auth/workspace.linkpreview"
  ],
  "urlFetchWhitelist": [
    "https://www.example.com/myendpoint/"
  ]
}
```

### HTTP

```
{
  "addOns": {
    "calendar": {
      "currentEventAccess": "READ_WRITE",
      "eventOpenTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onCalendarEventOpen"
      },
      "eventUpdateTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onCalendarEventUpdate"
      },
      "eventAttachmentTrigger": {
        "label": "My Event Attachment",
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onCalendarEventAddAttachment"
      },
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onCalendarHomePageOpen",
        "enabled": true
      }
    },
    "common": {
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onDefaultHomePageOpen",
        "enabled": true
      },
      "layoutProperties": {
        "primaryColor": "#ff392b",
        "secondaryColor": "#d68617"
      },
      "logoUrl": "https://ssl.gstatic.com/docs/script/images/logo/script-64.png",
      "name": "Demo Google Workspace add-on",
      "openLinkUrlPrefixes": [
        "https://mail.google.com/",
        "https://script.google.com/a/google.com/d/",
        "https://drive.google.com/a/google.com/file/d/",
        "https://www.example.com/"
      ],
      "universalActions": [{
        "label": "Open settings",
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=getSettingsCard"
      }, {
        "label": "Open Help URL",
        "openLink": "https://www.example.com/help"
      }],
      "useLocaleFromApp": true
    },
    "drive": {
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onDriveHomePageOpen",
        "enabled": true
      },
      "onItemsSelectedTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onDriveItemsSelected"
      }
    },
    "gmail": {
      "composeTrigger": {
        "actions": [
          {
            "label": "Add images to email",
            "runFunction": "https://myownpersonaldomain.com/mypage?trigger=getInsertImageComposeCards"
          }
        ],
        "draftAccess": "METADATA"
      },
      "contextualTriggers": [
        {
          "unconditional": {},
          "onTriggerFunction": "https://myownpersonaldomain.com/mypage?trigger=onGmailMessageOpen"
        }
      ]
    },
    "docs": {
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onFileScopeGrantedEditors"
      },
      "linkPreviewTriggers": [
        {
          "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onLinkPreview",
          "patterns": [
              {
                "hostPattern": "example.com",
                "pathPrefix": "example-path"
              }
          ],
          "labelText": "Link preview",
          "localizedLabelText": {
            "es": "Link preview localized in Spanish"
          },
          "logoUrl": "https://www.example.com/images/smart-chip-icon.png"
        }
      ],
      "createActionTriggers": [
        {
          "id": "exampleId",
          "labelText": "Example label text",
          "localizedLabelText": {
            "es": "Label text localized in Spanish"
          },
          "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onCreateAction",
          "logoUrl": "https://www.example.com/images/case.png"
        }
      ]
    },
    "sheets": {
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onFileScopeGrantedEditors"
      }
    },
    "slides": {
      "homepageTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onEditorsHomepage"
      },
      "onFileScopeGrantedTrigger": {
        "runFunction": "https://myownpersonaldomain.com/mypage?trigger=onFileScopeGrantedEditors"
      }
    },
    "meet": {
      "homepageTrigger",
      "Web": [
        {
          "sidePanelUrl": "https://myownpersonaldomain.com/sidePanelUrl",
          "supportsScreenSharing": true,
          "addOnOrigins": [
            "https://www.myownpersonaldomain.com",
            "https://www.myownpersonaldomain.com:443"
          ],
          "logoUrl": "https://myownpersonaldomain.com/meetWebLogoUrl",
          "darkModeLogoUrl": "https://myownpersonaldomain.com/darkModeLogoUrl"
        }
      ]
    },
    "httpOptions": {
      "authorizationHeader": "SYSTEM_ID_TOKEN",
      "granularOauthPermissionSupport": "OPT_IN"
    }
  },
  "oauthScopes": [
    "https://www.googleapis.com/auth/calendar.addons.execute",
    "https://www.googleapis.com/auth/calendar.addons.current.event.read",
    "https://www.googleapis.com/auth/calendar.addons.current.event.write",
    "https://www.googleapis.com/auth/drive.addons.metadata.readonly",
    "https://www.googleapis.com/auth/gmail.addons.current.action.compose",
    "https://www.googleapis.com/auth/gmail.addons.current.message.metadata",
    "https://www.googleapis.com/auth/userinfo.email",
    "https://www.googleapis.com/auth/script.external_request",
    "https://www.googleapis.com/auth/script.locale",
    "https://www.googleapis.com/auth/script.scriptapp",
    "https://www.googleapis.com/auth/drive.file",
    "https://www.googleapis.com/auth/documents.currentonly",
    "https://www.googleapis.com/auth/spreadsheets.currentonly",
    "https://www.googleapis.com/auth/presentations.currentonly",
    "https://www.googleapis.com/auth/workspace.linkpreview"
  ]
}
```

## Allowlist URLs

You use allowlists to designate specific URLs that are pre-approved for access by your script or add-on. Allowlists help protect user data; when you define an allowlist, script projects can't access URLs that have not been added to the allowlist.

This field is optional when you install a test deployment, but is required when you create a versioned deployment.

You use allowlists when your script or add-on performs the following actions:

- Retrieves or fetches information from an external location (such as HTTPS endpoints) using the Apps Script [`UrlFetch`](/apps-script/reference/url-fetch) service. To allowlist URLs for fetching, include the [`urlFetchWhitelist`](/apps-script/manifest#Manifest.FIELDS.urlFetchWhitelist) field in your manifest file.
- Opens or displays a URL in response to a user action (Required for Google Workspace add-ons that open or display URLs that are external to Google). To allowlist URLs for opening, include the [`addOns.common.openLinkUrlPrefixes`](/apps-script/manifest/addons#Common.FIELDS.openLinkUrlPrefixes) field in your manifest file.

> **Note:** *Whitelist*, as used in [`urlFetchWhitelist`](/apps-script/manifest#Manifest.FIELDS.urlFetchWhitelist), is a deprecated term that is synonymous with and replaced by *allowlist*. For more information, see [Writing inclusive documentation](https://developers.google.com/style/inclusive-documentation).

### Adding prefixes to your allowlist

When you specify allowlists in your manifest file (by including either the `addOns.common.openLinkUrlPrefixes` or `urlFetchWhitelist` field), you must include a list of URL prefixes. The prefixes you add to the manifest must satisfy the following requirements:

- Each prefix must be a valid URL.
- Each prefix must use `https://`, not `http://`.
- Each prefix must have a full domain.
- Each prefix must have a non-empty path. For example, `https://www.google.com/` is valid but `https://www.google.com` is not.
- You can use wildcards to match URL subdomain prefixes.
- A single `*` wildcard can be used in the [`addOns.common.openLinkUrlPrefixes`](/apps-script/manifest/addons#Common.FIELDS.openLinkUrlPrefixes) field to match all links, but this is not recommended as it can expose a user's data to risk and can prolong the [add-on review](/workspace/add-ons/concepts/gsuite-addon-review) process. Only use a wildcard if your add-on functionality requires it.

When determining if a URL matches a prefix in the allowlist, the following rules apply:

- Path matching is case-sensitive.
- If the prefix is identical to the URL, it is a match.
- If the URL is the same or a child of the prefix, it is a match.

For example, the prefix `https://example.com/foo` matches the following URLs:

- `https://example.com/foo`
- `https://example.com/foo/`
- `https://example.com/foo/bar`
- `https://example.com/foo?bar`
- `https://example.com/foo#bar`

### Using wildcards

You can use a single wildcard character (`*`) to match a subdomain for both the [`urlFetchWhitelist`](/apps-script/manifest#Manifest.FIELDS.urlFetchWhitelist) and [`addOns.common.openLinkUrlPrefixes`](/apps-script/manifest/addons#Common.FIELDS.openLinkUrlPrefixes) fields. You can't use more than one wildcard to match multiple subdomains, and the wildcard must represent the leading prefix of the URL.

For example, the prefix `https://*.example.com/foo` matches the following URLs:

- `https://subdomain.example.com/foo`
- `https://any.number.of.subdomains.example.com/foo`

The prefix `https://*.example.com/foo` *doesn't* match the following URLs:

- `https://subdomain.example.com/bar` (suffix mismatch)
- `https://example.com/foo` (at least one subdomain must be present)

Some of the prefix rules are enforced when you try to save your manifest. For example, the following prefixes cause an error if they are present in your manifest when you attempt to save:

- `https://*.*.example.com/foo` (multiple wildcards are forbidden)
- `https://subdomain.*.example.com/foo` (wildcards must be used as a leading prefix)
