# ContactsApp

Allows users to access their own Google Contacts and create, remove, and update contacts. (Deprecated)

**Deprecated.** Use the [People API advanced service](https://developers.google.com/apps-script/advanced/people) instead.

This class allows users to access their own Google Contacts and create, remove, and update contacts listed therein.

## Properties

| Property | Type |
|----------|------|
| `ExtendedField` | `ExtendedField` |
| `Field` | `Field` |
| `Gender` | `Gender` |
| `Month` | `Month` |
| `Priority` | `Priority` |
| `Sensitivity` | `Sensitivity` |

## Methods

All methods below are deprecated. Requires authorization scope `https://www.google.com/m8/feeds`.

### createContact(givenName, familyName, email)

**Signature:** `createContact(givenName: String, familyName: String, email: String): Contact`

**Description:** Creates a new contact.

### createContactGroup(name)

**Signature:** `createContactGroup(name: String): ContactGroup`

**Description:** Creates a contact group with the given name.

### deleteContact(contact)

**Signature:** `deleteContact(contact: Contact): void`

**Description:** Deletes the contact.

### deleteContactGroup(group)

**Signature:** `deleteContactGroup(group: ContactGroup): void`

**Description:** Deletes the contact group.

### findByEmailAddress(email)

**Signature:** `findByEmailAddress(email: String): Contact`

**Description:** Finds a Contact with the given email address.

### findContactGroup(name)

**Signature:** `findContactGroup(name: String): ContactGroup`

**Description:** Finds a contact group of the given name.

### getAllContacts()

**Signature:** `getAllContacts(): Contact[]`

**Description:** Get all the contacts belonging to this user.

### getContact(emailAddress)

**Signature:** `getContact(emailAddress: String): Contact`

**Description:** Gets a contact by the email address. Favors contacts with marked-primary email addresses when multiple contacts share the same email.

### getContactById(id)

**Signature:** `getContactById(id: String): Contact`

**Description:** Gets the contact with this id. Returns matching contact or null.

### getContactGroup(name)

**Signature:** `getContactGroup(name: String): ContactGroup`

**Description:** Gets a contact group with the given name, or returns null if no such contact group is found.

### getContactGroupById(id)

**Signature:** `getContactGroupById(id: String): ContactGroup`

**Description:** Gets a contact group with the given id, or returns null if no such contact group is found.

### getContactGroups()

**Signature:** `getContactGroups(): ContactGroup[]`

**Description:** Gets the complete list of the user's contact groups. Returns array of all user's contact groups.

### getContacts()

**Signature:** `getContacts(): Contact[]`

**Description:** Gets all of the user's contacts. Returns array containing all user contacts.

### getContactsByAddress(query)

**Signature:** `getContactsByAddress(query: String): Contact[]`

**Description:** Get contacts matching an address.

### getContactsByAddress(query, label)

**Signature:** `getContactsByAddress(query: String, label: Field): Contact[]`

**Description:** Get contacts matching an address, limited to a specific field.

### getContactsByAddress(query, label) [custom label]

**Signature:** `getContactsByAddress(query: String, label: String): Contact[]`

**Description:** Get contacts matching an address, limited to the specified custom address label.

### getContactsByCompany(query)

**Signature:** `getContactsByCompany(query: String): Contact[]`

**Description:** Get contacts matching the company field.

### getContactsByCustomField(query, label)

**Signature:** `getContactsByCustomField(query: String, label: String): Contact[]`

**Description:** Get contacts matching a given value in a custom field.

### getContactsByDate(month, day, label)

**Signature:** `getContactsByDate(month: Month, day: Integer, label: Field): Contact[]`

**Description:** Get contacts matching a given month and day for a particular standard field.

### getContactsByDate(month, day, year, label) [standard field]

**Signature:** `getContactsByDate(month: Month, day: Integer, year: Integer, label: Field): Contact[]`

**Description:** Get contacts matching a given month, day, and year for a particular standard field.

### getContactsByDate(month, day, year, label) [custom field]

**Signature:** `getContactsByDate(month: Month, day: Integer, year: Integer, label: String): Contact[]`

**Description:** Get contacts matching a given month, day, and year for a particular custom field.

### getContactsByDate(month, day, label) [custom field]

**Signature:** `getContactsByDate(month: Month, day: Integer, label: String): Contact[]`

**Description:** Get contacts matching a given month and day for a particular custom field.

### getContactsByEmailAddress(query)

**Signature:** `getContactsByEmailAddress(query: String): Contact[]`

**Description:** Get contacts matching an email address.

### getContactsByEmailAddress(query, label) [standard field]

**Signature:** `getContactsByEmailAddress(query: String, label: Field): Contact[]`

**Description:** Get contacts matching an email address, limited to a specific field.

### getContactsByEmailAddress(query, label) [custom label]

**Signature:** `getContactsByEmailAddress(query: String, label: String): Contact[]`

**Description:** Get contacts matching an email address, limited to the specified custom email address label.

### getContactsByGroup(group)

**Signature:** `getContactsByGroup(group: ContactGroup): Contact[]`

**Description:** Get the contacts in a given ContactGroup.

### getContactsByIM(query)

**Signature:** `getContactsByIM(query: String): Contact[]`

**Description:** Get contacts matching an instant messaging address.

### getContactsByIM(query, label) [standard field]

**Signature:** `getContactsByIM(query: String, label: Field): Contact[]`

**Description:** Get contacts matching an instant messaging address, limited to a specific field.

### getContactsByIM(query, label) [custom label]

**Signature:** `getContactsByIM(query: String, label: String): Contact[]`

**Description:** Get contacts matching an instant messaging address, limited to the specified custom instant messaging label.

### getContactsByJobTitle(query)

**Signature:** `getContactsByJobTitle(query: String): Contact[]`

**Description:** Get contacts matching the job title field.

### getContactsByName(query)

**Signature:** `getContactsByName(query: String): Contact[]`

**Description:** Get contacts matching the name field(s).

### getContactsByName(query, label)

**Signature:** `getContactsByName(query: String, label: Field): Contact[]`

**Description:** Get contacts matching the name field, limited to a specific standard field.

### getContactsByNotes(query)

**Signature:** `getContactsByNotes(query: String): Contact[]`

**Description:** Get contacts matching the notes field.

### getContactsByPhone(query)

**Signature:** `getContactsByPhone(query: String): Contact[]`

**Description:** Get contacts matching a phone number.

### getContactsByPhone(query, label) [standard field]

**Signature:** `getContactsByPhone(query: String, label: Field): Contact[]`

**Description:** Get contacts matching a phone number, limited to a specific field.

### getContactsByPhone(query, label) [custom label]

**Signature:** `getContactsByPhone(query: String, label: String): Contact[]`

**Description:** Get contacts matching a phone number, limited to the specified custom phone number label.

### getContactsByUrl(query)

**Signature:** `getContactsByUrl(query: String): Contact[]`

**Description:** Get contacts matching a URL.

### getContactsByUrl(query, label) [standard field]

**Signature:** `getContactsByUrl(query: String, label: Field): Contact[]`

**Description:** Get contacts matching a URL, limited to a specific field.

### getContactsByUrl(query, label) [custom label]

**Signature:** `getContactsByUrl(query: String, label: String): Contact[]`

**Description:** Get contacts matching a URL, limited to the specified custom URL label.

## Code Samples

The reference page includes examples for `createContact` (creating contact "John Doe" with email "john.doe@example.com"), `createContactGroup` (creating group "Work Friends"), `deleteContact` (retrieving then deleting a contact by email address), and `deleteContactGroup` (retrieving and deleting the group named "Work Friends").
