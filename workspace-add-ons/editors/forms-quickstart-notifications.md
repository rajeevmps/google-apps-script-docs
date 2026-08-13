# Send emails about new Google Forms submissions

## Page Summary

- This Google Forms add-on automates email notifications to form creators and/or respondents upon submission.
- Customizable settings allow control over notification frequency, recipient emails, and content.
- The add-on utilizes Google Apps Script triggers to execute functions when the form is opened, installed, or submitted.
- Users configure notification preferences through a sidebar accessible within the Google Form.
- The script manages authorization to access Google services for sending emails and interacting with form data.

---

This quickstart creates a Google Forms Editor add-on that uses triggers to send Gmail messages when a user responds to the form.

## Objectives

- Set up the script.
- Run the script.

## Prerequisites

To use this sample, you need the following prerequisites:

- A Google Account (Google Workspace accounts might require administrator approval).
- A web browser with access to the internet.

## Set up the script

1. Create a Google Forms form at [forms.new](https://docs.google.com/forms/create).
2. Click More more_vert > **Script editor**.
3. Click **Untitled project**.
4. Rename the Apps Script project **Forms notifications** and click **Rename**.
5. Click Add a file add > **HTML**. Name the file `sidebar`.
6. Repeat step 5 to create 4 more HTML files named `about`, `authorizationEmail`, `creatorNotification`, and `respondentNotification`. When you're done you should have 1 script file and 5 HTML files.
7. Replace the contents of each file with the following corresponding code, then click Save.

### code.gs

```javascript
/**
 * @OnlyCurrentDoc
 *
 * The above comment directs Apps Script to limit the scope of file
 * access for this add-on. It specifies that this add-on will only
 * attempt to read or modify the files in which the add-on is used,
 * and not all of the user's files. The authorization request message
 * presented to users will reflect this limited scope.
 */

/**
 * A global constant String holding the title of the add-on. This is
 * used to identify the add-on in the notification emails.
 */
const ADDON_TITLE = "Form Notifications";

/**
 * A global constant 'notice' text to include with each email
 * notification.
 */
const NOTICE =
  "Form Notifications was created as an sample add-on, and is" +
  " meant for" +
  "demonstration purposes only. It should not be used for complex or important" +
  "workflows. The number of notifications this add-on produces are limited by the" +
  "owner's available email quota; it will not send email notifications if the" +
  "owner's daily email quota has been exceeded. Collaborators using this add-on on" +
  "the same form will be able to adjust the notification settings, but will not be" +
  "able to disable the notification triggers set by other collaborators.";

/**
 * Adds a custom menu to the active form to show the add-on sidebar.
 *
 * @param {object} e The event parameter for a simple onOpen trigger. To
 *     determine which authorization mode (ScriptApp.AuthMode) the trigger is
 *     running in, inspect e.authMode.
 */
function onOpen(e) {
  try {
    FormApp.getUi()
      .createAddonMenu()
      .addItem("Configure notifications", "showSidebar")
      .addItem("About", "showAbout")
      .addToUi();
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Runs when the add-on is installed.
 *
 * @param {object} e The event parameter for a simple onInstall trigger. To
 *     determine which authorization mode (ScriptApp.AuthMode) the trigger is
 *     running in, inspect e.authMode. (In practice, onInstall triggers always
 *     run in AuthMode.FULL, but onOpen triggers may be AuthMode.LIMITED or
 *     AuthMode.NONE).
 */
function onInstall(e) {
  onOpen(e);
}

/**
 * Opens a sidebar in the form containing the add-on's user interface for
 * configuring the notifications this add-on will produce.
 */
function showSidebar() {
  try {
    const ui =
      HtmlService.createHtmlOutputFromFile("sidebar").setTitle(
        "Form Notifications",
      );
    FormApp.getUi().showSidebar(ui);
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Opens a purely-informational dialog in the form explaining details about
 * this add-on.
 */
function showAbout() {
  try {
    const ui = HtmlService.createHtmlOutputFromFile("about")
      .setWidth(420)
      .setHeight(270);
    FormApp.getUi().showModalDialog(ui, "About Form Notifications");
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Save sidebar settings to this form's Properties, and update the onFormSubmit
 * trigger as needed.
 *
 * @param {Object} settings An Object containing key-value
 *      pairs to store.
 */
function saveSettings(settings) {
  try {
    PropertiesService.getDocumentProperties().setProperties(settings);
    adjustFormSubmitTrigger();
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Queries the User Properties and adds additional data required to populate
 * the sidebar UI elements.
 *
 * @return {Object} A collection of Property values and
 *     related data used to fill the configuration sidebar.
 */
function getSettings() {
  try {
    const settings = PropertiesService.getDocumentProperties().getProperties();

    // Use a default email if the creator email hasn't been provided yet.
    if (!settings.creatorEmail) {
      settings.creatorEmail = Session.getEffectiveUser().getEmail();
    }

    // Get text field items in the form and compile a list
    //   of their titles and IDs.
    const form = FormApp.getActiveForm();
    const textItems = form.getItems(FormApp.ItemType.TEXT);

    settings.textItems = [];
    for (let i = 0; i < textItems.length; i++) {
      settings.textItems.push({
        title: textItems[i].getTitle(),
        id: textItems[i].getId(),
      });
    }
    return settings;
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Adjust the onFormSubmit trigger based on user's requests.
 */
function adjustFormSubmitTrigger() {
  try {
    const form = FormApp.getActiveForm();
    const triggers = ScriptApp.getUserTriggers(form);
    const settings = PropertiesService.getDocumentProperties();
    const triggerNeeded =
      settings.getProperty("creatorNotify") === "true" ||
      settings.getProperty("respondentNotify") === "true";

    // Create a new trigger if required; delete existing trigger
    // if it is not needed.
    let existingTrigger = null;
    for (let i = 0; i < triggers.length; i++) {
      if (triggers[i].getEventType() === ScriptApp.EventType.ON_FORM_SUBMIT) {
        existingTrigger = triggers[i];
        break;
      }
    }
    if (triggerNeeded && !existingTrigger) {
      const trigger = ScriptApp.newTrigger("respondToFormSubmit")
        .forForm(form)
        .onFormSubmit()
        .create();
    } else if (!triggerNeeded && existingTrigger) {
      ScriptApp.deleteTrigger(existingTrigger);
    }
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Responds to a form submission event if an onFormSubmit trigger has been
 * enabled.
 *
 * @param {Object} e The event parameter created by a form
 *      submission; see
 *      https://developers.google.com/apps-script/understanding_events
 */
function respondToFormSubmit(e) {
  try {
    const settings = PropertiesService.getDocumentProperties();
    const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL);

    // Check if the actions of the trigger require authorizations that have not
    // been supplied yet -- if so, warn the active user via email (if possible).
    // This check is required when using triggers with add-ons to maintain
    // functional triggers.
    if (
      authInfo.getAuthorizationStatus() ===
      ScriptApp.AuthorizationStatus.REQUIRED
    ) {
      // Re-authorization is required. In this case, the user needs to be alerted
      // that they need to reauthorize; the normal trigger action is not
      // conducted, since authorization needs to be provided first. Send at
      // most one 'Authorization Required' email a day, to avoid spamming users
      // of the add-on.
      sendReauthorizationRequest();
    } else {
      // All required authorizations have been granted, so continue to respond to
      // the trigger event.

      // Check if the form creator needs to be notified; if so, construct and
      // send the notification.
      if (settings.getProperty("creatorNotify") === "true") {
        sendCreatorNotification();
      }

      // Check if the form respondent needs to be notified; if so, construct and
      // send the notification. Be sure to respect the remaining email quota.
      if (
        settings.getProperty("respondentNotify") === "true" &&
        MailApp.getRemainingDailyQuota() > 0
      ) {
        sendRespondentNotification(e.response);
      }
    }
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Called when the user needs to reauthorize. Sends the user of the
 * add-on an email explaining the need to reauthorize and provides
 * a link for the user to do so. Capped to send at most one email
 * a day to prevent spamming the users of the add-on.
 */
function sendReauthorizationRequest() {
  try {
    const settings = PropertiesService.getDocumentProperties();
    const authInfo = ScriptApp.getAuthorizationInfo(ScriptApp.AuthMode.FULL);
    const lastAuthEmailDate = settings.getProperty("lastAuthEmailDate");
    const today = new Date().toDateString();
    if (lastAuthEmailDate !== today) {
      if (MailApp.getRemainingDailyQuota() > 0) {
        const template =
          HtmlService.createTemplateFromFile("authorizationEmail");
        template.url = authInfo.getAuthorizationUrl();
        template.notice = NOTICE;
        const message = template.evaluate();
        MailApp.sendEmail(
          Session.getEffectiveUser().getEmail(),
          "Authorization Required",
          message.getContent(),
          {
            name: ADDON_TITLE,
            htmlBody: message.getContent(),
          },
        );
      }
      settings.setProperty("lastAuthEmailDate", today);
    }
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Sends out creator notification email(s) if the current number
 * of form responses is an even multiple of the response step
 * setting.
 */
function sendCreatorNotification() {
  try {
    const form = FormApp.getActiveForm();
    const settings = PropertiesService.getDocumentProperties();
    let responseStep = settings.getProperty("responseStep");
    responseStep = responseStep ? Number.parseInt(responseStep) : 10;

    // If the total number of form responses is an even multiple of the
    // response step setting, send a notification email(s) to the form
    // creator(s). For example, if the response step is 10, notifications
    // will be sent when there are 10, 20, 30, etc. total form responses
    // received.
    if (form.getResponses().length % responseStep === 0) {
      const addresses = settings.getProperty("creatorEmail").split(",");
      if (MailApp.getRemainingDailyQuota() > addresses.length) {
        const template = HtmlService.createTemplateFromFile(
          "creatorNotification",
        );
        template.summary = form.getSummaryUrl();
        template.responses = form.getResponses().length;
        template.title = form.getTitle();
        template.responseStep = responseStep;
        template.formUrl = form.getEditUrl();
        template.notice = NOTICE;
        const message = template.evaluate();
        MailApp.sendEmail(
          settings.getProperty("creatorEmail"),
          `${form.getTitle()}: Form submissions detected`,
          message.getContent(),
          {
            name: ADDON_TITLE,
            htmlBody: message.getContent(),
          },
        );
      }
    }
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}

/**
 * Sends out respondent notification emails.
 *
 * @param {FormResponse} response FormResponse object of the event
 *      that triggered this notification
 */
function sendRespondentNotification(response) {
  try {
    const form = FormApp.getActiveForm();
    const settings = PropertiesService.getDocumentProperties();
    const emailId = settings.getProperty("respondentEmailItemId");
    const emailItem = form.getItemById(Number.parseInt(emailId));
    const respondentEmail = response
      .getResponseForItem(emailItem)
      .getResponse();
    if (respondentEmail) {
      const template = HtmlService.createTemplateFromFile(
        "respondentNotification",
      );
      template.paragraphs = settings.getProperty("responseText").split("\n");
      template.notice = NOTICE;
      const message = template.evaluate();
      MailApp.sendEmail(
        respondentEmail,
        settings.getProperty("responseSubject"),
        message.getContent(),
        {
          name: form.getTitle(),
          htmlBody: message.getContent(),
        },
      );
    }
  } catch (e) {
    // TODO (Developer) - Handle exception
    console.log("Failed with error: %s", e.error);
  }
}
```

### sidebar.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <link rel="stylesheet" href="https://ssl.gstatic.com/docs/script/css/add-ons1.css">
    <!-- The CSS package above applies Google styling to buttons and other elements. -->
    <style>
    .branding-below {
      bottom: 54px;
      top: 0;
    }
    .branding-text {
      left: 7px;
      position: relative;
      top: 3px;
    }
    .logo {
      vertical-align: middle;
    }
    .width-100 {
      width: 100%;
      box-sizing: border-box;
      -webkit-box-sizing: border-box;
      -moz-box-sizing: border-box;
    }
    label {
      font-weight: bold;
    }
    #creator-options,
    #respondent-options {
      background-color: #eee;
      border-color: #eee;
      border-width: 5px;
      border-style: solid;
      display: none;
    }
    #creator-email,
    #respondent-email,
    #button-bar,
    #submit-subject {
      margin-bottom: 10px;
    }

    #response-step {
      display: inline;
    }
    </style>
  </head>
  <body>
    <div class="sidebar branding-below">
      <form>
        <div class="block">
          <input type="checkbox" id="creator-notify">
          <label for="creator-notify">Notify me</label>
        </div>
        <div class="block form-group" id="creator-options">
          <label for="creator-email">
            My email addresses (comma-separated)
          </label>
          <input type="text" class="width-100" id="creator-email">
          <label for="response-step">Send notifications after every</label>
          <input type="number" id="response-step" value="10"
              min="1" max="99999"> responses (default 10)
        </div>

        <div class="block">
          <input type="checkbox" id="respondent-notify">
          <label for="respondent-notify">Notify respondents</label>
        </div>
        <div class="block form-group" id="respondent-options">
          <label for="respondent-email">
            Which question asks for their email?
          </label>
          <select class="width-100" id="respondent-email"></select>
          <label for="submit-subject">
            Notification email subject:
          </label>
          <input type="text" class="width-100" id="submit-subject">
          <label for="submit-notice">Notification email body:</label>
          <textarea rows="8" cols="40" id="submit-notice"
              class="width-100"></textarea>
        </div>

        <div class="block" id="button-bar">
          <button class="action" id="save-settings">Save</button>
        </div>
      </form>
    </div>

    <div class="sidebar bottom">
      <img alt="Add-on logo" class="logo" width="25"
          src="https://g-suite-documentation-images.firebaseapp.com/images/newFormNotificationsicon.png">
      <span class="gray branding-text">Form Notifications by Google</span>
    </div>

    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js">
    </script>
    <script>
      /**
       * On document load, assign required handlers to each element,
       * and attempt to load any saved settings.
       */
      $(function() {
        $('#save-settings').click(saveSettingsToServer);
        $('#creator-notify').click(toggleCreatorNotify);
        $('#respondent-notify').click(toggleRespondentNotify);
        $('#response-step').change(validateNumber);
        google.script.run
           .withSuccessHandler(loadSettings)
           .withFailureHandler(showStatus)
           .withUserObject($('#button-bar').get())
           .getSettings();
      });

      /**
       * Callback function that populates the notification options using
       * previously saved values.
       *
       * @param {Object} settings The saved settings from the client.
       */
      function loadSettings(settings) {
        $('#creator-email').val(settings.creatorEmail);
        $('#response-step').val(!settings.responseStep ?
           10 : settings.responseStep);
        $('#submit-subject').val(!settings.responseSubject ?
           'Thank you for filling out our form!' :
           settings.responseSubject);
        $('#submit-notice').val(!settings.responseText ?
           'Thank you for responding to our form!' :
           settings.responseText);

        if (settings.creatorNotify === 'true') {
          $('#creator-notify').prop('checked', true);
          $('#creator-options').show();
        }

        if (settings.respondentNotify === 'true') {
          $('#respondent-notify').prop('checked', true);
          $('#respondent-options').show();
        }

        // Fill the respondent email select box with the
        // titles given to the form's text Items. Also include
        // the form Item IDs as values so that they can be
        // easily recovered during the Save operation.
        for (var i = 0; i < settings.textItems.length; i++) {
          var option = $('<option>').attr('value', settings.textItems[i]['id'])
              .text(settings.textItems[i]['title']);
          $('#respondent-email').append(option);
        }
        $('#respondent-email').val(settings.respondentEmailItemId);
      }

      /**
       * Toggles the visibility of the form creator notification options.
       */
      function toggleCreatorNotify() {
        $('#status').remove();
        if ($('#creator-notify').is(':checked')) {
          $('#creator-options').show();
        } else {
          $('#creator-options').hide();
        }
      }

      /**
       * Toggles the visibility of the form sumbitter notification options.
       */
      function toggleRespondentNotify() {
        $('#status').remove();
        if($('#respondent-notify').is(':checked')) {
          $('#respondent-options').show();
        } else {
          $('#respondent-options').hide();
        }
      }

      /**
       * Ensures that the entered step is a number between 1
       * and 99999, inclusive.
       */
      function validateNumber() {
        var value = $('#response-step').val();
        if (!value) {
          $('#response-step').val(10);
        } else if (value < 1) {
          $('#response-step').val(1);
        } else if (value > 99999) {
          $('#response-step').val(99999);
        }
      }

      /**
       * Collects the options specified in the add-on sidebar and sends them to
       * be saved as Properties on the server.
       */
      function saveSettingsToServer() {
        this.disabled = true;
        $('#status').remove();
        var creatorNotify = $('#creator-notify').is(':checked');
        var respondentNotify = $('#respondent-notify').is(':checked');
        var settings = {
          'creatorNotify': creatorNotify,
          'respondentNotify': respondentNotify
        };

        // Only save creator options if notify is turned on
        if (creatorNotify) {
          settings.responseStep = $('#response-step').val();
          settings.creatorEmail = $('#creator-email').val().trim();

          // Abort save if entered email is blank
          if (!settings.creatorEmail) {
            showStatus('Enter an owner email', $('#button-bar'));
            this.disabled = false;
            return;
          }
        }

        // Only save respondent options if notify is turned on
        if (respondentNotify) {
          settings.respondentEmailItemId = $('#respondent-email').val();
          settings.responseSubject = $('#submit-subject').val();
          settings.responseText = $('#submit-notice').val();
        }

        // Save the settings on the server
        google.script.run
            .withSuccessHandler(
              function(msg, element) {
                showStatus('Saved settings', $('#button-bar'));
                element.disabled = false;
              })
            .withFailureHandler(
              function(msg, element) {
                showStatus(msg, $('#button-bar'));
                element.disabled = false;
              })
            .withUserObject(this)
            .saveSettings(settings);
      }

      /**
       * Inserts a div that contains an status message after a given element.
       *
       * @param {String} msg The status message to display.
       * @param {Object} element The element after which to display the Status.
       */
      function showStatus(msg, element) {
         var div = $('<div>')
             .attr('id', 'status')
             .attr('class','error')
             .text(msg);
        $(element).after(div);
      }
    </script>
  </body>
