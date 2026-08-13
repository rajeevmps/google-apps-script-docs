# Presentation

A presentation.

## Methods

### addEditor(emailAddress)

`Presentation`

Adds the given user to the list of editors for the Presentation. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

**Parameters**

- `emailAddress` (`String`) — The email address of the user to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### addEditor(user)

`Presentation`

Adds the given user to the list of editors for the Presentation. If the user was already on the list of viewers, this method promotes the user out of the list of viewers.

**Parameters**

- `user` (`User`) — A representation of the user to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### addEditors(emailAddresses)

`Presentation`

Adds the given array of users to the list of editors for the Presentation. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

**Parameters**

- `emailAddresses` (`String[]`) — An array of email addresses of the users to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### addViewer(emailAddress)

`Presentation`

Adds the given user to the list of viewers for the Presentation. If the user was already on the list of editors, this method has no effect.

**Parameters**

- `emailAddress` (`String`) — The email address of the user to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### addViewer(user)

`Presentation`

Adds the given user to the list of viewers for the Presentation. If the user was already on the list of editors, this method has no effect.

**Parameters**

- `user` (`User`) — A representation of the user to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### addViewers(emailAddresses)

`Presentation`

Adds the given array of users to the list of viewers for the Presentation. If any of the users were already on the list of editors, this method has no effect for them.

**Parameters**

- `emailAddresses` (`String[]`) — An array of email addresses of the users to add.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendSlide()

`Slide`

Appends a slide to the end of the presentation using the PredefinedLayout.BLANK predefined layout based on the current master. The current master is one of the following:

- The master of the current last slide.
- The first master in the presentation, if there is no slide.

**Returns**

`Slide` — The new slide that is appended.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendSlide(layout)

`Slide`

Appends a slide to the end of the presentation using the specified layout based on the current master. The current master is one of the following:

- The master of the current last slide.
- The first master in the presentation, if there is no slide.

**Parameters**

- `layout` (`Layout`) — The layout to use for the new slide; it should be present in the current master.

**Returns**

`Slide` — The new slide that is appended.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendSlide(predefinedLayout)

`Slide`

Appends a slide to the end of the presentation using the specified predefined layout based on the current master. The current master is one of the following:

- The master of the current last slide.
- The first master in the presentation, if there is no slide.

**Parameters**

- `predefinedLayout` (`PredefinedLayout`) — The predefined layout to use for the new slide; it should be present in the current master.

**Returns**

`Slide` — The new slide that is appended.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendSlide(slide)

`Slide`

Appends a copy of the provided Slide to the end of the presentation.

If the slide being copied is from a different presentation, the parent master and layout pages are copied as well if they do not already exist in this presentation.

```javascript
// Copy a slide from another presentation and appends it.
const otherPresentation = SlidesApp.openById('presentationId');
const currentPresentation = SlidesApp.getActivePresentation();
const slide = otherPresentation.getSlides()[0];
currentPresentation.appendSlide(slide);
```

**Parameters**

- `slide` (`Slide`) — The slide to be copied and appended.

**Returns**

`Slide` — The new slide that is appended.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### appendSlide(slide, linkingMode)

`Slide`

Appends a copy of the provided Slide from the source presentation to the end of the current presentation, and sets the slide link as specified by the SlideLinkingMode.

If the slide being copied is from a different presentation, the parent master and layout pages are copied as well if they do not already exist in the current presentation.

If the link mode is SlideLinkingMode.LINKED, the appended slide can be updated to match the provided source slide when Slide.refreshSlide() is called. Other collaborators can see the link to the source slide. SlideLinkingMode.LINKED cannot be used with source slides from the current presentation.

```javascript
// Copy a slide from another presentation, then append and link it.
const sourcePresentation = SlidesApp.openById('presentationId');
const currentPresentation = SlidesApp.getActivePresentation();
const slide = sourcePresentation.getSlides()[0];
const appendedSlide = currentPresentation.appendSlide(
    slide,
    SlidesApp.SlideLinkingMode.LINKED,
);
```

**Parameters**

- `slide` (`Slide`) — The slide to be copied, appended, and linked.
- `linkingMode` (`SlideLinkingMode`) — The link mode to use.

**Returns**

`Slide` — The new slide.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getEditors()

`User[]`

Gets the list of editors for this Presentation.

**Returns**

`User[]` — An array of users with edit permission.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getId()

`String`

Gets the presentation's unique identifier. The presentation ID is used with SlidesApp.openById() to open a specific presentation instance.

**Returns**

`String` — The ID of this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getLayouts()

`Layout[]`

Gets the layouts in the presentation.

**Returns**

`Layout[]` — The list of layouts in this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getMasters()

