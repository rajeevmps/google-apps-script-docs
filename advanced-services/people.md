# Advanced People Service

Source: https://developers.google.com/apps-script/advanced/people

## Overview

The Advanced People Service leverages the People API in Google Apps Script to manage contact and profile data. As stated in the documentation: "This API lets scripts create, read, and update contact data for the logged in user and read profile data for Google users."

This is an advanced service requiring explicit enablement before use.

## Key Features

- Create, read, and update contact information
- Access user profile data for Google Accounts
- Retrieve user connections and contacts
- Uses the same objects, methods, and parameters as the public People API

## Enabling the Service

The Advanced People Service must be enabled before use. Follow the standard procedure for enabling advanced services in Apps Script.

## Sample Code

### Get User Connections

```javascript
/**
 * Gets a list of people in the user's contacts.
 * @see https://developers.google.com/people/api/rest/v1/people.connections/list
 */
function getConnections() {
  try {
    const people = People.People.Connections.list("people/me", {
      personFields: "names,emailAddresses",
    });
    console.log("Connections: %s", JSON.stringify(people, null, 2));
  } catch (err) {
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

### Get User's Own Profile

Requires the `https://www.googleapis.com/auth/userinfo.profile` scope in `appsscript.json`:

```javascript
/**
 * Gets the own user's profile.
 * @see https://developers.google.com/people/api/rest/v1/people/getBatchGet
 */
function getSelf() {
  try {
    const people = People.People.getBatchGet({
      resourceNames: ["people/me"],
      personFields: "names,emailAddresses",
    });
    console.log("Myself: %s", JSON.stringify(people, null, 2));
  } catch (err) {
    console.log("Failed to get own profile with an error %s", err.message);
  }
}
```

### Get Any Google Account Information

```javascript
/**
 * Gets the person information for any Google Account.
 * @param {string} accountId The account ID.
 * @see https://developers.google.com/people/api/rest/v1/people/get
 */
function getAccount(accountId) {
  try {
    const people = People.People.get(`people/${accountId}`, {
      personFields: "names,emailAddresses",
    });
    console.log("Public Profile: %s", JSON.stringify(people, null, 2));
  } catch (err) {
    console.log("Failed to get account with an error %s", err.message);
  }
}
```

## Reference

For detailed information, consult the [People API reference documentation](https://developers.google.com/people/api/rest) (external — not scraped). Support is available through the [People v1 support guide](https://developers.google.com/people/support) (external — not scraped).
</content>
