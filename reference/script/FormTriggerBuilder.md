# FormTriggerBuilder

A builder for form triggers.

A builder for form triggers.

## Methods

### create() → Trigger

Creates and returns the new trigger.

**Return:** `Trigger` — The new trigger.

### onFormSubmit() → FormTriggerBuilder

Specifies a trigger that fires when a response is submitted to the form.

**Return:** `FormTriggerBuilder` — This `FormTriggerBuilder`, for chaining.

```javascript
const form = FormApp.openById('1234567890abcdefghijklmnopqrstuvwxyz');
ScriptApp.newTrigger('myFunction').forForm(form).onFormSubmit().create();
```

### onOpen() → FormTriggerBuilder

Specifies a trigger that fires when the form's edit view is opened.

**Return:** `FormTriggerBuilder` — This `FormTriggerBuilder`, for chaining.

```javascript
const form = FormApp.getActiveForm();
ScriptApp.newTrigger('myFunction').forForm(form).onOpen().create();
```
