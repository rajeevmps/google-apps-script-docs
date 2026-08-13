# EntryPoint

Definition of a specific way to join a conference.

Definition of a specific way to join a conference that enables configuration of various conference entry methods including video, phone, and SIP connections.

## Methods

### addFeature(feature)

**Signature:** `addFeature(feature: EntryPointFeature): EntryPoint`

**Description:** Adds the feature of the entry point, such as being toll or toll-free. Throws an error if the feature isn't applicable to the entry point type.

### setAccessCode(accessCode)

**Signature:** `setAccessCode(accessCode: String): EntryPoint`

**Description:** An access code for accessing the conference. Maximum length 128 characters. Optional. Throws an error if the provided access code exceeds length limits.

### setEntryPointType(entryPointType)

**Signature:** `setEntryPointType(entryPointType: EntryPointType): EntryPoint`

**Description:** Sets the type of this entry point. Required.

### setMeetingCode(meetingCode)

**Signature:** `setMeetingCode(meetingCode: String): EntryPoint`

**Description:** A meeting code for accessing the conference. Maximum length 128 characters. Optional. Throws an error if the code exceeds length limits.

### setPasscode(passcode)

**Signature:** `setPasscode(passcode: String): EntryPoint`

**Description:** A passcode for accessing the conference. Maximum length 128 characters. Optional. Throws an error if the passcode exceeds length limits.

### setPassword(password)

**Signature:** `setPassword(password: String): EntryPoint`

**Description:** A password code for accessing the conference. Maximum length 128 characters. Optional. Throws an error if the password exceeds length limits.

### setPin(pin)

**Signature:** `setPin(pin: String): EntryPoint`

**Description:** A PIN code for accessing the conference. Maximum length 128 characters. Optional. Throws an error if the PIN exceeds length limits.

### setRegionCode(regionCode)

**Signature:** `setRegionCode(regionCode: String): EntryPoint`

**Description:** The CLDR/ISO 3166 region code for the country associated with this entry point. Applicable only to phone entry point types. Optional.

### setUri(uri)

**Signature:** `setUri(uri: String): EntryPoint`

**Description:** Sets the URI for joining the conference through this entry point. Requires appropriate prefixes (tel:, sip:, http:, or https:) depending on type. Maximum length 1300 characters. Required. Throws an error if the URI is malformed.
