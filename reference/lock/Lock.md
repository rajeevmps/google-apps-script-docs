# Lock

A representation of a mutual-exclusion lock.

A representation of a mutual-exclusion lock. This class lets scripts make sure that only one instance of the script executes a given section of code at a time. It is particularly useful for callbacks and triggers, where a user action might cause changes to a shared resource and you want to ensure that there aren't collisions.

## Methods

### hasLock() → Boolean

Returns `true` if the lock was acquired. This method returns `false` if `tryLock(timeoutInMillis)` or `waitLock(timeoutInMillis)` were never called, timed out before the lock could be retrieved, or if `releaseLock()` was called.

### releaseLock() → void

Releases the lock, allowing other processes waiting on the lock to continue. The lock is automatically released when the script terminates, but for efficiency it is best to release it as soon as you no longer need exclusive access to a section of code. This method has no effect if the lock has not been acquired.

Note: if you are working with a spreadsheet, you should call SpreadsheetApp.flush() prior to releasing the lock, to commit all pending changes to the spreadsheet while you still have exclusive access to it.

### tryLock(timeoutInMillis: Integer) → Boolean

Attempts to acquire the lock, timing out after the provided number of milliseconds. This method has no effect if the lock has already been acquired.

### waitLock(timeoutInMillis: Integer) → void

Attempts to acquire the lock, timing out with an exception after the provided number of milliseconds. This method is the same as `tryLock(timeoutInMillis)` except that it throws an exception when the lock could not be acquired instead of returning `false`.

Throws: `Error` — if the method timed out before the lock was acquired.

## Properties

None.

## Code Example

```javascript
// Generates a unique ticket number for every form submission.
function onFormSubmit(e) {
  const targetCell = e.range.offset(0, e.range.getNumColumns(), 1, 1);

  // Gets a script lock before modifying a shared resource.
  const lock = LockService.getScriptLock();
  // Waits for up to 30 seconds for other processes to finish.
  lock.waitLock(30000);

  const scriptProperties = PropertiesService.getScriptProperties();

  const ticketNumber =
      Number(scriptProperties.getProperty('lastTicketNumber')) + 1;
  scriptProperties.setProperty('lastTicketNumber', ticketNumber);

  // Releases the lock so that other processes can continue.
  lock.releaseLock();

  targetCell.setValue(ticketNumber);
}
```
