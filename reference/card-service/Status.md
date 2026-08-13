# Status

An enum that represents the status code.

An enum that represents the status code. Only available for Google Chat apps. Not available for Google Workspace add-ons.

To call an enum, you call its parent class, name, and property. For example, `CardService.Status.OK`.

## Properties

### OK
HTTP Mapping: 200 OK

### CANCELLED
HTTP Mapping: 499 Client Closed Request

### UNKNOWN
Unknown error. HTTP Mapping: 500 Internal Server Error

### INVALID_ARGUMENT
The client specified an invalid argument. HTTP Mapping: 400 Bad Request

### DEADLINE_EXCEEDED
HTTP Mapping: 504 Gateway Timeout

### NOT_FOUND
HTTP Mapping: 404 Not Found

### ALREADY_EXISTS
The entity that a client attempted to create already exists. HTTP Mapping: 409 Conflict

### PERMISSION_DENIED
HTTP Mapping: 403 Forbidden

### UNAUTHENTICATED
HTTP Mapping: 401 Unauthorized

### RESOURCE_EXHAUSTED
HTTP Mapping: 429 Too Many Requests

### FAILED_PRECONDITION
The operation was rejected because the system is not in a state required for the operation's execution. HTTP Mapping: 400 Bad Request

### ABORTED
The operation was aborted, typically due to a concurrency issue such as a sequencer check failure or transaction abort. HTTP Mapping: 409 Conflict

### OUT_OF_RANGE
The operation was attempted past the valid range. HTTP Mapping: 400 Bad Request

### UNIMPLEMENTED
HTTP Mapping: 501 Not Implemented

### INTERNAL
Internal errors. This means that some invariants expected by the underlying system have been broken. This error code is reserved for serious errors. HTTP Mapping: 500 Internal Server Error

### UNAVAILABLE
HTTP Mapping: 503 Service Unavailable

### DATA_LOSS
Unrecoverable data loss or corruption. HTTP Mapping: 500 Internal Server Error
