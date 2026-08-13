# Translate text from Google Slides

## Page Summary

This quickstart demonstrates building a Google Slides Editor add-on using Apps Script for translating selected presentation text into multiple languages including Arabic, Chinese, English, French, German, Hindi, Japanese, Portuguese, and Spanish.

## Objectives

- Set up the script
- Run the script

## Prerequisites

- A Google Account (Google Workspace accounts may require administrator approval)
- A web browser with internet access

## Setup Instructions

1. Create a Slides presentation at slides.new
2. Navigate to Extensions > Apps Script
3. Rename the project to "Translate Slides"
4. Rename the Code.gs file to "translate"
5. Add a new HTML file named "sidebar"
6. Replace file contents with the provided code samples
7. Save all changes

## Implementation Files

**translate.gs** contains functions for:
- Creating the add-on menu via `onOpen()` event
- Managing installation with `onInstall()` event
- Displaying the sidebar interface
- Recursively extracting text from page elements
- Translating selected content using LanguageApp service

**sidebar.html** provides:
- Radio button selection for nine target languages
- Translation trigger button
- Error message display
- jQuery integration for DOM manipulation

## Running the Add-on

1. Reload your Slides presentation
2. Select Extensions > Translate Slides > Start
3. Authorize the add-on when prompted
4. Add text to slides and select it
5. Click "Translate" in the sidebar to replace text

## Next Steps

- Explore extending Google Slides with Apps Script
- Review Slides service reference documentation
