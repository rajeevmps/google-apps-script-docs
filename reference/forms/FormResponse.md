# FormResponse

A response to the form as a whole.

A response to the form as a whole. A `FormResponse` can be used in three ways: to access the answers submitted by a respondent (see `getItemResponses()`), to programmatically submit a response to the form (see `withItemResponse(response)` and `submit()`), and to generate a URL for the form which pre-fills fields using the provided answers. `FormResponse`s can be created or accessed from a `Form`.

## Methods

### getEditResponseUrl()
`getEditResponseUrl(): String`

Generates a URL that can be used to edit a response that has already been submitted. If the `Form.setAllowResponseEdits(enabled)` setting is disabled, the link leads to a page that explains that editing form responses is disabled. Anyone who visits the link can edit the response, although they need an account with access to the form if the `Form.setRequireLogin(requireLogin)` setting is enabled. If the `Form.setCollectEmail(collect)` setting is enabled, the form records the email address of the user who edited the response instead of the email address of the original respondent.

For a form response that the script has created but not yet submitted, this method returns `null`.

### getGradableItemResponses()
`getGradableItemResponses(): ItemResponse[]`

Gets all item responses contained in a form response, in the same order that the items appear in the form. This method works similarly to `getItemResponses()`, but to allow for grading a missing answer, it still returns an `ItemResponse` if the corresponding `Item` can be graded (that is, has a point value), even if there isn't an actual response. However, if the `Item` isn't gradable, this method excludes that item from its returned array.

### getGradableResponseForItem(item)
`getGradableResponseForItem(item: Item): ItemResponse`

Gets the item response contained in a form response for a given item. This method works similarly to `getResponseForItem(item)`, but to allow for grading a missing answer, it still returns an `ItemResponse` if the corresponding `Item` can be graded (that is, has a point value), even if there isn't an actual response. However, if the `Item` isn't gradable, this method returns `null`.

### getId()
`getId(): String|null`

Gets the ID of the form response. This method returns `null` if the form response has not been submitted.

### getItemResponses()
`getItemResponses(): ItemResponse[]`

Gets all item responses contained in a form response, in the same order that the items appear in the form. If the form response does not contain a response for a given `TextItem`, `DateItem`, `TimeItem`, or `ParagraphTextItem`, the `ItemResponse` returned for that item will have an empty string as the response. If the form response omits a response for any other item type, this method excludes that item from its returned array.

### getRespondentEmail()
`getRespondentEmail(): String`

Gets the email address of the person who submitted a response, if the `Form.setCollectEmail(collect)` setting is enabled.

For a form response that the script has created but not yet submitted, this method returns `null`.

### getResponseForItem(item)
`getResponseForItem(item: Item): ItemResponse`

Gets the item response contained in this form response for a given item.

### getTimestamp()
`getTimestamp(): Date`

Gets the timestamp for a form response submission.

For a form response that the script has created but not yet submitted, this method returns `null`.

### submit()
`submit(): FormResponse`

Submits the response. Throws a scripting exception if the response has already been submitted.

### toPrefilledUrl()
`toPrefilledUrl(): String`

Generates a URL for the form in which the answers are pre-filled based on the answers in this form response.

### withItemGrade(gradedResponse)
`withItemGrade(gradedResponse: ItemResponse): FormResponse`

Adds the given item response's grades to a form response. This method applies only to form responses that have already been submitted, and only affects stored grades once they are submitted. This method also only updates the item response's grades; it does not affect the actual response (since the response has already been submitted). If this method is called multiple times for the same item, only the last grade is retained. If the `ItemResponse` contains no grades, this method removes grades for the item.

### withItemResponse(response)
`withItemResponse(response: ItemResponse): FormResponse`

Adds the given item response to a form response. This method applies only to form responses that the script has created but not yet submitted; it cannot affect stored responses. If this method is called multiple times for the same item, only the last item response is retained.
