# Form

A form that has been created and saved in Google Drive.

A form that has been created and saved in Google Drive. Scripts can create a `Form` directly with `FormApp.create(title)`, or operate on an existing form via `FormApp.getActiveForm()` (for forms container-bound to the script) or `FormApp.openById(id)` / `FormApp.openByUrl(url)`.

## Methods

### Item Creation Methods

#### addCheckboxGridItem()
`addCheckboxGridItem(): CheckboxGridItem`

Appends a new question item, presented as a grid of columns and rows, that allows the respondent to select multiple choices per row from a sequence of checkboxes.

#### addCheckboxItem()
`addCheckboxItem(): CheckboxItem`

Appends a new question item that allows the respondent to select one or more checkboxes, as well as an optional "other" field.

#### addDateItem()
`addDateItem(): DateItem`

Appends a new question item that allows the respondent to indicate a date.

#### addDateTimeItem()
`addDateTimeItem(): DateTimeItem`

Appends a new question item that allows the respondent to indicate a date and time.

#### addDurationItem()
`addDurationItem(): DurationItem`

Appends a new question item that allows the respondent to indicate a length of time.

#### addGridItem()
`addGridItem(): GridItem`

Appends a new question item, presented as a grid of columns and rows, that allows the respondent to select one choice per row from a sequence of radio buttons.

#### addImageItem()
`addImageItem(): ImageItem`

Appends a new layout item that displays an image.

#### addListItem()
`addListItem(): ListItem`

Appends a new question item that allows the respondent to select one choice from a dropdown list.

#### addMultipleChoiceItem()
`addMultipleChoiceItem(): MultipleChoiceItem`

Adds a new question item that allows the respondent to select one choice from a list of radio buttons or an optional "other" field.

#### addPageBreakItem()
`addPageBreakItem(): PageBreakItem`

Adds a new layout item that marks the start of a page.

#### addParagraphTextItem()
`addParagraphTextItem(): ParagraphTextItem`

Adds a new question item that allows the respondent to enter a block of text.

#### addRatingItem()
`addRatingItem(): RatingItem`

Appends a new question item that allows the respondent to give a rating.

#### addScaleItem()
`addScaleItem(): ScaleItem`

Appends a new question item that allows the respondent to choose one option from a numbered sequence of radio buttons.

#### addSectionHeaderItem()
`addSectionHeaderItem(): SectionHeaderItem`

Appends a new layout item that visually indicates the start of a section.

#### addTextItem()
`addTextItem(): TextItem`

Appends a new question item that allows the respondent to enter a single line of text.

#### addTimeItem()
`addTimeItem(): TimeItem`

Appends a new question item that allows the respondent to indicate a time of day.

#### addVideoItem()
`addVideoItem(): VideoItem`

Appends a new layout item that displays a video.

### Editor/Responder Management Methods

#### addEditor(emailAddress)
`addEditor(emailAddress: String): Form`

Adds the given user to the list of editors for the `Form`. If the user was already on the list of viewers or responders, this method promotes the user out of the list.

#### addEditor(user)
`addEditor(user: User): Form`

Adds the given user to the list of editors for the `Form`. If the user was already on the list of viewers or responders, this method promotes the user out of the list.

#### addEditors(emailAddresses)
`addEditors(emailAddresses: String[]): Form`

Adds the given array of users to the list of editors for the `Form`. If any of the users were already on the list of viewers, this method promotes them out of the list of viewers.

#### addPublishedReader(emailAddress)
`addPublishedReader(emailAddress: String): Form`

Adds the given user to the list of responders for the `Form`.

#### addPublishedReader(user)
`addPublishedReader(user: User): Form`

Adds the given user to the list of responders for the `Form`.

#### addPublishedReaders(emailAddresses)
`addPublishedReaders(emailAddresses: String[]): Form`

Adds the given array of users to the list of responders for the `Form`.

#### removeEditor(emailAddress)
`removeEditor(emailAddress: String): Form`

Removes the given user from the list of editors for the `Form`.

#### removeEditor(user)
`removeEditor(user: User): Form`

Removes the given user from the list of editors for the `Form`.

#### removePublishedReader(emailAddress)
`removePublishedReader(emailAddress: String): Form`

Removes the given user from the list of responders for the `Form`.

#### removePublishedReader(user)
`removePublishedReader(user: User): Form`

Removes the given user from the list of responders for the `Form`.

### Response Management Methods

#### createResponse()
`createResponse(): FormResponse`

Creates a new response to the form.

#### deleteAllResponses()
`deleteAllResponses(): Form`

Deletes all submitted responses from the form's response store.

#### deleteResponse(responseId)
`deleteResponse(responseId: String): Form`

Deletes a single response from the form's response store.

#### getResponse(responseId)
`getResponse(responseId: String): FormResponse`

Gets a single form response based on its response ID.

#### getResponses()
`getResponses(): FormResponse[]`

Gets an array of all of the form's responses.

#### getResponses(timestamp)
`getResponses(timestamp: Date): FormResponse[]`

Gets an array of all of the form's responses after a given date and time.

#### submitGrades(responses)
`submitGrades(responses: FormResponse[]): Form`

Submits grades for the given `FormResponse`s.

### Item Management Methods

#### deleteItem(index)
`deleteItem(index: Integer): void`

Deletes the item at a given index among all the items in the form.

#### deleteItem(item)
`deleteItem(item: Item): void`

Deletes the given item.

#### getItemById(id)
`getItemById(id: Integer): Item|null`

Gets the item with a given ID.

#### getItems()
`getItems(): Item[]`

Gets an array of all items in the form.

#### getItems(itemType)
`getItems(itemType: ItemType): Item[]`

