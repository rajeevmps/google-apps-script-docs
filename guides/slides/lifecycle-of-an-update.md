# Lifecycle of a presentation update

## Page Summary

- A Presentation object in Slides Service has three main phases: opening, editing, and saving.
- Presentations can be opened using methods like `openById()`, `getActivePresentation()`, or created using `create()`.
- Changes made to an open presentation are reflected during script execution but not to collaborators until saved.
- Changes to a presentation are saved automatically when the script finishes or manually by calling `saveAndClose()`.

There are three main phases in the lifecycle of a
[Presentation](https://developers.google.com/apps-script/reference/slides/presentation) object: open,
edit, and save.

## Open a presentation

When using the Slides Service, the first step is to load a
presentation. Methods
like [SlidesApp.openById()](https://developers.google.com/apps-script/reference/slides/slides-app#openbyidid)
and
[SlidesApp.getActivePresentation()](https://developers.google.com/apps-script/reference/slides/slides-app#getactivepresentation)
load an existing Slides presentation, while
[SlidesApp.create()](https://developers.google.com/apps-script/reference/slides/slides-app#createname)
creates a new presentation. These methods return a
[Presentation](https://developers.google.com/apps-script/reference/slides/presentation) object that
represents the loaded presentation.

Once a presentation is open, it does not receive any further updates from
collaborators. Presentations are usually opened at their latest saved version
in Google Drive. However, if a script is container-bound to a
presentation,
that presentation is loaded at the same version as the accompanying
Slides editor.

## Modify a presentation

After a presentation is open, a script can read and modify it. Any changes that
the script makes to the presentation are reflected in subsequent reads and
modifications for the duration of the script execution.

## Save changes

After making changes to a presentation, the changes are saved all at once
when the script execution completes, or when
[Presentation.saveAndClose()](https://developers.google.com/apps-script/reference/slides/presentation#saveandclose)
is called. After changes are saved, they propagate asynchronously to the
user's editor, as if the changes were made by a collaborator.

After a presentation is closed using `Presentation.saveAndClose()`, it can be
reopened for editing using one of the presentation loading methods.