`Master[]`

Gets the masters in the presentation.

**Returns**

`Master[]` — The list of masters in this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getName()

`String`

Gets the name or title of the presentation.

**Returns**

`String` — The title of this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNotesMaster()

`NotesMaster`

Gets the notes master of the presentation.

**Returns**

`NotesMaster` — The notes master of the presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNotesPageHeight()

`Number`

Gets the page height of the notes master and notes pages in the presentation in points. They all have the same page height.

**Returns**

`Number` — The notes page height in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getNotesPageWidth()

`Number`

Gets the page width of the notes master and notes pages in the presentation in points. They all have the same page width.

**Returns**

`Number` — The notes page width in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageElementById(id)

`PageElement|null`

Returns the PageElement with the given ID, or null if none exists.

**Parameters**

- `id` (`String`) — The ID of the page element that is being retrieved.

**Returns**

`PageElement|null` — The page element with the given ID.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageHeight()

`Number`

Gets the page height of the slides, layouts, and masters in the presentation in points. They all have the same page height.

**Returns**

`Number` — The page height in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getPageWidth()

`Number`

Gets the page width of the slides, layouts, and masters in the presentation in points. They all have the same page width.

**Returns**

`Number` — The page width in points.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSelection()

`Selection|null`

Gets the user’s selection in the active presentation. A script can only access the selection of the user who is running the script, and only if the script is bound to the presentation.

Note that the selection returned is the current effective selection. As the script performs various changes to the presentation, the selection is transformed to take them into account. For example if two shapes A and B are selected, and then the script removes shape B, the returned selection object is implicitly updated such that only shape A is selected.

```javascript
// Gets the current active page that is selected in the active presentation.
const selection = SlidesApp.getActivePresentation().getSelection();
const currentPage = selection.getCurrentPage();
```

**Returns**

`Selection|null` — A representation of the user's selection, or null if the script is not bound to the presentation or if there is no valid user selection.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlideById(id)

`Slide|null`

Returns the Slide with the given ID, or null if none exists.

**Parameters**

- `id` (`String`) — The ID of the slide that is being retrieved.

**Returns**

`Slide|null` — The slide with the given ID.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getSlides()

`Slide[]`

Gets the slides in the presentation.

**Returns**

`Slide[]` — The list of slides in this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getUrl()

`String`

Retrieves the URL to access this presentation.

```javascript
const presentation = SlidesApp.getActivePresentation();

// Send out the link to open the presentation.
MailApp.sendEmail(
    '<email-address>',
    presentation.getName(),
    presentation.getUrl(),
);
```

**Returns**

`String` — The URL to access the current presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### getViewers()

`User[]`

Gets the list of viewers and commenters for this Presentation.

**Returns**

`User[]` — An array of users with view or comment permission.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSlide(insertionIndex)

`Slide`

Inserts a slide at the specified index in the presentation using the PredefinedLayout.BLANK predefined layout based on the current master. The current master is one of the following:

- The master of the previous slide.
- The master of the first slide, if the insertionIndex is zero.
- The first master in the presentation, if there is no slide.

**Parameters**

- `insertionIndex` (`Integer`) — The zero-based index indicating where to insert the slide.

**Returns**

`Slide` — The new slide that is inserted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSlide(insertionIndex, layout)

`Slide`

Inserts a slide at the specified index in the presentation using the specified layout based on the current master. The current master is one of the following:

- The master of the previous slide.
- The master of the first slide, if the insertionIndex is zero.
- The first master in the presentation, if there is no slide.

**Parameters**

- `insertionIndex` (`Integer`) — The zero-based index indicating where to insert the slide.
- `layout` (`Layout`) — The layout to use for the new slide; it should be present in the current master.

**Returns**

`Slide` — The new slide that is inserted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSlide(insertionIndex, predefinedLayout)

`Slide`

Inserts a slide at the specified index in the presentation using the specified predefined layout based on the current master. The current master is one of the following:

- The master of the previous slide.
- The master of the first slide, if the insertionIndex is zero.
- The first master in the presentation, if there is no slide.

**Parameters**

- `insertionIndex` (`Integer`) — The zero-based index indicating where to insert the slide.
- `predefinedLayout` (`PredefinedLayout`) — The predefined layout to use for the new slide; it should be present in the current master.

**Returns**

`Slide` — The new slide that is inserted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSlide(insertionIndex, slide)

`Slide`

Inserts a copy of the provided Slide at the specified index in the presentation.

If the slide being copied is from a different presentation, the parent master and layout pages are copied as well if they do not already exist in this presentation.

