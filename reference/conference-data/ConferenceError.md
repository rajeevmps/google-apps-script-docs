# ConferenceError

Error that occurred in a conferencing add-on.

Error that occurred in a conferencing add-on. The ConferenceError class represents errors in conferencing add-ons, allowing developers to specify error types and authentication URLs when needed.

## Methods

### setConferenceErrorType(conferenceErrorType)

**Signature:** `setConferenceErrorType(conferenceErrorType: ConferenceErrorType): ConferenceError`

**Description:** Sets the error type of this ConferenceError. Returns this object, for chaining.

### setAuthenticationUrl(authenticationUrl)

**Signature:** `setAuthenticationUrl(authenticationUrl: String): ConferenceError`

**Description:** If the error type is AUTHENTICATION, the add-on must provide a URL calling back into the add-on to allow users to log in. The maximum length for this field is 1800 characters. Returns this object, for chaining. Throws an error if the provided URL is not a valid http/https URL or is too long.

## Code Samples

Basic error creation:
```javascript
const conferenceError = ConferenceDataService.newConferenceError()
    .setConferenceErrorType(ConferenceDataService.ConferenceErrorType.PERMANENT);
```

With authentication URL:
```javascript
const state = ScriptApp.newStateToken()
    .withMethod('myLoginCallbackFunction')
    .withTimeout(3600)
    .createToken();

const authenticationUrl = `https://script.google.com/a/google.com/d/${
    ScriptApp.getScriptId()}/usercallback?state=${state}`;

const conferenceError = ConferenceDataService.newConferenceError()
    .setConferenceErrorType(ConferenceDataService.ConferenceErrorType.AUTHENTICATION)
    .setAuthenticationUrl(authenticationUrl);
```
