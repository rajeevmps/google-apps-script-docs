# Extend Google Slides

## Page Summary

- Google Apps Script allows you to programmatically create and modify Google Slides presentations using the Slides service.
- You can customize Google Slides by adding custom menus, dialog boxes, and sidebars with Apps Script.
- Apps Script lets you integrate Slides with other Google services like Calendar, Drive, and Gmail.
- You can publish your Apps Script projects as add-ons for Google Slides to share them with others.

Google Apps Script lets you programmatically create and modify
Slides presentations using the
[Slides service](https://developers.google.com/apps-script/reference/slides/slides-app).
Use Apps Script to add [custom menus](https://developers.google.com/apps-script/guides/menus),
[dialogs, and sidebars](https://developers.google.com/apps-script/guides/dialogs) to Slides.
You can also integrate Slides with other
[Google services](https://developers.google.com/apps-script/guides/services) like Google Calendar,
Google Drive, and Gmail.

The [Slides service](https://developers.google.com/apps-script/reference/slides/slides-app)
is the recommended way of working with Slides in
Apps Script. Also enable the [Slides advanced
service](https://developers.google.com/apps-script/advanced/slides) if you need to invoke the
[Google Slides API](https://developers.google.com/slides) directly.

## Get started

Apps Script includes a
[built-in service](https://developers.google.com/apps-script/reference/slides/slides-app)
that lets you programmatically create, read, and edit Slides.
Apps Script can interact with Slides in two ways:

1. Any script can create a new presentation or access an existing presentation
if the user has the appropriate access permissions for that presentation.
2. A script can be [bound](https://developers.google.com/apps-script/guides/bound) to a presentation, which
provides the script more direct access to the Slides user
interface for that script. To create a bound script, select **Extensions**
> **Apps Script**
from within Slides.

## Custom menus and user interfaces

Customize Slides by adding custom menus, dialog boxes, and
sidebars. To learn the basics of creating menus, see the
[guide to menus](https://developers.google.com/apps-script/guides/menus). To learn about customizing the
content of a dialog, see the
[guide to HTML service](https://developers.google.com/apps-script/guides/html#serve_html_as_a_google_docs_sheets_or_forms_user_interface).

If you're planning to publish your custom interface as part of an
Google Workspace add-on, follow the
[style guide](https://developers.google.com/workspace/add-ons/guides/editor-style) for
consistency with the style and layout of the Slides editor.

## Google Workspace add-ons for Slides

[Google Workspace add-ons](https://developers.google.com/workspace/add-ons/overview) are
specially packaged Apps Script
projects that run inside Slides and can be installed
from the Google Slides add-ons store. If you've
developed a script for Slides and want to share it with the
world, Apps Script lets you
[publish](https://developers.google.com/workspace/add-ons/how-tos/editor-publish-overview)
your script as an
add-on so other users can install it from the
add-on store.

See the
[sample translate add-on](https://developers.google.com/workspace/add-ons/editors/slides/quickstart/translate)
or
[sample progress bar add-on](https://developers.google.com/workspace/add-ons/editors/slides/quickstart/progress-bar)
for examples of Slides add-ons.