Gets an array of all items of a given type.

#### moveItem(from, to)
`moveItem(from: Integer, to: Integer): Item`

Moves an item at a given index among all the items in the form to another given index.

#### moveItem(item, toIndex)
`moveItem(item: Item, toIndex: Integer): Item`

Moves a given item to a given index among all the items in the form.

### Form Property Getter Methods

#### getConfirmationMessage()
`getConfirmationMessage(): String`

Gets the form's confirmation message.

#### getCustomClosedFormMessage()
`getCustomClosedFormMessage(): String`

Gets the custom message that is displayed if the form is not accepting responses, or an empty string if no custom message is set.

#### getDescription()
`getDescription(): String`

Gets the form's description.

#### getDestinationId()
`getDestinationId(): String`

Gets the ID of the form's response destination.

#### getDestinationType()
`getDestinationType(): DestinationType`

Gets the type of the form's response destination.

#### getEditUrl()
`getEditUrl(): String`

Gets the URL that can be used to access the form's edit mode.

#### getEditors()
`getEditors(): User[]`

Gets the list of editors for this `Form`.

#### getId()
`getId(): String`

Gets the ID of the form.

#### getPublishedReaders()
`getPublishedReaders(): User[]`

Gets the list of responders for this `Form`.

#### getPublishedUrl()
`getPublishedUrl(): String`

Gets the URL that can be used to respond to the form.

#### getSummaryUrl()
`getSummaryUrl(): String`

Gets the URL that can be used to view a summary of the form's responses.

#### getTitle()
`getTitle(): String`

Gets the form's title.

### Form Property Setter Methods

#### setAcceptingResponses(enabled)
`setAcceptingResponses(enabled: Boolean): Form`

Sets whether the form is currently accepting responses.

#### setAllowResponseEdits(enabled)
`setAllowResponseEdits(enabled: Boolean): Form`

Sets whether the form displays a link to edit a response after submitting it.

#### setCollectEmail(collect)
`setCollectEmail(collect: Boolean): Form`

Sets whether the form collects respondents' email addresses.

#### setConfirmationMessage(message)
`setConfirmationMessage(message: String): Form`

Sets the form's confirmation message.

#### setCustomClosedFormMessage(message)
`setCustomClosedFormMessage(message: String): Form`

Sets the message to display if the form is not accepting responses.

#### setDescription(description)
`setDescription(description: String): Form`

Sets the form's description.

#### setDestination(type, id)
`setDestination(type: DestinationType, id: String): Form`

Sets the destination where form responses are saved.

#### setIsQuiz(enabled)
`setIsQuiz(enabled: Boolean): Form`

Sets whether the form is a quiz.

#### setLimitOneResponsePerUser(enabled)
`setLimitOneResponsePerUser(enabled: Boolean): Form`

Sets whether the form allows only one response per respondent.

#### setProgressBar(enabled)
`setProgressBar(enabled: Boolean): Form`

Sets whether the form has a progress bar.

#### setPublished(enabled)
`setPublished(enabled: Boolean): Form`

Sets whether the form is published.

#### setPublishingSummary(enabled)
`setPublishingSummary(enabled: Boolean): Form`

Sets whether the form displays a link to view a summary of responses after a respondent submits the form.

#### setShowLinkToRespondAgain(enabled)
`setShowLinkToRespondAgain(enabled: Boolean): Form`

Sets whether the form displays a link to submit another response after a respondent completes the form.

#### setShuffleQuestions(shuffle)
`setShuffleQuestions(shuffle: Boolean): Form`

Sets whether the order of the questions on each page of the form is randomized.

#### setTitle(title)
`setTitle(title: String): Form`

Sets the form's title.

### Form Property Boolean Query Methods

#### canEditResponse()
`canEditResponse(): Boolean`

Determines whether the form displays a link to edit a response after submitting it.

#### collectsEmail()
`collectsEmail(): Boolean`

Determines whether the form collects respondents' email addresses.

#### getShuffleQuestions()
`getShuffleQuestions(): Boolean`

Determines whether the order of the questions on each page of the form is randomized.

#### hasLimitOneResponsePerUser()
`hasLimitOneResponsePerUser(): Boolean`

Determines whether the form allows only one response per respondent.

#### hasProgressBar()
`hasProgressBar(): Boolean`

Determines whether the form displays a progress bar.

#### hasRespondAgainLink()
`hasRespondAgainLink(): Boolean`

Determines whether the form displays a link to submit another response after a respondent completes the form.

#### isAcceptingResponses()
`isAcceptingResponses(): Boolean`

Determines whether the form is currently accepting responses.

#### isPublished()
`isPublished(): Boolean`

Determines whether the form is published.

#### isPublishingSummary()
`isPublishingSummary(): Boolean`

Determines whether the form displays a link to view a summary of responses after a respondent completes the form.

#### isQuiz()
`isQuiz(): Boolean`

Determines whether the form is a quiz.

#### supportsAdvancedResponderPermissions()
`supportsAdvancedResponderPermissions(): Boolean`

Determines whether the form supports publishing.

### URL & Utility Methods

#### removeDestination()
`removeDestination(): Form`

Unlinks the form from its current response destination.

#### shortenFormUrl(url)
`shortenFormUrl(url: String): String`

Converts a long URL for a form to a short URL.

### Deprecated Methods

#### requiresLogin()
`requiresLogin(): Boolean`

*Deprecated.* Determines whether the form requires respondents to log in to an account in the same domain or a subdomain before responding.

#### setRequireLogin(requireLogin)
`setRequireLogin(requireLogin: Boolean): Form`

*Deprecated.* Sets whether the form requires respondents to log in to an account in the same domain or a subdomain before responding.
