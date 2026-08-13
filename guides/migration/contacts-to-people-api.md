# Migrate from Contacts service to People API advanced service

## Page Summary

- You must migrate your scripts from the Contacts service to the People API advanced service before the Contacts service shuts down on January 31, 2025.
- The People API advanced service uses a newer JSON protocol and offers advanced features not available in the Contacts service.
- While some Contacts service search methods lack direct People API equivalents, you can still search by fields like names, email addresses, and phone numbers.
- The People API advanced service provides additional features like specifying data sources, searching by query strings, and batch requests.
- Code samples are provided for common tasks to assist with migrating from the Contacts service to the People API advanced service.

Google Apps Script deprecated the Contacts service on **December 16, 2022** and shut down the service on **January 31, 2025**.

Instead, use the [People API advanced service](https://developers.google.com/apps-script/advanced/people). The People API uses a newer JSON protocol and provides advanced features, like merging contacts with profiles.

Use this guide to learn which Contacts service methods have no equivalent in the People API advanced service, learn what you can use instead, and find code samples for migrating common tasks. For more information, refer to the [Contacts API Migration Guide](https://developers.google.com/people/contacts-api-migration).

## Methods without People API equivalents

The following lists `getContacts` methods in the Contacts service that don't have equivalent ways to search for contacts in the People API advanced service. With the People API advanced service, you can search by a contact's `names`, `nickNames`, `emailAddresses`, `phoneNumbers`, and `organizations` fields that are from the [`CONTACT`](https://developers.google.com/people/api/rest/v1/people#Person.SourceType) source.

### Methods without equivalents

- `getContactsByAddress(query)`
- `getContactsByAddress(query, label)`
- `getContactsByAddress(query, label)`
- `getContactsByCustomField(query, label)`
- `getContactsByDate(month, day, label)`
- `getContactsByDate(month, day, year, label)`
- `getContactsByDate(month, day, year, label)`
- `getContactsByIM(query)`
- `getContactsByIM(query, label)`
- `getContactsByJobTitle(query)`
- `getContactsByNotes(query)`
- `getContactsByUrl(query)`
- `getContactsByUrl(query, label)`
- `getContactsByGroup(group)`

The following table lists `getContacts` methods from the Contacts service that use an extra `label` parameter. Although the People API advanced service lets you get contacts by the equivalent field using [`searchContacts`](https://developers.google.com/people/api/rest/v1/people/searchContacts), you can't limit the search to a specific label.

### Methods with partial equivalents

- `getContactsByEmailAddress(query, label)`
- `getContactsByName(query, label)`
- `getContactsByPhone(query, label)`

## Additional features available with People API

When you migrate to the People API advanced service, you can access the following People API features that aren't available in the Contacts service:

- [Specify the data source](https://developers.google.com/people/api/rest/v1/people#sourcetype) – When you search for information about a person, you can specify where to search, such as a Google contact or a Google profile.
- [Search for people by a query string](https://developers.google.com/people/v1/directory#search_the_directory_people) – You can get a list of profiles and contacts that match a specific string.
- [Batch requests](https://developers.google.com/people/v1/batch) – You can batch your People API calls to help reduce your script execution time.

## Code samples for common tasks

This section lists common tasks from the Contacts service. The code samples show how to construct the tasks using the People API advanced service.

### Get a contact group by name

The following code sample shows how to get a contact group by its name, which is the equivalent to `getContactGroup` in the Contacts service.

```javascript
/**
 * Gets a contact group with the given name
 * @param {string} name The group name.
 * @see https://developers.google.com/people/api/rest/v1/contactGroups/list
 */
function getContactGroup(name) {
  try {
    const people = People.ContactGroups.list();
    // Finds the contact group for the person where the name matches.
    const group = people.contactGroups.find((group) => group.name === name);
    // Prints the contact group
    console.log("Group: %s", JSON.stringify(group, null, 2));
  } catch (err) {
    // TODO (developers) - Handle exception
    console.log(
      "Failed to get the contact group with an error %s",
      err.message,
    );
  }
}
```

### Get a contact by email address

The following code sample shows how to get a contact by their email address, which is the equivalent to `getContact` in the Contacts service.

```javascript
/**
 * Gets a contact by the email address.
 * @param {string} email The email address.
 * @see https://developers.google.com/people/api/rest/v1/people.connections/list
 */
function getContactByEmail(email) {
  try {
    // Gets the person with that email address by iterating over all contacts.
    const people = People.People.Connections.list("people/me", {
      personFields: "names,emailAddresses",
    });
    const contact = people.connections.find((connection) => {
      return connection.emailAddresses.some(
        (emailAddress) => emailAddress.value === email,
      );
    });
    // Prints the contact.
    console.log("Contact: %s", JSON.stringify(contact, null, 2));
  } catch (err) {
    // TODO (developers) - Handle exception
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

### Get all contacts

The following code sample shows how to get all of a user's contacts, which is the equivalent to `getContacts` in the Contacts service.

```javascript
/**
 * Gets a list of people in the user's contacts.
 * @see https://developers.google.com/people/api/rest/v1/people.connections/list
 */
function getConnections() {
  try {
    // Get the list of connections/contacts of user's profile
    const people = People.People.Connections.list("people/me", {
      personFields: "names,emailAddresses",
    });
    // Print the connections/contacts
    console.log("Connections: %s", JSON.stringify(people, null, 2));
  } catch (err) {
    // TODO (developers) - Handle exception here
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

### Get a contact's full name

The following code sample shows how to get a contact's full name, which is the equivalent to `getFullName` in the Contacts service.

```javascript
/**
 * Gets the full name (given name and last name) of the contact as a string.
 * @see https://developers.google.com/people/api/rest/v1/people/get
 */
function getFullName() {
  try {
    // Gets the person by specifying resource name/account ID
    // in the first parameter of People.People.get.
    // This example gets the person for the user running the script.
    const people = People.People.get("people/me", { personFields: "names" });
    // Prints the full name (given name + family name)
    console.log(`${people.names[0].givenName} ${people.names[0].familyName}`);
  } catch (err) {
    // TODO (developers) - Handle exception
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

### Get all phone numbers for a contact

The following code sample shows how to get all of the phone numbers for a contact, which is the equivalent to `getPhones` in the Contacts service.

```javascript
/**
 * Gets all the phone numbers for this contact.
 * @see https://developers.google.com/people/api/rest/v1/people/get
 */
function getPhoneNumbers() {
  try {
    // Gets the person by specifying resource name/account ID
    // in the first parameter of People.People.get.
    // This example gets the person for the user running the script.
    const people = People.People.get("people/me", {
      personFields: "phoneNumbers",
    });
    // Prints the phone numbers.
    console.log(people.phoneNumbers);
  } catch (err) {
    // TODO (developers) - Handle exception
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

### Get a specific phone number for a contact

The following code sample shows how to get a specific phone number for a contact, which is the equivalent to `getPhoneNumber` in the Contacts service.

```javascript
/**
 * Gets a phone number by type, such as work or home.
 * @see https://developers.google.com/people/api/rest/v1/people/get
 */
function getPhone() {
  try {
    // Gets the person by specifying resource name/account ID
    // in the first parameter of People.People.get.
    // This example gets the person for the user running the script.
    const people = People.People.get("people/me", {
      personFields: "phoneNumbers",
    });
    // Gets phone number by type, such as home or work.
    const phoneNumber = people.phoneNumbers.find(
      (phone) => phone.type === "home",
    ).value;
    // Prints the phone numbers.
    console.log(phoneNumber);
  } catch (err) {
    // TODO (developers) - Handle exception
    console.log("Failed to get the connection with an error %s", err.message);
  }
}
```

Source: https://developers.google.com/apps-script/migration/contacts-people
