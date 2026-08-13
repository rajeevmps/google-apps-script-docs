# Event objects

This page outlines the structure of Google Workspace add-ons event objects.

Event objects are JSON structures that are automatically constructed and passed as parameters to trigger or callback functions when a user interacts with an add-on. Event objects carry client-side information about the host app and the current context to the add-on's server-side callback function.

Google Workspace add-ons use event objects in the following places:

- [**Homepage triggers**](/workspace/add-ons/concepts/homepages#homepage_configuration). Every `homepageTrigger` function you define is automatically passed an event object when the homepage trigger function fires. You can use this object in your homepage trigger function to identify the active host app, the client's platform, the user locale, and other information. The event objects created when homepage triggers fire don't contain all the fields included in the other cases; fields pertaining to widgets and contextual information are omitted.
- [**Contextual triggers**](/workspace/add-ons/guides/glossary#contextual_triggering). Each host application provides a different set of contextual triggers that fire when the user enters a specific context: When a contextual trigger fires, the host application calls the corresponding `runFunction` listed in the add-on manifest, passing it an event object as a parameter. The event objects created when contextual triggers fire contain all the fields included in homepage trigger event objects, plus fields containing contextual information.
  - When the user:
    - [opens a message](/workspace/add-ons/gmail/extending-message-ui#contextual_triggers)
    - [composes a message](/workspace/add-ons/gmail/extending-compose-ui#compose_trigger_function).
    - [opens an event](/workspace/add-ons/calendar/building-calendar-interfaces#extending_the_event_interface).

  - Google Drive provides a contextual trigger when a user [selects Drive files](/workspace/add-ons/drive/building-drive-interfaces#drive_contextual_interface_for_items_selected).

- **[Widget actions](/workspace/add-ons/concepts/actions)**. Event objects provide [widget](/workspace/add-ons/concepts/widgets) interactivity, using the same [action model](/workspace/add-ons/concepts/actions) that Gmail add-ons use. Google Workspace add-ons use the same widget handler functions, [`Action`](/apps-script/reference/card-service/action) objects, and action responses. In Google Workspace add-ons, [action event objects](/workspace/add-ons/concepts/actions#action_event_objects) include more information a callback function can act on. The event objects created from widget actions contain all the fields included in contextual trigger event objects, plus fields containing widget information.
- **[Preview link triggers](/workspace/add-ons/editors/gsao/preview-links)**. In Google Docs, Sheets, and Slides, you can configure link previews for third-party services based on specific URL patterns. When users interact with a link that meets the pattern, the [`linkPreviewTriggers`](/apps-script/manifest/editor-addons#linkpreviewtriggers) fires and an event object containing the link is passed to the trigger's callback function. Your add-on can use this event object to construct a smart chip and card that surface information about the link within the host application. You can also build widget actions so users can interact with the preview card and its contents.
- **[Google Chat app triggers](/workspace/add-ons/chat/build#triggers)**. In Google Chat, your add-on appears to users as a Chat app, and users can interact with it by adding it to spaces, sending messages, using slash commands, and more. To build interactive features, you set up and use various Chat app triggers. Each trigger sends a different event object payload that helps you process or respond to each type of interaction.

## Event object structure

The following table describes the top-level structure of Google Workspace add-ons event objects. The structure includes a `commonEventObject` top-level field for host-independent information. Each event object can also have one of the following host-specific top-level fields, determined by the active host app: `gmailEventObject`, `calendarEventObject`, or `driveEventObject`.

For backward compatibility, Google Workspace add-ons event objects include the original fields used in [Gmail add-on action event objects](/workspace/add-ons/concepts/actions#action_event_objects). These fields are under "Original Gmail add-on fields" and aren't part of `commonEventObject`.

The original Gmail add-on fields are deprecated. When developing or migrating Google Workspace add-on, use the newer event object structure instead. These fields might be removed in a future update.

| Event object |  |
| --- | --- |
| `eventObject.commonEventObject` | `Common fields object` An object containing information common to all event objects, regardless of the host application. |
| `eventObject.calendar` | `Calendar event object ` **Only present if the calling host is Google Calendar**. An object containing calendar and event information. |
| `eventObject.chat` | `Chat event object ` **Only present if the calling host is Google Chat**. An object containing Chat information. |
| `eventObject.drive` | `Drive event object ` **Only present if the calling host is Google Drive**. An object containing Drive information. |
| `eventObject.gmail` | `Gmail event object ` **Only present if the calling host is Gmail**. An object containing Gmail information. |
| `eventObject.docs` | `Docs event object ` **Only present if the calling host is Google Docs**. An object containing Docs information. |
| `eventObject.sheets` | `Sheets event object ` **Only present if the calling host is Google Sheets**. An object containing Sheets information. |
| `eventObject.slides` | `Slides event object ` **Only present if the calling host is Google Slides**. An object containing Slides information. |
| Original Gmail add-on fields |  |
| `eventObject.messageMetadata.accessToken` | `string` **Deprecated.** An access token. You can use this to turn on access to user data using temporary Gmail add-on scopes. For Google Workspace add-ons, find this information in the `eventObject.gmail.accessToken` field. |
| `eventObject.messageMetadata.messageId` | `string` **Deprecated.** The message ID of the thread open in the Gmail UI. For Google Workspace add-ons, find this information in the `eventObject.gmail.messageId` field. |
| `eventObject.clientPlatform` | `string` **Deprecated.** Indicates where the event originates (web, iOS, or Android). For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.platform` field. |
| `eventObject.formInput` | `object` **Deprecated.** A map of the current values of all form widgets in the card, restricted to one value per widget. The keys are the string IDs associated with the widgets, and the values are strings. The event object provides `formInput` as a convenience for when you need to read data from multiple widgets with expected singular values, such as text inputs and switches. For multi-valued widgets such as checkboxes, read each value from `formInputs` instead. Date and time picker widget values can't be read from this field. Get those picker values from `commonEventObject.formInputs` instead. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.formInputs` field instead; widgets with single values are represented as arrays with a single element. |
| `eventObject.formInputs` | `object` **Deprecated.** A map of current values of widgets in the card, presented as lists of strings. The keys are the string IDs associated with the widget. For single-valued widgets, the value is presented in a single-element array. For multi-valued widgets such as checkbox groups, all the values are presented in a list. Date and time picker widget values can't be read from this field. Get those picker values from `commonEventObject.formInputs` instead. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.formInputs` field. |
| `eventObject.parameters` | `object` **Deprecated.** A map of any additional parameters you supply to the [`Action`](/apps-script/reference/card-service/action) using [`Action.setParameters`](/apps-script/reference/card-service/action#setParameters(Object)). The map keys and values are strings. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.parameters` field. |
| `eventObject.userCountry` | `string` **Deprecated and disabled by default**. The two-letter code indicating the user's country or region. It can also be a numeric [UN M49](https://en.wikipedia.org/wiki/UN_M49) country code. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.userLocale` field. |
| `eventObject.userLocale` | `string` **Deprecated and disabled by default**. The two-letter [ISO 639](https://en.wikipedia.org/wiki/ISO_639_macrolanguage) code indicating the user's language. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.userLocale` field. |
| `eventObject.userTimezone.id` | `string` **Deprecated and disabled by default**. The [timezone identifier](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) of the user's timezone. Examples include: `America/New_York`, `Europe/Vienna`, and `Asia/Seoul`. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.timeZone.id` field. |
| `eventObject.userTimezone.offset` | `string` **Deprecated and disabled by default**. The [time offset from Coordinated Universal Time (UTC)](https://en.wikipedia.org/wiki/ISO_8601#Time_offsets_from_UTC) of the user's timezone, measured in milliseconds. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. For Google Workspace add-ons, find this information in the `eventObject.commonEventObject.timeZone.offset` field. |

## Common event object

The common event object is the portion of the overall event object that carries general, host-independent information to the add-on from the user's client. This information includes details such as the user's locale, host app, and platform.

In addition to homepage and contextual triggers, add-ons construct and pass event objects to [action callback functions](/workspace/add-ons/concepts/actions#callback_functions) when the user interacts with widgets. Your add-on's callback function can query the common event object to determine the contents of open widgets in the user's client. For example, your add-on can locate the text a user has entered into a [`TextInput`](/apps-script/reference/card-service/text-input) widget in the `eventObject.commentEventObject.formInputs` object.

| Common event object fields |  |
| --- | --- |
| `commonEventObject.platform` | `string` Indicates where the event originates (`WEB`, `IOS`, or `ANDROID`). |
| `commonEventObject.formInputs` | `object` A map containing the current values of the widgets in the displayed card. The map keys are the string IDs assigned with each widget. The structure of the map value object is dependent on the widget type: Examples are formatted for Apps Script's V8 runtime. If you're using Rhino runtime, you must add `[""]` after the value. For example, instead of `e.commonEventObject.formInputs.employeeName.stringInputs.value[0]`, format the event object as `e.commonEventObject.formInputs.employeeName[""].stringInputs.value[0]`. To learn more about runtimes in Apps Script, see the [V8 Runtime Overview](https://developers.google.com/apps-script/guides/v8-runtime). Single-valued widgets (for example, a text box): a list of strings (only one element). **Example**: for a text input widget with `employeeName` as its ID, access the text input value with: `e.commonEventObject.formInputs.employeeName.stringInputs.value[0]` Multi-valued widgets (for example, checkbox groups): a list of strings. **Example**: for a multi-value widget with `participants` as its ID, access the value array with: `e.commonEventObject.formInputs.participants.stringInputs.value`. `A date-time picker`: a `DateTimeInput object`. **Example**: For a picker with an ID of `myDTPicker`, access the `DateTimeInput` object using `e.commonEventObject.formInputs.myDTPicker.dateTimeInput`. `A date-only picker`: a `DateInput object`. **Example**: For a picker with an ID of `myDatePicker`, access the `DateInput ` object using `e.commonEventObject.formInputs.myDatePicker.dateInput`. `A time-only picker`: a `TimeInput object`. **Example**: For a picker with an ID of `myTimePicker`, access the `TimeInput` object using `e.commonEventObject.formInputs.myTimePicker.timeInput`. |
| `commonEventObject.hostApp` | `string` Indicates the host app the add-on is active in when the event object is generated. Possible values include the following: `GMAIL` `CALENDAR` `DRIVE` `DOCS` `SHEETS` `SLIDES` |
| `commonEventObject.parameters` | `object` Any additional parameters you supply to an action using `actionParameters` or ` Action.setParameters`. **Developer Preview:** For [add-ons that extend Google Chat](/workspace/add-ons/chat), to suggest items based on what the users type in multiselect menus, use the value of the `"autocomplete_widget_query"` key (`event.commonEventObject.parameters["autocomplete_widget_query"]`). You can use this value to query a database and suggest selectable items to users as they type. For details, see [Collect and process information from Google Chat users](/workspace/add-ons/chat/collect-information). |
| `commonEventObject.userLocale` | `string` **Disabled by default**. The user's language and country/region identifier in the format of [ISO 639](https://wikipedia.org/wiki/ISO_639_macrolanguage) language code-[ISO 3166](https://wikipedia.org/wiki/ISO_3166) country/region code. For example, `en-US`. To turn on this field, you must set `addOns.common.useLocaleFromApp` to `true` in your add-on's manifest. Your add-on's scope list must also include `https://www.googleapis.com/auth/script.locale`. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. |
| `commonEventObject.timeZone` | `string` **Disabled by default**. The timezone ID and offset. To turn on this field, you must set `addOns.common.useLocaleFromApp` to `true` in your add-on's manifest. Your add-on's scope list must also include `https://www.googleapis.com/auth/script.locale`. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. |
| `commonEventObject.timeZone.id` | `string` The [timezone identifier](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) of the user's timezone. Examples include: `America/New_York`, `Europe/Vienna`, and `Asia/Seoul`. To turn on this field, you must set `addOns.common.useLocaleFromApp` to `true` in your add-on's manifest. Your add-on's scope list must also include `https://www.googleapis.com/auth/script.locale`. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. |
| `commonEventObject.timeZone.offset` | `string` The [time offset from Coordinated Universal Time (UTC)](https://en.wikipedia.org/wiki/ISO_8601#Time_offsets_from_UTC) of the user's timezone, measured in milliseconds. See [Accessing user locale and timezone](/workspace/add-ons/how-tos/access-user-locale) for more details. |

### Date-time picker form inputs

[Action callback functions](/workspace/add-ons/concepts/actions#callback_functions) can receive current widget values in the `commonEventObject.formInputs` field. This includes the user's selected date or time values in date or time picker widgets. The information structure differs depending on whether the widget was configured as a date-time picker, a date-only picker, or a time-only picker. The structural differences are described in the following table:

| DateTimeInput object |  |
| --- | --- |
| `dateTimeInput.hasDate` | `boolean` `true` if the input date time includes a date; if `false` only a time is included. |
| `dateTimeInput.hasTime` | `boolean` `true` if the input date time includes a time; if `false` only a date is included. |
| `dateTimeInput.msSinceEpoch` | `string` The time selected by the user, in milliseconds since epoch (00:00:00 UTC on 1 January 1970). |
| DateInput object |  |
| `dateInput.msSinceEpoch` | `string` The time selected by the user, in milliseconds since epoch (00:00:00 UTC on 1 January 1970). |
| TimeInput object |  |
| `timeInput.hours` | `number` The hour number selected by the user. |
| `timeInput.minutes` | `number` The minute number selected by the user. |

## Chat event object

The Chat event object is the portion of the overall event object that carries information about a user's interactions with a Chat app. It's only present in an event object if the [add-on extends Google Chat](/workspace/add-ons/chat).

| Chat |  |
| --- | --- |
| `chat.user` | `object (User) ` The Chat user that interacted with the Chat app. |
| `chat.space` | `object (Space)` The Chat space where a user interacted with the Chat app. |
| `chat.eventTime` | `string (Timestamp format)` The time when the interaction occurred. |
| Union field `payload`.`payload` can be only one of the following: |  |
| `chat.messagePayload` | `object (MessagePayload)` The payload that Chat apps receive from a **Message** trigger. |
| `chat.addedToSpacePayload` | `object (AddedToSpacePayload)` The payload that Chat apps receive from an **Added to space** trigger. |
| `chat.removedFromSpacePayload` | `object (RemovedFromSpacePayload)` The payload that Chat apps receive from a **Removed from space** trigger. |
| `chat.buttonClickedPayload` | `object (ButtonClickedPayload)` The payload that Chat apps receive when users click a button from a message or card. If a user clicks a button to submit information, the `commonEventObject.formInputs` object contains the values collected from the user. For details, see [Collect information from Google Chat users](/workspace/add-ons/chat/collect-information). |
| `chat.widgetUpdatedPayload` | `object (WidgetUpdatedPayload)` The payload that Chat apps receive when users type text into the multiselect menu of a [`selectionInput`](/workspace/add-ons/reference/rpc/google.apps.card.v1#google.apps.card.v1.SelectionInput) widget. Chat apps can use this event object to populate suggested items from a dynamic data source. For example, to populate support cases from an external data source, a Chat app can query the data source based on what the user types into the menu, and then return matching support cases as selectable items. The `CommonEventObject.parameters['autocomplete_widget_query']` object contains the string value that the user types into the menu. |
| `chat.appCommandPayload` | `object (AppCommandPayload)` The payload that Chat apps receive when a user uses a command from the Chat app. |

### Payload

Depending on the type of Chat app interaction, the event contains a payload with one or more Chat API resources.

Message payload MessagePayload `chat.messagePayload.message` `object (Message) `  
The Chat message that triggered the event. `chat.messagePayload.space` `object (Space)`   
The Chat space in which a user sent the message that invoked the Chat app. `chat.messagePayload.configCompleteRedirectUri` `string`  
 The URL the Chat app should redirect the user to after they complete an authorization or configuration flow outside of Google Chat. For more information, see [Connect your Google Workspace add-on to a third-party service](/workspace/add-ons/guides/connect-third-party-service).

Added to space payload AddedToSpacePayload `chat.addedToSpacePayload.space` `object (Space)`   
The Chat space to which the user added or installed the Chat app. When administrators install Chat apps, the `space.adminInstalled` field is set to `true`. `chat.addedToSpacePayload.interactionAdd` `boolean`  
 Whether a user adds the Chat app to a space using a message. For example, @mentions the Chat app or uses a command. If `true`, Chat sends another event object with a `messagePayload` that contains information about the message. `chat.addedToSpacePayload.configCompleteRedirectUri` `string`  
 The URL the Chat app should redirect the user to after they complete an authorization or configuration flow outside of Google Chat. For more information, see [Connect your Google Workspace add-on to a third-party service](/workspace/add-ons/guides/connect-third-party-service).

Removed from space payload RemovedFromSpacePayload `chat.removedFromSpacePayload.space` `object (Space)`   
The Chat space from which the user removed or uninstalled the Chat app. When administrators uninstall Chat apps, the `space.adminInstalled` field is set to `false`.

Button clicked payload ButtonClickedPayload `chat.buttonClickedPayload.message` `object (Message) `  
The Chat message that contains the button that a user clicked. `chat.buttonClickedPayload.space` `object (Space)`   
The Chat space where the user clicked a button from a Chat app message. `chat.buttonClickedPayload.isDialogEvent` `boolean`  
 Whether the user clicked the button to interact with a [dialog](/workspace/add-ons/chat/dialogs). `chat.buttonClickedPayload.dialogEventType` `enum (DialogEventType)`  
 If `isDialogEvent` is `true`, the type of interaction in a dialog. Enum `DialogEventType`.Value of `dialogEventType` can be only one of the following: `TYPE_UNSPECIFIED` Default value. Unspecified. `REQUEST_DIALOG` A user requests a dialog. For example, they use a command or click a button from a message. `SUBMIT_DIALOG` A user clicks an interactive element within a dialog. For example, a user fills out information in a dialog and clicks a button to submit the information.

Widget updated payload WidgetUpdatedPayload `chat.widgetUpdatedPayload.space` `object (Space)`   
The Chat space where the interaction occurred.

App command payload AppCommandPayload `chat.appCommandPayload.appCommandMetadata` `object (AppCommandMetadata) `  
Metadata about which command the user used and how they triggered it. `chat.appCommandPayload.space` `object (Space)`   
The Chat space in which a user used the command. `chat.appCommandPayload.thread` `object (Thread)`   
If the interaction occurred in a thread, the Chat thread where the user used the command. `chat.appCommandPayload.message` `object (Message)`   
For slash commands, the message with the slash command. `chat.appCommandPayload.configCompleteRedirectUri` `string`  
 If authorization or configuration is required for the command, a URL to redirect the user to after they complete the process outside of Google Chat. `chat.appCommandPayload.isDialogEvent` `boolean`  
 Whether the command opens a [dialog](/workspace/add-ons/chat/dialogs). `chat.appCommandPayload.dialogEventType` `enum (DialogEventType)`  
 The type of interaction with a dialog. Enum `DialogEventType`.Value of `dialogEventType` can be only one of the following: `TYPE_UNSPECIFIED` Default value. Unspecified. `REQUEST_DIALOG` A user requests a dialog. For example, they use a command or click a button from a message. `SUBMIT_DIALOG` A user clicks an interactive element within a dialog. For example, a user fills out information in a dialog and clicks a button to submit the information. App Command Metadata AppCommandMetadata `chat.appCommandPayload.appCommandMetadata.appCommandId` `string (int64 format)` The command ID. `chat.appCommandPayload.appCommandMetadata.appCommandType` `enum (AppCommandType)`  
 The type of command. Enum `AppCommandType`.Value of `AppCommandType` can be only one of the following: `APP_COMMAND_TYPE_UNSPECIFIED` Default value. Unspecified. `SLASH_COMMAND` A user uses the command by sending a message that begins with a slash `/`. `QUICK_COMMAND` The user selects the command from the Chat menu in the message reply area.

## Calendar event object

The Calendar event object is the portion of the overall event object that carries information about a user's calendar and calendar events. It's only present in an event object if the add-on extends Google Calendar.

The following table lists the fields present in the `calendarEventObject` field of an event object. Fields marked as **User-generated data** are present in the event object if and only if the data is present in the Calendar event and the add-on sets its `addOns.calendar.currentEventAccess` [manifest](/apps-script/manifest/calendar-addons) field to `READ` or `READ_WRITE`.

For many of the fields in this object and its substructures, there is a direct mapping to the [Calendar API Event resource](/workspace/calendar/v3/reference/events#resource-representations) fields of the same name. If the field descriptions differ, the information in the following table is correct.

| Calendar event object |  |
| --- | --- |
| `calendar.attendees[]` | `list of attendee objects` **User-generated data.** A list of the attendees of the calendar event. |
| `calendar.calendarId` | `string` The calendar ID. |
| `calendar.capabilities` | `object` **User-generated data.** An object describing the capabilities of the add-on to view or update event information. |
| `calendar.capabilities.canAddAttendees` | `boolean` **User-generated data.** `true` if the add-on can add new attendees to the event attendee list; `false` otherwise. |
| `calendar.capabilities.canSeeAttendees` | `boolean` **User-generated data.** `true` if the add-on can read the event attendee list; `false` otherwise. |
| `calendar.capabilities.canSeeConferenceData` | `boolean` **User-generated data.** `true` if the add-on can read the event conference data; `false` otherwise. |
| `calendar.capabilities.canSetConferenceData` | `boolean` **User-generated data.** `true` if the add-on can update the event conference data; `false` otherwise. |
| `calendar.capabilities.canAddAttachments` | `boolean` **User-generated data.** `true` if the add-on can add new attachments to the event; `false` otherwise. |
| `calendar.conferenceData` | `Conference data object` **User-generated data.** An object representing any conference data associated with this event, such as Google Meet conference details. |
| `calendar.id` | `string` The event ID. |
| `calendar.organizer` | `object` An object representing the organizer of the event. |
| `calendar.organizer.email` | `string` The event organizer's email address. |
| `calendar.recurringEventId` | `string` The ID of a recurring event. |

### Attendee

Attendee objects carry information about individual attendees to Google Calendar events. This information is present in the event object if and only if the data is present in the Calendar event and the add-on sets its `addOns.calendar.currentEventAccess` [manifest](/apps-script/manifest/calendar-addons) field to `READ` or `READ_WRITE`.

| Attendee object |  |
| --- | --- |
| `attendee.additionalGuests` | `number` The number of additional guests the attendee had indicated they are bringing. Defaults to zero. |
| `attendee.comment` | `string` The attendee's response comment, if any. |
| `attendee.displayName` | `string` The attendee displayed name. |
| `attendee.email` | `string` The attendee email address. |
| `attendee.optional` | `boolean` `true` if the attendance for this attendee is marked as optional; `false` otherwise. |
| `attendee.organizer` | `boolean` `true` if the attendee is an organizer for this event. |
| `attendee.resource` | `boolean` `true` if the attendee represents a resource, such as room or piece of equipment; `false` otherwise. |
| `attendee.responseStatus` | `string` The attendee's response status. Possible values include the following: `accepted`: The attendee has accepted the event invitation. `declined`: The attendee has declined the event invitation. `needsAction`: The attendee has not responded to the event invitation. `tentative`: The attendee has tentatively accepted the event invitation. |
| `attendee.self` | `boolean` `true` if this attendee represents the calendar in which this event appears; `false` otherwise. |

### Conference data

Conference data objects carry information about conferences that are attached to Google Calendar events. These can be Google conference solutions such as Google Meet, or third-party conferences. This information is present in the event object if and only if the data is present in the Calendar event and the add-on sets its `addOns.calendar.currentEventAccess` [manifest](/apps-script/manifest/calendar-addons) field to `READ` or `READ_WRITE`.

| Conference data object |  |
| --- | --- |
| `conferenceData.conferenceId` | `string` The ID of the conference. This ID is meant to allow applications to keep track of conferences; you shouldn't display this ID to users. |
| `conferenceData.conferenceSolution` | `object` An object representing the conference solution, such as Hangouts or Google Meet. |
| `conferenceData.conferenceSolution.iconUri` | `string` The URI for the user-visible icon representing this conference solution. |
| `conferenceData.conferenceSolution.key` | `object` The key which uniquely identifies the conference solution for this event. |
| `conferenceData.conferenceSolution.key.type` | `string` The conference solution type. Possible values include the following: `eventHangout` for Hangouts for consumers (http://hangouts.google.com). `eventNamedHangout` for classic Hangouts for Google Workspace users (http://hangouts.google.com). `hangoutsMeet` for Google Meet (http://meet.google.com). |
| `conferenceData.conferenceSolution.name` | `string` The user-visible name of this conference solution (not localized). |
| `conferenceData.entryPoints[]` | `list of entry point objects` The list of conference entry points, such as URLs or phone numbers. |
| `conferenceData.notes` | `string` Additional notes (such as instructions from the domain administrator or legal notices) about the conference to display to the user. Can contain HTML. The maximum length is 2048 characters. |
| `conferenceData.parameters` | `object` An object containing a map of defined parameter data for use by the add-on. |
| `conferenceData.parameters.addOnParameters` | `object` A map of parameter string keys and values. These keys and values are defined by the add-on developer to attach information to a specific conference for the add-on's use. |

### Entry point

Entry point objects carry information about the established means of accessing a given conference, such as by phone or video. This information is present in the event object if and only if the data is present in the Calendar event and the add-on sets its `addOns.calendar.currentEventAccess` [manifest](/apps-script/manifest/calendar-addons) field to `READ` or `READ_WRITE`.

| Entry point object |  |
| --- | --- |
| `entryPoint.accessCode` | `string` The access code used to access the conference. The maximum length is 128 characters. Conference providers typically only use a subset of {`accessCode`, `meetingCode`, `passcode`, `password`, `pin`} to provide access to conferences. Match and only ever display the fields the conference provider uses. |
| `entryPoint.entryPointFeatures` | `list` Features of the entry point. Currently these features only apply to `phone` entry points: `toll`: The entry point is a toll phone call. `toll_free`: The entry point is a toll-free phone call. |
| `entryPoint.entryPointType` | `string` The type of entry point. Possible values are the following: `more`: Additional conference joining instructions, such as alternate phone numbers. A conference can only have one `more` entry point; if present at least one other type of entry point is also required. `phone`: Join the conference via a phone number. A conference can have zero or more `phone` entry points. Google Calendar only displays the first two phone entry points, after formatting and sorting alphabetically. `sip`: Join the conference over SIP. A conference can have at most one `sip` entry point. `video`: Join the conference over HTTP. A conference can have at most one `video` entry point. |
| `entryPoint.label` | `string` The user-visible label for the entry point URI (not localized). |
| `entryPoint.meetingCode` | `string` The meeting code used to access the conference. The maximum length is 128 characters. Conference providers typically only use a subset of {`accessCode`, `meetingCode`, `passcode`, `password`, `pin`} to provide access to conferences. Match and only ever display the fields the conference provider uses. |
| `entryPoint.passcode` | `string` The passcode used to access the conference. The maximum length is 128 characters. Conference providers typically only use a subset of {`accessCode`, `meetingCode`, `passcode`, `password`, `pin`} to provide access to conferences. Match and only ever display the fields the conference provider uses. |
| `entryPoint.password` | `string` The password used to access the conference. The maximum length is 128 characters. Conference providers typically only use a subset of {`accessCode`, `meetingCode`, `passcode`, `password`, `pin`} to provide access to conferences. Match and only ever display the fields the conference provider uses. |
| `entryPoint.pin` | `string` The PIN used to access the conference. The maximum length is 128 characters. Conference providers typically only use a subset of {`accessCode`, `meetingCode`, `passcode`, `password`, `pin`} to provide access to conferences. Match and only ever display the fields the conference provider uses. |
| `entryPoint.regionCode` | `string` Region code of the phone number. Needed by users if the URI doesn't include a country code. Values are based on the public [CLDR list of region codes](http://cldr.unicode.org/translation/country-names). |
| `entryPoint.uri` | `string` The URI of the entry point. The maximum length is 1300 characters. The formatting depends on the entry point type: `more`: A `http:` or `https:` schema is required. `phone`: A `tel:` schema is required. The URI should include the entire dial sequence (for example, "tel:+12345678900,,,12345678;1234"). `sip`: A `sip:` or `sips:` schema is required. For example "sip:12345678@myprovider.com". `video`: A `http:` or `https:` schema is required. |

## Drive event object

The Drive event object is the portion of the overall event object that carries information about a user's Google Drive and its contents. It's only present in an event object if the add-on extends Google Drive.

| Drive event object |  |
| --- | --- |
| `drive.activeCursorItem` | `Drive item object` The Drive item currently active. |
| `drive.selectedItems[]` | `list of Drive item objects` A list of items (files or folders) selected in Drive. |

### Drive item

Drive item objects carry information about specific Drive items, such as files or folders.

| Drive item object |  |
| --- | --- |
| `item.addonHasFileScopePermission` | `boolean` If `true`, the add-on has requested and received `https://www.googleapis.com/auth/drive.file` scope authorization for this item; otherwise this field is `false`. If the add-on uses a more permissive scope such as `https://www.googleapis.com/auth/drive` or `https://www.googleapis.com/auth/drive.readonly`, this field isn't relevant. Always use the least permissive scopes possible when designing add-ons to protect user information. |
| `item.id` | `string` The ID of the selected item. |
| `item.iconUrl` | `string` The URL of the icon that represents the selected item. |
| `item.mimeType` | `string` The MIME type of the selected item. |
| `item.title` | `string` The title of the selected item. |

## Gmail event object

The Gmail event object is the portion of the overall event object that carries information about a user's Gmail messages. It's only present in an event object if the host application is Gmail.

| Gmail event object |  |
| --- | --- |
| `gmail.accessToken` | `string` The Gmail-specific access token. Use this token with the [`GmailApp.setCurrentMessageAccessToken`](/apps-script/reference/gmail/gmail-app#setcurrentmessageaccesstokenaccesstoken) method to grant your add-on temporary access to a user's currently open Gmail message or let your add-on compose new drafts. |
| `gmail.bccRecipients[]` | `list of strings` **Disabled by default**. The list of "BCC:" recipient email addresses currently included in a draft the add-on is composing. To turn on this field, set the `addOns.gmail.composeTrigger.draftAccess` field in your manifest to `METADATA`. |
| `gmail.ccRecipients[]` | `list of strings` **Disabled by default**. The list of "CC:" recipient email addresses currently included in a draft the add-on is composing. To turn on this field, set the `addOns.gmail.composeTrigger.draftAccess` field in your manifest to `METADATA`. |
| `gmail.messageId` | `string` The ID of the currently open Gmail message. |
| `gmail.threadId` | `string` The currently open Gmail thread ID. |
| `gmail.toRecipients[]` | `list of strings` **Disabled by default**. The list of "To:" recipient email addresses currently included in a draft the add-on is composing. To turn on this field, set the `addOns.gmail.composeTrigger.draftAccess` field in your manifest to `METADATA`. |

## Docs event object

The Docs event object is the portion of the overall event object that carries information about a user's document and its contents. It's only present in an event object if the add-on extends Google Docs.

| Docs event object |  |
| --- | --- |
| `docs.id` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The ID of the document open in the Docs UI. |
| `docs.title` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The title of the document open in the Docs UI. |
| `docs.addonHasFileScopePermission` | `boolean` If `true`, the add-on has requested and received `https://www.googleapis.com/auth/drive.file` scope authorization for the document open in the Docs UI; otherwise this field is `false`. |
| `docs.matchedUrl.url` | `string` **Only present if the following conditions are met:** `https://www.googleapis.com/auth/workspace.linkpreview` has been authorized by the user. The URL matches the host pattern specified in the `LinkPreviewTriggers` trigger. The URL of the link that generates a preview in Google Docs. To use this field, you must configure the `LinkPreviewTriggers` in your add-on's manifest. See [Preview links with smart chips](/workspace/add-ons/editors/gsao/preview-links) for more details. Example payload for when a user previews the link `https://www.example.com/12345`: "docs" : { "matchedUrl" : { "url" : "https://www.example.com/12345" } } |

## Sheets event object

The Sheets event object is the portion of the overall event object that carries information about a user's document and its contents. It's only present in an event object if the add-on extends Google Sheets.

| Sheets event object |  |
| --- | --- |
| `sheets.id` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The ID of the spreadsheet open in the Sheets UI. |
| `sheets.title` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The title of the spreadsheet open in the Sheets UI. |
| `sheets.addonHasFileScopePermission` | `boolean` If `true`, the add-on has requested and received `https://www.googleapis.com/auth/drive.file` scope authorization for the spreadsheet open in the Sheets UI; otherwise this field is `false`. |
| `sheets.matchedUrl.url` | `string` **Only present if the following conditions are met:** `https://www.googleapis.com/auth/workspace.linkpreview` has been authorized by the user. The URL matches the host pattern specified in the `LinkPreviewTriggers` trigger. The URL of the link that generates a preview in Google Sheets. To use this field, configure the `LinkPreviewTriggers` in your add-on's manifest. See [Preview links with smart chips](/workspace/add-ons/editors/gsao/preview-links) for more details. Example payload for when a user previews the link `https://www.example.com/12345`: "sheets" : { "matchedUrl" : { "url" : "https://www.example.com/12345" } } |

## Slides event object

The Slides event object is the portion of the overall event object that carries information about a user's document and its contents. It's only present in an event object if the add-on extends Google Slides.

| Slides event object |  |
| --- | --- |
| `slides.id` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The ID of the presentation open in the Slides UI. |
| `slides.title` | `string` **Only present if the ` https://www.googleapis.com/auth/drive.file` scope has been authorized by the user**. The title of the presentation open in the Slides UI. |
| `slides.addonHasFileScopePermission` | `boolean` If `true`, the add-on has requested and received `https://www.googleapis.com/auth/drive.file` scope authorization for the presentation open in the Slides UI; otherwise this field is `false`. |
| `slides.matchedUrl.url` | `string` **Only present if the following conditions are met:** `https://www.googleapis.com/auth/workspace.linkpreview` has been authorized by the user. The URL matches the host pattern specified in the `LinkPreviewTriggers` trigger. The URL of the link that generates a preview in Google Slides. To use this field, configure the `LinkPreviewTriggers` in your add-on's manifest. See [Preview links with smart chips](/workspace/add-ons/editors/gsao/preview-links) for more details. Example payload for when a user previews the link `https://www.example.com/12345`: "slides" : { "matchedUrl" : { "url" : "https://www.example.com/12345" } } |
