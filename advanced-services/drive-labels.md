# Advanced Drive Labels Service

Source: https://developers.google.com/apps-script/advanced/drive-labels

## Overview

The Google Drive Labels advanced service in Apps Script enables creation and management of labels for Drive files and folders. This service leverages the Drive Labels API and requires activation before use.

**Key capability:** "Create and manage labels for your Drive files and folders with the Google Drive Labels advanced service."

## Enabling the Service

This is an advanced service requiring activation. To apply or remove Drive labels, use the Advanced Drive Service in conjunction with this service.

## Reference Documentation

The service mirrors the public [Google Drive Labels API](https://developers.google.com/drive/labels) with identical objects, methods, and parameters (external — not scraped). For support issues, consult the Drive Labels API support guide.

## Code Examples

### List Available Labels

```javascript
/**
 * List labels available to the user.
 */
function listLabels() {
  let pageToken = null;
  let labels = [];
  do {
    try {
      const response = DriveLabels.Labels.list({
        publishedOnly: true,
        pageToken: pageToken,
      });
      pageToken = response.nextPageToken;
      labels = labels.concat(response.labels);
    } catch (err) {
      console.log("Failed to list labels with error %s", err.message);
    }
  } while (pageToken != null);

  console.log("Found %d labels", labels.length);
}
```

### Retrieve a Specific Label

```javascript
/**
 * Get a label by name.
 * @param {string} labelName The label name.
 */
function getLabel(labelName) {
  try {
    const label = DriveLabels.Labels.get(labelName, {
      view: "LABEL_VIEW_FULL",
    });
    const title = label.properties.title;
    const fieldsLength = label.fields.length;
    console.log(
      `Fetched label with title: '${title}' and ${fieldsLength} fields.`,
    );
  } catch (err) {
    console.log("Failed to get label with error %s", err.message);
  }
}
```

### List Labels on a Drive Item

```javascript
/**
 * List Labels on a Drive Item
 * Fetches a Drive Item and prints all applied values along with their
 * human-readable names.
 *
 * @param {string} fileId The Drive File ID
 */
function listLabelsOnDriveItem(fileId) {
  try {
    const appliedLabels = Drive.Files.listLabels(fileId);

    console.log(
      "%d label(s) are applied to this file",
      appliedLabels.labels.length,
    );

    for (const appliedLabel of appliedLabels.labels) {
      const labelName = `labels/${appliedLabel.id}@${appliedLabel.revisionId}`;

      console.log("Fetching Label: %s", labelName);
      const label = DriveLabels.Labels.get(labelName, {
        view: "LABEL_VIEW_FULL",
      });

      console.log("Label Title: %s", label.properties.title);

      for (const fieldId of Object.keys(appliedLabel.fields)) {
        const fieldValue = appliedLabel.fields[fieldId];
        const field = label.fields.find((f) => f.id === fieldId);

        console.log(
          `Field ID: ${field.id}, Display Name: ${field.properties.displayName}`,
        );
        switch (fieldValue.valueType) {
          case "text":
            console.log("Text: %s", fieldValue.text[0]);
            break;
          case "integer":
            console.log("Integer: %d", fieldValue.integer[0]);
            break;
          case "dateString":
            console.log("Date: %s", fieldValue.dateString[0]);
            break;
          case "user": {
            const user = fieldValue.user
              .map((user) => {
                return `${user.emailAddress}: ${user.displayName}`;
              })
              .join(", ");
            console.log(`User: ${user}`);
            break;
          }
          case "selection": {
            const choices = fieldValue.selection.map((choiceId) => {
              return field.selectionOptions.choices.find(
                (choice) => choice.id === choiceId,
              );
            });
            const selection = choices
              .map((choice) => {
                return `${choice.id}: ${choice.properties.displayName}`;
              })
              .join(", ");
            console.log(`Selection: ${selection}`);
            break;
          }
          default:
            console.log("Unknown: %s", fieldValue.valueType);
            console.log(fieldValue.value);
        }
      }
    }
  } catch (err) {
    console.log("Failed with error %s", err.message);
  }
}
```
</content>
