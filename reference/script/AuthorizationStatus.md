# AuthorizationStatus

An enumeration denoting the authorization status of a script.

An enumeration denoting the authorization status of a script. To call an enum, you call its parent class, name, and property, e.g. `ScriptApp.AuthorizationStatus.REQUIRED`.

## Properties

### REQUIRED

The user needs to authorize this script to use one or more services. In most cases, the script prompts the user for authorization the next time it runs; however, if the script is published as an add-on that uses installable triggers, the trigger runs the script without prompting for authorization but throws an exception if the script attempts to call the unauthorized service.

### NOT_REQUIRED

The user has granted this script all the authorization it currently requires.
