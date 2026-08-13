# EventGuest

Represents a guest of an event.

Represents a guest of an event. The EventGuest object provides methods to retrieve information about a guest, including the number of additional guests, email address, guest status, and name.

All methods require authorization with one or more of these scopes:
- `https://www.googleapis.com/auth/calendar`
- `https://www.googleapis.com/auth/calendar.readonly`
- `https://www.google.com/calendar/feeds`

## Methods

### getAdditionalGuests()
**Return type:** `Integer`

Gets the number of additional people that this guest has said are attending.

Returns: the number of additional people this guest has said are attending.

### getEmail()
**Return type:** `String`

Gets the email address of the guest.

Returns: the guest's email address.

### getGuestStatus()
**Return type:** `GuestStatus`

Gets the status of the guest for the event.

Returns: the status of this guest.

### getName()
**Return type:** `String`

Gets the name of the guest. If the name of the guest is not available, this method returns the guest's email address.

Returns: the guest's name, or the guest's email address if the name is not available.

### getStatus() — Deprecated
**Return type:** `String`

Deprecated. This function is deprecated and should not be used in new scripts. Use `getGuestStatus()` instead.

Gets the status of the guest for the event.

Returns: the status of this guest.
