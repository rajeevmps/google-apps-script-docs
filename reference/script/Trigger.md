# Trigger

A script trigger.

A script trigger.

## Methods

### getEventType() → EventType

Returns the event type that the trigger fires on.

**Return:** `EventType` — The event type that this is a trigger for.

```javascript
const triggers = ScriptApp.getProjectTriggers();
for (let i = 0; i < triggers.length; i++) {
  if (triggers[i].getEventType() === ScriptApp.EventType.CLOCK) {
    // Some code here - other options are:
    // ScriptApp.EventType.ON_EDIT
    // ScriptApp.EventType.ON_FORM_SUBMIT
    // ScriptApp.EventType.ON_OPEN
  }
}
```

### getHandlerFunction() → String

Returns the function that is called when the trigger fires.

**Return:** `String` — The method name.

```javascript
ScriptApp.newTrigger('myFunction')
    .forSpreadsheet('id of my spreadsheet')
    .onEdit()
    .create();
Logger.log(ScriptApp.getProjectTriggers()[0]
               .getHandlerFunction());  // logs "myFunction"
```

### getTriggerSource() → TriggerSource

Returns the source of events that causes the trigger to fire. For example, a spreadsheet onEdit trigger returns SPREADSHEETS, or a time based trigger returns CLOCK.

**Return:** `TriggerSource` — The publisher this is a trigger for.

```javascript
const triggers = ScriptApp.getProjectTriggers();
for (let i = 0; i < triggers.length; i++) {
  if (triggers[i].getTriggerSource() === ScriptApp.TriggerSource.CLOCK) {
    Logger.log(`${triggers[i].getUniqueId()} source is clock`);
  } else if (
      triggers[i].getTriggerSource() === ScriptApp.TriggerSource.SPREADSHEETS) {
    Logger.log(`${triggers[i].getUniqueId()} source is spreadsheets`);
  }
}
```

### getTriggerSourceId() → String

Returns the id specific to the source. For example, if the trigger source is a spreadsheet, this is the id of the spreadsheet. For clock events this returns `null`.

**Return:** `String` — The id of the entity in the publisher that this is a trigger for.

### getUniqueId() → String

Returns a unique identifier that can be used to distinguish triggers from each other.

**Return:** `String` — The unique identifier of the trigger.
