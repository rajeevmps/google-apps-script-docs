# Common Use-Case Snippets

A cookbook of ready-to-adapt code for the tasks that come up most often in Apps Script projects. Each snippet is deliberately minimal — for full method-level detail, follow the link into [`reference/`](reference/README.md) or [`guides/`](guides/README.md).

## Contents

- [Spreadsheets](#spreadsheets)
- [Gmail](#gmail)
- [Drive](#drive)
- [Calendar](#calendar)
- [Docs](#docs)
- [Forms](#forms)
- [Triggers](#triggers)
- [Properties & Cache](#properties--cache)
- [UrlFetchApp (HTTP requests)](#urlfetchapp-http-requests)
- [Custom menus & UI](#custom-menus--ui)
- [Custom functions](#custom-functions)
- [Web apps (HtmlService)](#web-apps-htmlservice)
- [Locking (avoid race conditions)](#locking-avoid-race-conditions)
- [Utilities](#utilities)
- [Error handling & logging](#error-handling--logging)
- [Card Service (Add-on UI)](#card-service-add-on-ui)

---

## Spreadsheets
Reference: [`reference/spreadsheet/`](reference/spreadsheet/README.md)

**Read a range into a 2D array:**
```javascript
const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Sheet1');
const values = sheet.getRange('A1:C10').getValues(); // values[row][col]
```

**Write a 2D array back:**
```javascript
sheet.getRange(1, 1, values.length, values[0].length).setValues(values);
```

**Append a row:**
```javascript
sheet.appendRow(['Alice', 'alice@example.com', new Date()]);
```

**Loop over all rows with headers as keys:**
```javascript
const data = sheet.getDataRange().getValues();
const headers = data.shift();
const rows = data.map(row => Object.fromEntries(headers.map((h, i) => [h, row[i]])));
```

**Find a value and get its row:**
```javascript
const finder = sheet.createTextFinder('alice@example.com').findNext();
if (finder) Logger.log(finder.getRow());
```

**Format cells:**
```javascript
sheet.getRange('A1:C1').setFontWeight('bold').setBackground('#f0f0f0');
```

---

## Gmail
Reference: [`reference/gmail/`](reference/gmail/README.md), [`reference/mail/`](reference/mail/README.md)

**Send a simple email:**
```javascript
MailApp.sendEmail('someone@example.com', 'Subject', 'Plain text body');
```

**Send HTML email with attachment (prefer GmailApp for quota/threading control):**
```javascript
GmailApp.sendEmail('someone@example.com', 'Subject', 'Fallback text', {
  htmlBody: '<b>Hello</b> world',
  attachments: [DriveApp.getFileById('FILE_ID').getBlob()],
});
```

**Search and process messages:**
```javascript
const threads = GmailApp.search('is:unread from:boss@example.com', 0, 10);
threads.forEach(thread => {
  thread.getMessages().forEach(msg => Logger.log(msg.getSubject()));
  thread.markRead();
});
```

---

## Drive
Reference: [`reference/drive/`](reference/drive/README.md)

**Create a file / folder:**
```javascript
const folder = DriveApp.createFolder('Reports');
const file = folder.createFile('notes.txt', 'Hello world', MimeType.PLAIN_TEXT);
```

**Find files by name:**
```javascript
const files = DriveApp.getFilesByName('notes.txt');
while (files.hasNext()) Logger.log(files.next().getId());
```

**Move a file and share it:**
```javascript
const file = DriveApp.getFileById('FILE_ID');
file.moveTo(DriveApp.getFolderById('DEST_FOLDER_ID'));
file.setSharing(DriveApp.Access.ANYONE_WITH_LINK, DriveApp.Permission.VIEW);
```

---

## Calendar
Reference: [`reference/calendar/`](reference/calendar/README.md)

**Create an event:**
```javascript
CalendarApp.getDefaultCalendar().createEvent(
  'Team sync',
  new Date('2026-08-20T10:00:00'),
  new Date('2026-08-20T10:30:00'),
  { description: 'Weekly sync', guests: 'a@example.com,b@example.com' },
);
```

**List today's events:**
```javascript
const today = new Date();
const events = CalendarApp.getDefaultCalendar().getEventsForDay(today);
events.forEach(e => Logger.log(e.getTitle()));
```

---

## Docs
Reference: [`reference/document/`](reference/document/README.md)

**Append text and a heading:**
```javascript
const doc = DocumentApp.openById('DOC_ID');
const body = doc.getBody();
body.appendParagraph('Report').setHeading(DocumentApp.ParagraphHeading.HEADING1);
body.appendParagraph('Generated on ' + new Date());
```

**Replace placeholder text (mail-merge style):**
```javascript
body.replaceText('{{name}}', 'Alice');
```

---

## Forms
Reference: [`reference/forms/`](reference/forms/README.md)

**Create a form with a question:**
```javascript
const form = FormApp.create('Feedback');
form.addTextItem().setTitle('What did you think?').setRequired(true);
```

**Read all responses:**
```javascript
FormApp.openById('FORM_ID').getResponses().forEach(response => {
  response.getItemResponses().forEach(ir => Logger.log(ir.getResponse()));
});
```

---

## Triggers
Guide: [`guides/triggers/`](guides/triggers/simple-triggers.md) · Reference: [`reference/script/`](reference/script/README.md)

**Simple trigger (add to any bound script — no setup needed):**
```javascript
function onOpen() {
  SpreadsheetApp.getUi().createMenu('My Tools').addItem('Run', 'myFunction').addToUi();
}
```

**Create a time-driven (installable) trigger, once:**
```javascript
function createDailyTrigger() {
  ScriptApp.newTrigger('dailyJob').timeBased().everyDays(1).atHour(6).create();
}
```

**Create an installable onEdit trigger (needed for actions simple triggers can't do, e.g. sending email):**
```javascript
function createEditTrigger() {
  ScriptApp.newTrigger('onEditInstallable')
    .forSpreadsheet(SpreadsheetApp.getActive())
    .onEdit()
    .create();
}
```

---

## Properties & Cache
Reference: [`reference/properties/`](reference/properties/README.md), [`reference/cache/`](reference/cache/README.md)

**Persist small config/state across executions:**
```javascript
PropertiesService.getScriptProperties().setProperty('lastRunId', '42');
const lastRunId = PropertiesService.getScriptProperties().getProperty('lastRunId');
```

**Cache an expensive computation for 10 minutes:**
```javascript
const cache = CacheService.getScriptCache();
let data = cache.get('apiResult');
if (!data) {
  data = JSON.stringify(fetchExpensiveThing());
  cache.put('apiResult', data, 600); // seconds
}
data = JSON.parse(data);
```

---

## UrlFetchApp (HTTP requests)
Reference: [`reference/url-fetch/`](reference/url-fetch/README.md)

**GET request and parse JSON:**
```javascript
const response = UrlFetchApp.fetch('https://api.example.com/data');
const json = JSON.parse(response.getContentText());
```

**POST with JSON body and auth header:**
```javascript
const response = UrlFetchApp.fetch('https://api.example.com/items', {
  method: 'post',
  contentType: 'application/json',
  headers: { Authorization: 'Bearer ' + token },
  payload: JSON.stringify({ name: 'Alice' }),
  muteHttpExceptions: true, // inspect response.getResponseCode() instead of throwing
});
```

---

## Custom menus & UI
Guide: [`guides/Menus_dialogs_sidebars.md`](guides/Menus_dialogs_sidebars.md) · Reference: [`reference/base/`](reference/base/README.md)

**Prompt and alert dialogs:**
```javascript
const ui = SpreadsheetApp.getUi();
const result = ui.prompt('Enter your name:');
if (result.getSelectedButton() === ui.Button.OK) {
  ui.alert('Hello, ' + result.getResponseText());
}
```

---

## Custom functions
Guide: [`guides/sheets/custom-functions.md`](guides/sheets/custom-functions.md)

**A function usable as `=DOUBLE(A1)` in a cell:**
```javascript
/**
 * Doubles the input value.
 * @param {number} input The value to double.
 * @return {number} The doubled value.
 * @customfunction
 */
function DOUBLE(input) {
  return input * 2;
}
```

---

## Web apps (HtmlService)
Guide: [`guides/html/web-apps.md`](guides/html/web-apps.md) · Reference: [`reference/html/`](reference/html/README.md)

**Serve a page from `doGet`:**
```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile('Index').setTitle('My App');
}
```

**Call a server function from client-side HTML:**
```html
<script>
  google.script.run
    .withSuccessHandler(result => console.log(result))
    .myServerFunction('arg');
</script>
```

---

## Locking (avoid race conditions)
Reference: [`reference/lock/`](reference/lock/README.md)

**Guard a critical section when a script can be triggered concurrently:**
```javascript
const lock = LockService.getScriptLock();
try {
  lock.waitLock(10000); // wait up to 10s
  // ... critical section (e.g. read-modify-write on a sheet) ...
} finally {
  lock.releaseLock();
}
```

---

## Utilities
Reference: [`reference/utilities/`](reference/utilities/README.md)

**Format a date, sleep, and base64-encode:**
```javascript
const formatted = Utilities.formatDate(new Date(), 'GMT', 'yyyy-MM-dd HH:mm:ss');
Utilities.sleep(1000); // milliseconds
const encoded = Utilities.base64Encode('hello');
```

---

## Error handling & logging
Guide: [`guides/Logging.md`](guides/Logging.md)

**Structured logging plus try/catch with context:**
```javascript
function safeRun() {
  try {
    doTheWork();
  } catch (err) {
    console.error(`safeRun failed: ${err.message}`, err.stack);
    throw err; // rethrow if the caller (e.g. a trigger) should also fail loudly
  }
}
```

---

## Card Service (Add-on UI)
Reference: [`reference/card-service/`](reference/card-service/README.md) · Guide: [`workspace-add-ons/concepts/cards.md`](workspace-add-ons/concepts/cards.md)

**Build a minimal card returned from a homepage trigger:**
```javascript
function onHomepage(e) {
  const section = CardService.newCardSection().addWidget(
    CardService.newTextParagraph().setText('Hello from my add-on!'),
  );
  return CardService.newCardBuilder()
    .setHeader(CardService.newCardHeader().setTitle('My Add-on'))
    .addSection(section)
    .build();
}
```