</html>
```

### about.html

```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <link rel="stylesheet" href="https://ssl.gstatic.com/docs/script/css/add-ons1.css">
    <!-- The CSS package above applies Google styling to buttons and other elements. -->
  </head>
  <body>
    <div>
      <p>
      <i>Form Notifications</i> was created as an sample add-on, and is meant
      for demonstration purposes only. It should not be used for complex or
      important workflows.
      </p>
      <p>
      The number of notifications this add-on produces are limited by the owner's
      available email quota; it will not send email notifications if the owner's
      daily email quota has been exceeded. Collaborators using this add-on on the
      same form will be able to adjust the notification settings, but will not be
      able to disable the notification triggers set by other collaborators.
      </p>
    </div>
  </body>
</html>
```

### authorizationEmail.html

```html
<p>The Google Forms add-on <i>Form Notifications</i> is set to run automatically
whenever a form is submitted. The add-on was recently updated and it needs you
to re-authorize it to run on your behalf.</p>

<p>The add-on's automatic functions are temporarily disabled until you
re-authorize the add-on. You can accomplish this by opening one of the forms
using the add-on and running the add-on through the menu. Alternatively, you can
click this link to approve authorization directly:</p>

<p><a href="<?= url ?>">Click here</a> to re-authorize the add-on.</p>

