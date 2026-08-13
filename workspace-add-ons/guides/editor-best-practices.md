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

## Editor add-on best practices

The following best practices only apply to Editor add-on.

### Place interface HTML and client-side JavaScript in their own script files

You can create multiple script files in an Apps Script project. It's easier to manage a complex add-on if you place the HTML and JavaScript that defines the add-on sidebars and dialogs in script files dedicated to them.

### Test thoroughly in different authorization modes

When testing your add-on, be sure to try configurations that have different files and different authorization states.
