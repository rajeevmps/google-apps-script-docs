# DocumentTriggerBuilder

A builder for document triggers.

A builder for document triggers.

## Methods

### create() → Trigger

Creates and returns the new trigger.

**Return:** `Trigger` — The new trigger.

### onOpen() → DocumentTriggerBuilder

Specifies a trigger that fires when the document is opened.

**Return:** `DocumentTriggerBuilder` — This `DocumentTriggerBuilder`, for chaining.

```javascript
const document = DocumentApp.getActiveDocument();
ScriptApp.newTrigger('myFunction').forDocument(document).onOpen().create();
```
