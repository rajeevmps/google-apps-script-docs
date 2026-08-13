# Migrate from Groups Service to Cloud Identity Groups Advanced Service

## Page Summary

- Cloud Identity Groups (CIG) Advanced Service provides equivalent functionality to the Groups Service API.
- You must enable CIG Advanced Service in your script project to use it.
- Helper methods are provided to demonstrate how to achieve equivalent capabilities to the Groups Service API using CIG Advanced Service.
- In this guide, "group" refers to a Group Resource, which is a JavaScript object without methods but can be used to retrieve information similar to Group Class objects.

Cloud Identity Groups (CIG) Advanced Service provides feature parity to the [Groups Service API](https://developers.google.com/apps-script/reference/groups) and can be used in its stead.

See the helper methods provided to learn how to achieve equivalent capabilities through CIG Advanced Service.

## Setup

To use CIG Advanced Service, first [enable it](https://developers.google.com/apps-script/guides/services/advanced#enable_advanced_services) within your script project.

To shorten some of the method signatures in this guide, we defined the following variable:

```javascript
const groups = CloudIdentityGroups.Groups;
```

## GroupsApp Methods

The following helper methods correspond to those of the Groups Service [`GroupsApp`](https://developers.google.com/apps-script/reference/groups/groups-app).

In this guide, the term _group_ refers to a [Group Resource](https://cloud.google.com/identity/docs/reference/rest/v1/groups#resource:-group), as opposed to a [Group Class](https://developers.google.com/apps-script/reference/groups/group) object. [Group Resources](https://cloud.google.com/identity/docs/reference/rest/v1/groups#resource:-group) are JavaScript objects that don't have methods, but they can be used in CIG Advanced Service to retrieve similar information to that in [Group Class](https://developers.google.com/apps-script/reference/groups/group) objects.

### getGroupByEmail

```javascript
/**
 * Given a group's email, returns that group's resource
 *
 * @param {String} email: The email address to lookup a group by
 * @return {Group} group: The group resource associated with the email
 */
function groupsAppGetGroupByEmail(email) {
  // Retrieve the name ID of the group
  const groupName = groups.lookup({
    'groupKey.id': email,
    'groupKey.namespace': ''  // Optional for google groups, dynamic groups, and security groups
                              // Necessary for identity-mapped groups (see https://developers.google.com/cloud-search/docs/guides/identity-mapping)
  }).name;

  // Retrieve the group resource
  return groups.get(groupName);
}
```

### getGroups

The following helper method returns a list of [Membership Resources](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships#resource:-membership). Access the `group` field of an element to find its name ID. This is useful for many methods of CIG Advanced Service. Similarly, access `groupKey.id` of an element to find its email.

```javascript
/**
 * Retrieves all the membership relation resources to groups which you are a
 * direct member (or a pending member).
 *
 * @return {Array<MembershipRelation>} groups : List of direct memberships where
 * you are the member.
 */
function groupsAppGetGroups() {
  const myEmail = Session.getActiveUser().getEmail();
  let pageToken = '';
  let membershipList = [];

  do {
    const queryParams = {
      query:`member_key_id=='${myEmail}'`,
      pageToken:pageToken
    };
    const searchResult = groups.Memberships.searchDirectGroups('groups/-', queryParams);
    membershipList = membershipList.concat(searchResult.memberships);
    pageToken = searchResult.nextPageToken;
  } while (pageToken);

  return membershipList;
}
```

## Group Methods

The following helper methods correspond to those of the Groups Service [`Group` Class](https://developers.google.com/apps-script/reference/groups/group).

### getEmail

```javascript
/**
 * Gets a group's email address
 *
 * @param {Object} group: A group resource
 * @return {String} email: The email associated with the group resource.
 */
function getEmail(group) {
  return group.groupKey.id;
}
```

### getGroups

The following method uses [`Memberships.list`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships/list), which will fetch every membership to the given group. This can include memberships of users as well as groups.

To better approximate the Groups Service [`getGroups`](https://developers.google.com/apps-script/reference/groups/group#getGroups()) method, we can filter memberships by their [`Type`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships#type). We get access to this field by either providing a `FULL` [`View`](https://cloud.google.com/identity/docs/reference/rest/v1/View) as a query parameter to [`Memberships.list`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships/list) or by performing an individual [`Memberships.lookup`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships/lookup) for each given membership.

```javascript
/**
 * Fetch a list of memberships with provided group as its parent
 *
 * @param {Group} group: A group resource
 * @return {Array<Membership>} membershipList: The memberships where the parent
 * is the provided group and member is a also a group.
 */
function getGroups(group) {
  let membershipList = [];
  let pageToken = '';

  do {
    // Fetch a page of memberships
    const queryParams = {
      view: 'FULL',
      pageToken: pageToken
    }
    const response = groups.Memberships.list(group.name, queryParams);

    // Filter non-group memberships
    const onlyGroupMemberships = response.memberships.filter(
      membership => membership.type == 'GROUP'
    );
    membershipList = membershipList.concat(onlyGroupMemberships);

    // Set up next page
    pageToken = response.nextPageToken;
  } while(pageToken);

  return membershipList;
}
```

### getRole and getRoles

While Groups Service might have only returned the highest priority role in `getRole`, the `roles` field in a membership resource contains a separate element for each role the member qualifies for (example: MEMBER, OWNER, ADMIN).

```javascript
/**
 * Retrieve the membership roles of a member to a group.
 *
 * @param {Group} containingGroup: The group whom the member belongs to
 * @param {String} email: The email address associated with a member that
 * belongs to the containingGroup
 * @return {Array<Role>} roles: List of roles the member holds with respect to
 * the containingGroup.
 */
function getRoleWithEmail(containingGroup, email) {
  // First fetch the membership
  const membershipName = groups.Memberships.lookup(containingGroup.name, { 'memberKey.id': email }).name;
  const membership = groups.Memberships.get(membershipName);

  // Then retrieve the role
  return membership.roles;
}

/**
 * Retrieve the membership roles of a member to a group.
 *
 * @param {Group} containingGroup: The group resource whom the member belongs to
 * @param {User} user: The user associated with a member that belongs to the
 * containingGroup
 * @return {Array<Role>} roles: List of roles the member holds with respect to
 * the containingGroup
 */
function getRoleWithUser(containingGroup, user) {
  return getRoleWithEmail(containingGroup, user.getEmail());
}

/**
 * Retrieve the membership roles of a group of members to a group
 *
 * @param {Group} containingGroup: The group resource to which roles are
 * relevant
 * @param {Array<User>} users: List of users to fetch roles from
 * @return {Array<Array<Role>>} roles: A list where every element is a list of
 * roles of member to the containingGroup
 */
function getRoles(containingGroup, users) {
  let roles = [];
  for (const user of users) {
    roles.push(getRoleWithUser(containingGroup, user));
  }
  return roles;
}
```

### getUsers

Similarly to our approach in [getGroups](#get-groups-header), we can fetch a group's memberships with [`Memberships.list`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships/list) and filter the results to only keep our target [`Type`](https://cloud.google.com/identity/docs/reference/rest/v1/groups.memberships#type).

```javascript
/**
 * Given a group, retrieve its direct members and banned members of the group
 * that have a known corresponding Google Account.
 *
 * @param {Group} group: The group Resource whom the users being queried belong
 * to
 * @return {Array<String>} users: A list of emails associated with members of
 * the given group
 */
function getUsers(group) {
  let userList = [];
  let pageToken = '';

  do {
    // Fetch a page of memberships from the group
    const queryParams = {
      view: 'FULL',
      pageToken: pageToken
    }
    const listResponse = groups.Memberships.list(group.name, queryParams);

    // Filter non-users and keep member emails
    const users = listResponse.memberships
      .filter(membership => membership.type == 'USER')
      .map(membership => membership.preferredMemberKey.id);
    userList = userList.concat(users);

    // Prepare next page
    pageToken = listResponse.nextPageToken;
  } while (pageToken);

  return userList;
}
```

### hasGroup and hasUser

Both Groups Service [`hasGroup`](https://developers.google.com/apps-script/reference/groups/group#hasgroupemail) and [`hasUser`](https://developers.google.com/apps-script/reference/groups/group#hasuseremail) confirm whether an entity is a member to a given group. Given that both a Group and a User can be represented by an email address, the following method can be used to confirm whether either belongs to a given group.

```javascript
/**
 * Tests if the given email has an associated direct member to the given group.
 *
 * @param {Group} group: Group resource to which the entity is checked as
 * a member
 * @param {String} email: Email that can represent a Group or User entity
 * @return {Boolean} isMember: Whether the entity is a direct member to the
 * group or not
 */
function checkDirectGroupMembership(group, email) {
  try {
    groups.Memberships.lookup(group.name, {'memberKey.id': email});

  } catch(e) {
    // Log failure if exception is not related to membership existence
    if (!e.message.includes('Membership does not exist.')) {
      console.error(e);
    }
    return false;
  }
  return true;
}
```

Source: https://developers.google.com/apps-script/migration/groups-cig
