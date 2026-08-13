# Fix Errors in Your Converted Code

## Overview

The Google Apps Script Macro Converter automates VBA-to-Apps Script conversion but requires manual adjustments. The tool adds helper files to your project that define VBA constants, implement unconverted APIs, and resolve type variants.

## Key Files Added to Your Project

**Library.gs**: Contains function and constant definitions that replicate VBA functionality. Generally requires no modifications.

**Unimplemented_constructs.gs**: Addresses APIs and constructs the converter couldn't handle. "You likely need to modify this file to make your code work as intended."

**Variant_resolutions.gs**: Added when object types cannot be determined. Contains `__handle_resolve_<api>` functions that help determine object types at runtime.

## Finding Errors

Error messages reference specific file locations. In the V8 runtime, format is: `_api_name (filename:line:character)`. In Rhino runtime: `filename:line (_api_name)`.

## Error Types and Solutions

### Unimplemented APIs
These lack known workarounds. You must either implement a workaround using existing Apps Script APIs or remove the code. "If you can't find a way to implement the API in Apps Script, consider removing it from your code."

**Example solutions include**:
- Protecting chart data ranges instead of charts
- Creating custom object types to replicate unsupported VBA objects
- Using alternative Google Sheets APIs for similar functionality

### Unimplemented Language Constructs
VBA constructs like `GoTo`, `Declare`, `AddressOf`, and `Implements` aren't supported. Refactor code to use loops or conditional logic instead.

**Replace `GoTo` with loops**: Use `while` loops with labeled `break` or `continue` statements to achieve similar control flow.

### Partially Supported APIs
Some parameter values aren't supported. The converter adds validation that throws errors for unsupported values. Modify the error handler to return supported alternatives.

**Example**: Legend positions like `xlLegendPositionCustom` aren't supported; substitute with `xlLegendPositionBottom` or similar.

### Manual Work Needed
APIs can be converted with workarounds. Comments suggest equivalent Apps Script APIs to use. "Implement a workaround for the API to get the API to work as intended."

**Examples**:
- Use `onEdit` triggers with `createTextFinder` for auto-correct functionality
- Convert Excel files to Google Sheets and reference by spreadsheet ID for `workbook.open`

### Intentional Errors
These mimic VBA error behavior (like array out-of-bounds exceptions). No modifications needed; they ensure Apps Script behaves like the original code.

## Implementation Strategy

1. Locate errors using the provided line/character references
2. Read comments explaining the limitation
3. Implement a workaround using available APIs, or refactor your logic
4. Test thoroughly to ensure converted functionality matches original behavior

Source: https://developers.google.com/apps-script/guides/macro-converter/fix-conversion-errors
