# GmailLabel

A user-created label in a user's Gmail account.

A user-created label in a user's Gmail account. The class provides methods to manage labels, including adding/removing them from threads, deleting labels, retrieving label information, and accessing associated threads.

## Methods

### addToThread(thread)
**Parameters:** `thread` (GmailThread)
**Return type:** `GmailLabel`

Adds this label to the given thread and forces the thread to refresh (`GmailThread.refresh()`).

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
label.addToThread(firstThread);
```

### addToThreads(threads)
**Parameters:** `threads` (GmailThread[])
**Return type:** `GmailLabel`

Adds this label to the given threads and forces the threads to refresh. You can add labels for up to 100 threads per batch.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const threads = GmailApp.getInboxThreads(0, 3);
label.addToThreads(threads);
```

### deleteLabel()
**Return type:** `void`

Deletes this label. Throws Error if the label cannot be deleted.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
label.deleteLabel();
```

### getId()
**Return type:** `String`

Gets the id of this label.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
console.log(label.getId());
```

### getName()
**Return type:** `String`

Gets the name of this label.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
Logger.log(label.getName());  // logs MyLabel
```

### getThreads()
**Return type:** `GmailThread[]`

Gets the threads that are marked with this label. This call fails when the size of all threads is too large for the system to handle. Where the thread size is unknown, and potentially very large, please use `getThreads(start, max)` and specify ranges.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const threads = label.getThreads();
for (let i = 0; i < threads.length; i++) {
  Logger.log(threads[i].getFirstMessageSubject());
}
```

### getThreads(start, max)
**Parameters:** `start` (Integer), `max` (Integer)
**Return type:** `GmailThread[]`

Gets a range of threads marked with this label.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const threads = label.getThreads(0, 30);
for (let i = 0; i < threads.length; i++) {
  Logger.log(threads[i].getFirstMessageSubject());
}
```

### getUnreadCount()
**Return type:** `Integer`

Gets the number of unread threads tagged with this label.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
Logger.log(label.getUnreadCount());
```

### removeFromThread(thread)
**Parameters:** `thread` (GmailThread)
**Return type:** `GmailLabel`

Removes this label from the given thread and forces the thread to refresh.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const firstThread = GmailApp.getInboxThreads(0, 1)[0];
label.removeFromThread(firstThread);
```

### removeFromThreads(threads)
**Parameters:** `threads` (GmailThread[])
**Return type:** `GmailLabel`

Removes this label from the given threads and forces the threads to refresh. You can remove labels for up to 100 threads per batch.

```javascript
const label = GmailApp.getUserLabelByName('MyLabel');
const threads = GmailApp.getInboxThreads(0, 3);
label.removeFromThreads(threads);
```
