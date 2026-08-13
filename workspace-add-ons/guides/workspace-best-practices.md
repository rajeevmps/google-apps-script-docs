# Best practices

Improve your users' overall experience by following these guides for add-on design.

## General best practices

You are encouraged to use the following best practices for all add-ons you develop.

### Determine add-on ownership before starting

Add-ons are defined by Apps Script projects, which must be owned by a specific account or else placed in a shared drive. Before coding an add-on, determine what account should own the project, and what account acts as its publisher. Also determine what accounts are to act as collaborators, and make sure those accounts have access to the script project and its associated Google Cloud project.

**Note:** It's important to plan add-on ownership. If the add-on owner leaves your organization, you must make sure ownership is transferred or else you could lose the ability to update and manage your add-on. For this reason, it may be best to create an organization account specifically to own and publish your organization's add-ons. You can also use a shared drive to act as the script project owner, but a specific account must act as the add-on publisher.

### Extend Google Workspace, don't replicate it

Add-ons are meant to provide new capabilities to the Google Workspace applications they extend, or else automate complex tasks. Add-ons that merely replicate functionality already within the application or ones that don't make significant improvements to a workflow aren't likely to pass add-on review for publication.

### Keep the scopes narrow

When defining your scopes explicitly, always choose the least-permissive set of scopes possible. For example, don't have your add-on request full access to the user's Calendar with the `https://www.googleapis.com/auth/calendar` scope if it only needs read access. For read-only access, use the `https://www.googleapis.com/auth/calendar.readonly` scope.

### Avoid relying too much on libraries

Using Apps Script libraries can cause your add-on to run more slowly than it would if all the Apps Script code were contained within a single script project. Although Apps Script libraries work in add-ons, you might run into performance reductions if you use them. Avoid including unnecessary libraries in your project, and consider ways to reduce your add-on's reliance on them.

The latency described above only applies to Apps Script projects being used as server-side libraries. You can use client-side JavaScript libraries like jQuery freely without encountering this latency.

## Google Workspace add-on best practices

The following best practices only apply to Google Workspace add-ons and the use of the Card service.

### Use just a few cards

If the add-on uses too many cards the navigation configuration becomes complex and difficult to manage.

Avoid the impulse to create more cards than necessary.

### Use widget creation functions

When writing code that creates a `Card` or other complex UI objects, consider putting that code in its own function. This creation function should just build the object and return it. This lets you quickly regenerate that object whenever the UI must be refreshed. Remember to call `build()` after using the builder classes in the Card service.

### Keep cards simple

If a given card has too many widgets, it can fill too much of the screen and become less useful. While large card sections render as collapsible UI elements, this hides information from the user. Aim to streamline your add-on and provide exactly what the user needs and no more.

### Use error cards

Create cards for error conditions. If your add-on produces an error, it should display a card with the error information and instructions on how to correct it, if possible. For example, if your add-on couldn't connect to a non-Google service because the authorization failed, display a card stating this and ask the user to verify the account information being used.

### Write tests and test messages

You should thoroughly test all the add-ons you create. Build test functions that create cards and widgets using test data, and then verify that the objects are created as expected.

When using action callback functions, you usually must construct a response object. You can use statements like the following to verify that the responses are being constructed correctly:

    Logger.log(response.printJson());

Run test functions you create directly from the Apps Script editor using the **Run** menu. When you have a viable add-on working, be sure to install the unpublished version so you can test it.

Use test data appropriate for each host application the add-on extends. For example, if the add-on extends Gmail you're likely to need a few test emails and their message IDs so that you can ensure that the add-on functions as expected when given different message content. You can get the message ID for a given message by listing messages using the Gmail API `users.messages.list` method, or by making use of Apps Script's Gmail service.

## Calendar conferencing best practices

If your add-on integrates third-party calendar conferencing options into Google Calendar, follow these additional best practices:

### Keep your `onCreateFunction` light

Each `onCreateFunction` you define in your manifest is called synchronously when a user attempts to create a conference solution of that type. Make sure these functions only do the minimum necessary work to create the conference. Doing too much in these functions can cause a slow user experience for your add-on.

### Use appropriate `ConferenceData` fields for conference data

When you build `ConferenceData` objects, you can populate them with details about the conference (access codes, phone numbers, pins, URIs, etc.). Be sure to use the corresponding `EntryPoint` field for this information. Don't place these details in the `ConferenceData` notes field.

### Don't append conferencing details to the Calendar event

Your add-on doesn't need to add information about created third-party conferences to the Calendar event description. Calendar does this automatically when necessary.
