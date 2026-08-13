# ConferenceData

Container for all conference-related information.

Container for all conference-related information. The ConferenceData class holds conference details and can be constructed using `ConferenceDataService.newConferenceDataBuilder()`. It supports adding entry points and conference parameters.

## Methods

### printJson()

**Signature:** `printJson(): String`

**Description:** Prints the JSON representation of this object. This is for debugging only.

## Code Sample

```javascript
let conferenceId;
const entryPoint = ConferenceDataService.newEntryPoint();
const conferenceParameter = ConferenceDataService.newConferenceParameter();
const conferenceData = ConferenceDataService.newConferenceDataBuilder()
                           .setConferenceId(conferenceId)
                           .addEntryPoint(entryPoint)
                           .addConferenceParameter(conferenceParameter)
                           .build();
```

Note: `printJson()` is the only public method on ConferenceData itself. Builder methods like `setConferenceId()`, `addEntryPoint()`, and `addConferenceParameter()` belong to the [ConferenceDataBuilder](./ConferenceDataBuilder.md) class.
