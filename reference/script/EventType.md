# EventType

An enumeration denoting the type of triggered event.

An enumeration denoting the type of triggered event. To call an enum, you call its parent class, name, and property. For example, `ScriptApp.EventType.CLOCK`.

## Properties

### CLOCK

The trigger fires once the time-driven event reaches a specific time.

### ON_OPEN

The trigger fires once the user opens the Google Docs, Sheets, or Forms file.

### ON_EDIT

The trigger fires once the user edits the Google Sheets file (for example, by entering a new value into a cell, which counts as an edit instead of a change).

### ON_FORM_SUBMIT

The trigger fires once the user responds to a Google Form. This trigger is available either in the Google Form itself or in the Google Sheets file that the form sends its responses to.

### ON_CHANGE

The trigger fires once the user changes the Google Sheets file (for example, by adding a row, which counts as a change instead of an edit).

### ON_EVENT_UPDATED

The trigger fires once an event gets created, updated, or deleted on the specified Google Calendar.
