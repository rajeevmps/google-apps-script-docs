# Automation quickstart

## Page Summary

- This guide helps you build and run an automation that creates a Google Docs document and emails you a link to it.
- To use this sample, you need a Google Account and a web browser with internet access.
- The setup involves opening the Apps Script editor, creating a new project, pasting in the provided code, saving, and naming the script.
- Running the script requires clicking run, authorizing it when prompted, and then checking your Gmail inbox for the email containing the document link.

Build and run an automation that creates a Google Docs document and emails you a link to the document.

## Objectives

- Set up the script.
- Run the script.

## Prerequisites

To use this sample, you need the following prerequisites:

- A Google Account (Google Workspace accounts might require administrator approval).
- A web browser with access to the internet.

## Set up the script

To build the automation, do the following:

1. To open the Google Apps Script editor, go to `script.google.com`. If this is the first time you've been to `script.google.com`, click **View Dashboard**.
2. Click **New project**.
3. Delete any code in the script editor and paste in the following code.

```javascript
/**
 * Creates a Google Doc and sends an email to the current user with a link to the doc.
 */
function createAndSendDocument() {
  try {
    // Create a new Google Doc named 'Hello, world!'
    const doc = DocumentApp.create("Hello, world!");

    // Access the body of the document, then add a paragraph.
    doc
      .getBody()
      .appendParagraph("This document was created by Google Apps Script.");

    // Get the URL of the document.
    const url = doc.getUrl();

    // Get the email address of the active user - that's you.
    const email = Session.getActiveUser().getEmail();

    // Get the name of the document to use as an email subject line.
    const subject = doc.getName();

    // Append a new string to the "url" variable to use as an email body.
    const body = `Link to your doc: ${url}`;

    // Send yourself an email with a link to the document.
    GmailApp.sendEmail(email, subject, body);
  } catch (err) {
    // TODO (developer) - Handle exception
    console.log("Failed with error %s", err.message);
  }
}
```

4. Click **Save**.
5. Click **Untitled project**.
6. Enter a name for your script and click **Rename**.

## Run the script

To run the script, do the following:

1. Click **Run**.
2. When prompted, authorize the script.
3. When the script execution completes, check your [Gmail inbox](https://mail.google.com) for the email.
4. Open the email and click the link to open the document that you created.

## Next steps

- [Extend Docs](https://developers.google.com/apps-script/guides/docs)
- [Extend Google Sheets](https://developers.google.com/apps-script/guides/sheets)
- [Extend Google Slides](https://developers.google.com/apps-script/guides/slides)
- [Basic JavaScript features](https://developers.google.com/apps-script/guides/services#basic_javascript_features)

Source: https://developers.google.com/apps-script/quickstart/automation
