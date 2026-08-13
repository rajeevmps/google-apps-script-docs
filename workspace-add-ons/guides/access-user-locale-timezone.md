# Get user locale and timezone

Google Workspace add-ons can access the locale and timezone of its user and use that information to customize its interface and behavior. Configure your add-on's [manifest](/workspace/add-ons/concepts/workspace-manifests) to permit your add-on to access this information.

## Configure the add-on manifest

Configure your add-on to access user locale and timezone information with the following steps:

1.  In your add-on's [manifest](/workspace/add-ons/concepts/workspace-manifests) file, set the `addOns.common.useLocaleFromApp` field to `true`.
2.  If it isn't present already, add the following explicit scope in the manifest's `oauthScopes` list: `https://www.googleapis.com/auth/script.locale`

If you added a scope to the add-on's `oauthScope` list, users must [re-authorize](/workspace/add-ons/how-tos/authorizing-addons) the add-on the next time it is opened.

**Note:** If your add-on previously used the [Calendar API](/workspace/calendar/api/v3/reference/settings), the Apps Script [Calendar service](/apps-script/reference/calendar), or another service to access the user's locale and timezone, consider whether that service is still needed by your add-on. If not, remove any scopes that service requires from your manifest. Always limit your scope list to only those services that your add-on needs.

## Get locale and timezone information

[Event objects](/workspace/add-ons/concepts/event-objects) carry user locale information when properly configured. The following fields appear in the [`commonEventObject`](/workspace/add-ons/concepts/event-objects#common_event_object) substructure of the event object:

*   `commonEventObject.userLocale`—The user's language and country/region identifier. For example, `en-US`.
*   `commonEventObject.timeZone.offset`—The user's timezone offset, in milliseconds, from Coordinated Universal Time (UTC).
*   `commonEventObject.timeZone.id`—The user's timezone identifier. For example, `America/New_York`.
*   `commonEventObject.timeZone`—The user's timezone ID and offset.

See [Event objects](/workspace/add-ons/concepts/event-objects) for more details.

[Event objects](/workspace/add-ons/concepts/event-objects) are passed to [action callback functions](/workspace/add-ons/concepts/actions#callback_functions) as the user interacts with your add-on, and to homepage and contextual trigger functions. Each callback or trigger function can read the locale and timezone information from the event object and use it as necessary. For example, a callback function that is [navigating to a new card](/workspace/add-ons/how-tos/navigation#navigation_methods) could refer to the locale string when deciding what text to add to the card.