<p>This notification email will be sent to you at most once per day until the
add-on is re-authorized.</p>

<hr>

<p style="font-size:80%">This automatic message was sent to you via the <i>Form
Notifications</i> add-on for Google Forms.
<?= notice ?></p>
```

### creatorNotification.html

```html
<p><i>Form Notifications</i> (a Google Forms add-on) has detected that the form
titled <a href="<?= formUrl?>"><b><?= title ?></b></a> has received
<?= responses ?> responses so far.</p>

<p><a href="<?= summary ?>">Summary of form responses</a></p>

<p>You are receiving this email because an editor of this form configured
<i>Form Notifications</i> to alert you every time this form receives
<b><?= responseStep ?></b> responses.</p>

<p>To change this setting, or to stop receiving these notifications, have the
form owner or editors open the form and adjust the <i>Form Notifications</i>
add-on configuration via the "Configure notifications" menu item.</p>

<hr>

<p style="font-size:80%">This automatic message was sent to you via the <i>Form
Notifications</i> add-on for Google Forms.
<?= notice ?></p>
```

### respondentNotification.html

```html
<? for (var i = 0; i < paragraphs.length; i++) { ?>
  <p><?= paragraphs[i] ?></p>
<? } ?>

<hr>

<p style="font-size:80%">This automatic message was sent to you via the <i>Form
Notifications</i> add-on for Google Forms.
<?= notice ?></p>
```

## Run the script

1. Switch back to your form and refresh the page.
2. Add a short answer text question to your form. In **Untitled question**, enter **Email Address**. Optionally, you can create other form questions.
3. Click add-ons extension > **Form notifications**. It can take several seconds for add-ons extension to appear.
4. In the dialog, click **Configure notifications**.
5. When prompted, authorize the add-on.
6. Again, click add-ons extension > **Form notifications** > **Configure notifications**.
7. In the add-on, check the **Notify me** box and enter your email address.
8. For **Send notifications after every**, enter **1**.
9. Click **Save**.
10. To submit a response, click Preview visibility
11. Fill out the form and click **Submit**.
12. Check your email for a notification.

## Next steps

- [Extend Forms with Apps Script](/workspace/add-ons/editors/forms)
- [Forms service reference](/apps-script/reference/forms)

---

## Summary

This quickstart demonstrates building a Google Forms add-on that uses automation for email notifications. The sample enables form creators and respondents to "receive automated notifications triggered by form submissions." The implementation uses Apps Script, leveraging triggers and the MailApp service to manage notification preferences through a configurable sidebar interface within the form.
