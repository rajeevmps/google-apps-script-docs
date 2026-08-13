# MailApp

Sends email.

Sends email. This service allows users to send emails with complete control over the content of the email. Unlike GmailApp, MailApp's sole purpose is sending email. MailApp cannot access a user's Gmail inbox. Changes to scripts written using GmailApp are more likely to trigger a re-authorization request from a user than MailApp scripts.

## Methods

### getRemainingDailyQuota()
**Return type:** `Integer`

Returns the number of recipients you can send emails to for the rest of the day. The returned value is valid for the current execution and might vary between executions. Quotas are based on the number of email recipients.

```javascript
const emailQuotaRemaining = MailApp.getRemainingDailyQuota();
Logger.log(`Remaining email quota: ${emailQuotaRemaining}`);
```

### sendEmail(message)
**Parameters:** `message` (Object)
**Return type:** `void`

Sends an email message. This variation of the method is much more flexible, allowing for many more options.

Advanced parameters (message object): `to`, `subject`, `body`, `cc`, `bcc`, `htmlBody`, `inlineImages`, `attachments`, `name`, `noReply`, `replyTo`

```javascript
function inlineImage() {
  const googleLogoUrl = 'https://www.gstatic.com/images/branding/googlelogo/1x/googlelogo_color_74x24dp.png';
  const youtubeLogoUrl = 'https://developers.google.com/youtube/images/YouTube_logo_standard_white.png';
  const googleLogoBlob = UrlFetchApp.fetch(googleLogoUrl).getBlob().setName('googleLogoBlob');
  const youtubeLogoBlob = UrlFetchApp.fetch(youtubeLogoUrl).getBlob().setName('youtubeLogoBlob');
  MailApp.sendEmail({
    to: 'recipient@example.com',
    subject: 'Logos',
    htmlBody: 'inline Google Logo<img src=\'cid:googleLogo\'> images! <br>inline YouTube Logo <img src=\'cid:youtubeLogo\'>',
    inlineImages: { googleLogo: googleLogoBlob, youtubeLogo: youtubeLogoBlob }
  });
}
```

### sendEmail(recipient, subject, body)
**Parameters:** `recipient` (String), `subject` (String), `body` (String)
**Return type:** `void`

Sends an email message.

```javascript
MailApp.sendEmail('recipient@example.com', 'TPS reports', 'Where are the TPS reports?');
```

### sendEmail(recipient, subject, body, options)
**Parameters:** `recipient` (String), `subject` (String), `body` (String), `options` (Object)
**Return type:** `void`

Sends an email message with optional arguments.

Advanced parameters (options object): `attachments`, `cc`, `bcc`, `htmlBody`, `inlineImages`, `name`, `noReply`, `replyTo`

```javascript
const file = DriveApp.getFileById('1234567890abcdefghijklmnopqrstuvwxyz');
const blob = Utilities.newBlob('Insert any HTML content here', 'text/html', 'my_document.html');
MailApp.sendEmail('mike@example.com', 'Attachment example', 'Two files are attached.', {
  name: 'Automatic Emailer Script',
  attachments: [file.getAs(MimeType.PDF), blob]
});
```

### sendEmail(to, replyTo, subject, body)
**Parameters:** `to` (String), `replyTo` (String), `subject` (String), `body` (String)
**Return type:** `void`

Sends an email message. This method allows a user to easily specify a Reply-To address for the sent message that can differ from the sender.

```javascript
MailApp.sendEmail('recipient@example.com', 'replies@example.com', 'TPS report status', 'What is the status of those TPS reports?');
```
