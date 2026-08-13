# Translate text in a Google Docs document

## Page Summary

This quickstart demonstrates creating a Google Docs add-on using Apps Script that enables text translation. The guide covers:

- Building an add-on allowing users to "select text, choose source and target languages, and obtain the translation"
- Inserting translated content directly into documents
- Requirements include a Google Account and web browser
- Setup involves configuring a script, running it, and authorizing permissions

## Objectives

- Set up the script
- Run the script

## Prerequisites

- A Google Account (Google Workspace accounts may require administrator approval)
- A web browser with internet access

## Set Up Instructions

1. Create a Google Docs document at docs.new
2. Click **Extensions** > **Apps Script**
3. Rename the project "Translate Docs"
4. Rename the Code.gs file to "translate"
5. Add an HTML file named "sidebar"
6. Replace file contents with provided code samples

## Key Code Components

**translate.gs** handles:
- Menu creation via `onOpen()` and `onInstall()` functions
- Text selection retrieval through `getSelectedText()`
- Language preference management
- Translation execution using `LanguageApp.translate()`
- Text insertion into documents

**sidebar.html** provides:
- User interface with radio buttons for language selection
- Support for English, French, German, Japanese, and Spanish
- Auto-detect functionality for source language
- Translation textarea and Insert/Translate buttons

## Running the Script

1. Reload the Docs document
2. Click **Extensions** > **Translate Docs** > **Start**
3. Authorize when prompted
4. Select text and click **Translate**
5. Click **Insert** to replace document text

## Next Steps

- Extend Docs with Apps Script
- Reference Document service documentation
