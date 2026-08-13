# ConferenceParameter

A solution-specific parameter for add-ons that is persisted with conference data.

A ConferenceParameter is a solution-specific parameter for add-ons that is persisted with conference data. These parameters can be updated or deleted and are passed to the add-on for such operations.

## Code Sample

```javascript
const conferenceParameter = ConferenceDataService.newConferenceParameter()
                                .setKey('meetingId')
                                .setValue('123456');
```

## Methods

### setKey(key)

**Signature:** `setKey(key: String): ConferenceParameter`

**Description:** Establishes the key identifier for this ConferenceParameter, with a limit of 50 characters maximum length. This field is required. Returns the current ConferenceParameter object, enabling method chaining. Throws an error if the supplied key exceeds the character limit.

### setValue(value)

**Signature:** `setValue(value: String): ConferenceParameter`

**Description:** Establishes the value for this ConferenceParameter, with a limit of 1024 characters maximum length. This field is required. Returns the current ConferenceParameter object, enabling method chaining. Throws an error if the supplied value exceeds the character limit.
