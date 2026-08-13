# Address common issues

## Overview

This page documents challenges developers encounter when converting Visual Basic for Applications (VBA) to Apps Script using Google's Macro Converter tool.

## Key Issues

**Printing behavior:** VBA print commands like `PrintOut` convert to Apps Script but "prints to a file instead of a printer" requiring manual PDF printing, while `PrintToFile` saves PDFs to MyDrive.

**Unconverted features** requiring manual implementation include:
- Keyboard shortcuts and event-based triggers
- UserForms (dialog windows)
- Certain named range types

## Manual Workarounds

**For Userforms:** Create HTML files with form fields, then add Apps Script functions like `onOpen()` and `showForm()` to display them as sidebars in Sheets.

**For triggers:** 
- Keyboard shortcuts can be imported as macros
- `BeforeClose` events can use custom menus as alternatives
- `BeforeSave` events have no workaround due to Sheets' automatic saving

**For named ranges:** Excel Tables aren't supported in Sheets, but you can create matching named ranges pointing to the table's A1 notation range.

The documentation emphasizes that "Some events from VBA code, like BeforeClose or BeforeSave, don't have equivalents in Apps Script" and requires developers to implement creative solutions.

Source: https://developers.google.com/apps-script/guides/macro-converter/address-conversion-issues