```javascript
// Copy a slide from another presentation and inserts it.
const otherPresentation = SlidesApp.openById('presentationId');
const currentPresentation = SlidesApp.getActivePresentation();
const slide = otherPresentation.getSlides()[0];
const insertionIndex = 1;
currentPresentation.insertSlide(insertionIndex, slide);
```

**Parameters**

- `insertionIndex` (`Integer`) — The zero-based index indicating where to insert the slide.
- `slide` (`Slide`) — The slide to be copied and inserted.

**Returns**

`Slide` — The new slide that is inserted.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### insertSlide(insertionIndex, slide, linkingMode)

`Slide`

Inserts a copy of the provided Slide from the source presentation into the specified index in the current presentation, and sets the slide link as specified by the SlideLinkingMode.

If the slide being copied is from a different presentation, the parent master and layout pages are copied as well if they do not already exist in the current presentation.

If the link mode is SlideLinkingMode.LINKED, the inserted slide can be updated to match the provided source slide when Slide.refreshSlide() is called. Other collaborators can see the link to the source slide. SlideLinkingMode.LINKED cannot be used with source slides from the current presentation.

```javascript
// Copy a slide from another presentation, then insert and link it.
const sourcePresentation = SlidesApp.openById('presentationId');
const currentPresentation = SlidesApp.getActivePresentation();
const slide = sourcePresentation.getSlides()[0];
const insertionIndex = 1;
const insertedSlide = currentPresentation.insertSlide(
    insertionIndex,
    slide,
    SlidesApp.SlideLinkingMode.LINKED,
);
```

**Parameters**

- `insertionIndex` (`Integer`) — The zero-based index indicating where to insert the slide.
- `slide` (`Slide`) — The slide to be copied and inserted.
- `linkingMode` (`SlideLinkingMode`) — The link mode to use.

**Returns**

`Slide` — The new slide.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeEditor(emailAddress)

`Presentation`

Removes the given user from the list of editors for the Presentation. This method doesn't block users from accessing the Presentation if they belong to a class of users who have general access—for example, if the Presentation is shared with the user's entire domain, or if the Presentation is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of viewers.

**Parameters**

- `emailAddress` (`String`) — The email address of the user to remove.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeEditor(user)

`Presentation`

Removes the given user from the list of editors for the Presentation. This method doesn't block users from accessing the Presentation if they belong to a class of users who have general access—for example, if the Presentation is shared with the user's entire domain, or if the Presentation is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of viewers.

**Parameters**

- `user` (`User`) — A representation of the user to remove.

**Returns**

`Presentation` — This Presentation, for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeViewer(emailAddress)

`Presentation`

Removes the given user from the list of viewers and commenters for the Presentation. This method has no effect if the user is an editor, not a viewer or commenter. This method also doesn't block users from accessing the Presentation if they belong to a class of users who have general access—for example, if the Presentation is shared with the user's entire domain, or if the Presentation is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of editors.

**Parameters**

- `emailAddress` (`String`) — The email address of the user to remove.

**Returns**

`Presentation` — This Presentation for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### removeViewer(user)

`Presentation`

Removes the given user from the list of viewers and commenters for the Presentation. This method has no effect if the user is an editor, not a viewer. This method also doesn't block users from accessing the Presentation if they belong to a class of users who have general access—for example, if the Presentation is shared with the user's entire domain, or if the Presentation is in a shared drive that the user can access.

For Drive files, this also removes the user from the list of editors.

**Parameters**

- `user` (`User`) — A representation of the user to remove.

**Returns**

`Presentation` — This Presentation for chaining.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText)

`Integer`

Replaces all instances of text matching find text with replace text. The search is case insensitive.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### replaceAllText(findText, replaceText, matchCase)

`Integer`

Replaces all instances of text matching find text with replace text.

**Parameters**

- `findText` (`String`) — The text to find.
- `replaceText` (`String`) — The text to replace the matched text.
- `matchCase` (`Boolean`) — If true, the search is case sensitive; if false, the search is case insensitive.

**Returns**

`Integer` — The number of occurrences changed.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### saveAndClose()

Saves the current Presentation. Causes pending updates to be flushed and applied.

The saveAndClose() method is automatically invoked at the end of script execution for each open Presentation, even if the script execution terminated with an error.

A closed Presentation cannot be edited. Use one of the open methods on SlidesApp to reopen a given presentation for editing.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

### setName(name)

Sets the name or title of the presentation.

**Parameters**

- `name` (`String`) — The name to set for this presentation.

**Authorization**

Scripts that use this method require authorization with one or more of the following scopes:
- `https://www.googleapis.com/auth/presentations.currentonly`
- `https://www.googleapis.com/auth/presentations`

## Properties

This class has no properties listed on the reference page.
